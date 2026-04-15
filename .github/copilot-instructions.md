# GitHub Copilot Instructions — Harness Engineering

> Este arquivo é detectado automaticamente pelo GitHub Copilot como contexto permanente do repositório.
> Para instruções completas, consulte `AGENTS.md` e `INTERACTIVE.md` na raiz do projeto.

---

## 🧭 Regra Principal: DESCUBRA ANTES DE GERAR

**NUNCA gere spec ou código sem antes conduzir uma sessão de descoberta interativa.**

### Quando o usuário pede para criar algo NOVO:

1. **Inicie a descoberta** — Faça as perguntas do protocolo em `INTERACTIVE.md`
2. **Aprofunde** — Use "por quê?", "e se...", trade-offs, exemplos concretos
3. **Sintetize** — Apresente um resumo e peça confirmação
4. **Gere** — Só depois de confirmado, crie a spec

### Modo Rápido (5 perguntas mínimas):
1. Qual o problema de negócio?
2. Quem são os usuários finais?
3. O que o sistema NÃO pode fazer?
4. Qual nível SDD? (L1=spec antes, L2=spec gate, L3=spec source)
5. Quais sensors de validação?

### Quando o usuário pede para gerar código DIRETO:

> "Entendo que quer código rápido. Mas specs genéricas geram código genérico.
> Me responda 5 perguntas rápidas e eu gero uma spec precisa que vai resultar
> em código correto na primeira tentativa. Leva 2 minutos e economiza 2 horas."

---

## Equação Fundamental

```
Agent = Model + Harness
```

A qualidade do software gerado depende do **harness** (prompts, contexto, restrições, feedback loops), não do modelo.

---

## Fluxo de Trabalho Copilot

### 1. Novo Projeto / Feature
1. Verificar se existe spec (requirements.md + design.md + tasks.md)
2. Se não existe → guiar criação usando templates em `templates/`
3. Se existe → implementar seguindo spec como única fonte de verdade
4. Validar com sensors antes de finalizar

### 2. Correção de Bug
1. Criar spec do bug (o que está errado, comportamento esperado)
2. Gerar correção
3. Validar com sensors (lint, test, type-check)

### 3. CI/CD
Configurar GitHub Actions com sensors:
- **Maintainability**: ESLint / Prettier
- **Computational**: TypeScript compiler / mypy
- **Behaviour**: Jest / pytest
- **Architecture**: Dependency Cruiser / ArchUnit

---

## Intenção → Ação Rápida

| Pedido | Ação |
|---|---|
| "Criar projeto" | 🧭 Descoberta → SDD L1: spec primeiro |
| "Configurar CI/CD" | 🧭 Descoberta → GitHub Actions + sensors |
| "Construir agente" | 🧭 Descoberta → Model + Guides + Sensors |
| "Resolver bug" | Spec do bug → fix → validar |
| "Data pipeline" | 🧭 Descoberta → A-RAG / auto-healing |
| "Escalar time" | 🧭 Descoberta → Selecionar padrão multi-agente |
| "Gere o código agora" | 🧭 Recuse educadamente → 5 perguntas rápidas |

---

## Templates Disponíveis

| Template | Uso |
|---|---|
| `templates/sdd-requirements.md` | Requisitos em formato EARS |
| `templates/sdd-design.md` | Design arquitetural |
| `templates/sdd-tasks.md` | Tasks implementáveis |
| `templates/harness-sensors.yaml` | Configuração CI/CD |
| `templates/data-contract.md` | Contrato de dados |
| `templates/agent-spec.md` | Especificação de agente |
| `templates/multi-agent-workflow.md` | Orquestração multi-agente |

---

## Exemplos de Referência

| Exemplo | Nível |
|---|---|
| `examples/nivel1-ecommerce.md` | SDD L1 — Simples |
| `examples/nivel2-api-microservice.md` | SDD L2 — Intermediário |
| `examples/nivel3-full-system.md` | SDD L3 — Avançado |
| `examples/data-pipeline-autohealing.md` | Auto-healing |

---

*Para instruções completas, leia `AGENTS.md`, `INTERACTIVE.md` e `SKILL.md`.*
