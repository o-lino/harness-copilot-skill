# Exemplo SDD Nível 1 — Catálogo de Produtos (E-commerce)

## Contexto

Uma loja online precisa de um CRUD básico para gerenciar produtos: nome, preço, descrição, categoria.

**Nível SDD:** L1 (Spec-First) — A spec é escrita antes do código, mas o código pode divergir se o desenvolvedor decidir.

---

## Spec

### requirements.md
```markdown
## User Stories
- Como vendedor, quero cadastrar produtos para que apareçam no catálogo.
- Como cliente, quero filtrar por categoria para encontrar produtos relevantes.

## Requisitos (EARS)
### RF-001: Cadastrar Produto
- Quando o vendedor submeter dados válidos,
- O sistema SHALL criar o produto e retornar seu ID.
- Critério: status 201, body contém id e dados enviados.

### RF-002: Listar Produtos por Categoria
- Quando o cliente solicitar `/produtos?categoria=X`,
- O sistema SHALL retornar apenas produtos daquela categoria.
- Critério: array com produtos filtrados, status 200.
```

### design.md
```markdown
- Backend: Node.js + Express
- Banco: PostgreSQL com Prisma ORM
- Endpoint: GET/POST /api/produtos
```

---

## Harness

### Guides
- `AGENTS.md` na raiz (instruções permanentes)
- Spec em `specs/catalogo/`

### Sensors
| Sensor | Ferramenta | Gate |
|---|---|---|
| Maintainability | ESLint | CI bloqueia se warnings > 0 |
| Computational | TypeScript | `tsc --noEmit` |
| Behaviour | Jest | 5 testes mínimos |

---

## Implementação

O agente gera:
```typescript
// src/routes/produtos.ts
import { Router } from 'express';
import { db } from '../db';

const router = Router();

router.post('/', async (req, res) => {
  const { nome, preco, descricao, categoria } = req.body;
  const produto = await db.produto.create({ data: { nome, preco, descricao, categoria } });
  res.status(201).json(produto);
});

router.get('/', async (req, res) => {
  const { categoria } = req.query;
  const where = categoria ? { categoria } : {};
  const produtos = await db.produto.findMany({ where });
  res.json(produtos);
});

export default router;
```

---

## Validação

```bash
# Sensor: Type Check
npx tsc --noEmit        # ✅ PASS

# Sensor: Tests
npm test                # ✅ 5/5 passing

# Sensor: Lint
npm run lint            # ✅ 0 warnings
```

---

## Lições

- **Funcionou:** Spec clara em EARS gerou código correto na primeira iteração.
- **Melhorar:** Faltou requisito de validação de preço (número positivo).
- **Próximo:** Adicionar RF-003: validar preço > 0 antes de criar.
