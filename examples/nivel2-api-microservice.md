# Exemplo SDD Nível 2 — Microserviço de Pedidos (API REST)

## Contexto

Microserviço responsável por processar pedidos de um e-commerce. Deve validar estoque, calcular frete e persistir o pedido.

**Nível SDD:** L2 (Spec-Anchored) — O agente NÃO pode tocar no código sem uma spec aprovada. A spec é gate obrigatório.

---

## Spec (Aprovada antes do código)

### requirements.md
```markdown
## Requisitos
### RF-001: Criar Pedido
- Quando o cliente submeter um pedido com itens válidos,
- O sistema SHALL verificar disponibilidade de estoque,
- O sistema SHALL calcular o frete total,
- O sistema SHALL persistir o pedido com status "pendente".

### RF-002: Consultar Pedido
- Quando o cliente solicitar `/pedidos/{id}`,
- O sistema SHALL retornar o pedido completo com itens e frete.
```

### design.md
```markdown
- Arquitetura: Microserviço isolado
- Comunicação: REST + RabbitMQ para eventos
- Banco: PostgreSQL
- Validação: Zod para input schema
- Testes: Integração com testcontainers
```

---

## Harness

### Guides
- Spec aprovada em `specs/pedidos/` (gate obrigatório)
- `AGENTS.md` com regra: "NÃO escreva código sem spec aprovada"

### Sensors
| Sensor | Ferramenta | Gate |
|---|---|---|
| Spec Check | Script customizado | CI bloqueia se spec não existe |
| Maintainability | ESLint + SonarQube | Quality gate A |
| Computational | TypeScript strict | Zero `any` permitido |
| Behaviour | Jest + testcontainers | 80% cobertura |
| Architecture | Dependency Cruiser | Sem import circular |

---

## Implementação

```typescript
// src/services/pedido.service.ts
import { z } from 'zod';
import { db } from '../db';
import { estoqueClient } from '../clients/estoque';
import { freteCalculator } from '../lib/frete';

const PedidoSchema = z.object({
  customerId: z.string().uuid(),
  itens: z.array(z.object({
    produtoId: z.string().uuid(),
    quantidade: z.number().int().positive(),
  })),
  endereco: z.object({
    cep: z.string().length(8),
  }),
});

export async function criarPedido(input: z.infer<typeof PedidoSchema>) {
  // 1. Verificar estoque (RF-001)
  for (const item of input.itens) {
    const disponivel = await estoqueClient.verificar(item.produtoId, item.quantidade);
    if (!disponivel) throw new Error(`Produto ${item.produtoId} sem estoque`);
  }

  // 2. Calcular frete (RF-001)
  const frete = freteCalculator.calcular(input.endereco.cep, input.itens.length);

  // 3. Persistir pedido (RF-001)
  const pedido = await db.pedido.create({
    data: {
      customerId: input.customerId,
      itens: { create: input.itens },
      frete,
      status: 'pendente',
    },
  });

  return pedido;
}
```

---

## Validação

```bash
# Sensor: Spec Check (obrigatório no L2)
node scripts/check-spec.js   # ✅ Spec aprovada encontrada

# Sensor: TypeScript strict
npx tsc --noEmit --strict    # ✅ 0 errors, 0 any

# Sensor: Tests
npm test                     # ✅ 12/12 passing, 85% coverage

# Sensor: Architecture
npx depcruise src            # ✅ 0 violations
```

---

## Lições

- **Funcionou:** Zod garantiu type safety nos inputs. Spec aprovada evitou scope creep.
- **Melhorar:** Faltou tratamento de retry se o serviço de estoque estiver indisponível.
- **Próximo:** Adicionar circuit breaker no cliente de estoque e idempotência no POST.
