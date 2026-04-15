# Exemplo SDD Nível 3 — Sistema Completo Gerado da Spec

## Contexto

Sistema de gestão de biblioteca: empréstimos, devoluções, reservas e multas. 100% do código é gerado a partir da spec. O humano apenas escreve e aprova specs.

**Nível SDD:** L3 (Spec-as-Source) — A spec é o ÚNICO artefato mantido manualmente. Todo código, testes e docs são derivados.

---

## Spec (Único artefato mantido pelo humano)

### requirements.md
```markdown
## User Stories
- Como bibliotecário, quero registrar empréstimos para controlar acervo.
- Como usuário, quero reservar livros indisponíveis.
- Como sistema, quero calcular multas por atraso automaticamente.

## Requisitos
### RF-001: Emprestar Livro
- Quando o bibliotecário registrar um empréstimo,
- O sistema SHALL verificar se o livro está disponível,
- O sistema SHALL verificar se o usuário não tem multas ativas,
- O sistema SHALL criar o empréstimo com data de devolução (14 dias).

### RF-002: Devolver Livro
- Quando o bibliotecário registrar uma devolução,
- O sistema SHALL calcular multa se houver atraso (R$2/dia),
- O sistema SHALL atualizar status do livro para "disponível".

### RF-003: Reservar Livro
- Quando o usuário solicitar reserva de livro indisponível,
- O sistema SHALL adicionar à fila de reservas.
- O sistema SHALL notificar o primeiro da fila quando disponível.
```

### design.md
```markdown
- Arquitetura: Monólito modular
- Backend: Python + FastAPI
- Banco: PostgreSQL + SQLAlchemy
- Fila: Redis (reservas)
- Notificação: Email via SMTP
```

---

## Harness

### Guides
- Spec em `.kiro/specs/biblioteca/` — ÚNICO input humano
- Prompt do agente: "Gere TODO o código, testes e docs a partir desta spec"

### Sensors (loop automático)
```
Agente gera código → Sensors validam → Se falha → Agente corrige → Repete
```

| Sensor | Ferramenta | Loop de Correção |
|---|---|---|
| Type Check | mypy | Auto-correção até passar |
| Lint | ruff | Auto-correção até passar |
| Tests | pytest | Re-gera até 100% passar |
| Coverage | pytest-cov | Mínimo 90% |

---

## Código Gerado (100% pela IA)

O agente, a partir da spec, gerou:

```
biblioteca/
├── src/
│   ├── models/          # SQLAlchemy models (auto-gerados)
│   ├── services/        # Business logic (auto-gerada)
│   ├── routes/          # FastAPI endpoints (auto-gerados)
│   └── notifications/   # Email service (auto-gerado)
├── tests/               # Testes (auto-gerados da spec)
├── docs/                # Documentação (auto-gerada da spec)
└── .kiro/specs/         # Spec (único artefato humano)
```

```python
# src/services/emprestimo.py — Gerado pela IA a partir de RF-001
from datetime import date, timedelta

class EmprestimoService:
    PRAZO_DIAS = 14
    MULTA_POR_DIA = 2.0

    def criar_emprestimo(self, livro_id: str, usuario_id: str) -> Emprestimo:
        livro = self.repo.get_livro(livro_id)
        if not livro.disponivel:
            raise LivroIndisponivelError(livro_id)

        usuario = self.repo.get_usuario(usuario_id)
        if usuario.multas_ativas:
            raise MultasAtivasError(usuario_id)

        devolucao = date.today() + timedelta(days=self.PRAZO_DIAS)
        return self.repo.create_emprestimo(livro_id, usuario_id, devolucao)

    def devolver(self, emprestimo_id: str) -> dict:
        emprestimo = self.repo.get_emprestimo(emprestimo_id)
        multa = self._calcular_multa(emprestimo)
        self._atualizar_livro(emprestimo.livro_id, 'disponivel')
        self._notificar_fila_reserva(emprestimo.livro_id)
        return {'multa': multa, 'status': 'devolvido'}
```

---

## Validação

```bash
# Sensor: mypy (auto-correção até passar)
mypy src/                   # ✅ PASS (3 iterações)

# Sensor: ruff
ruff check src/             # ✅ PASS (1 iteração)

# Sensor: pytest
pytest --cov=src --cov-min=90  # ✅ 45/45 passing, 94% coverage
```

---

## Lições

- **Funcionou:** Spec detalhada em EARS gerou código completo e testado.
- **Desafio:** A IA errou a lógica de multas na primeira iteração (usou dias úteis em vez de corridos). O sensor de teste pegou e a correção automática resolveu.
- **Conclusão:** L3 é viável quando a spec é detalhada e os sensors são robustos. O humano foca 100% na spec, não no código.
