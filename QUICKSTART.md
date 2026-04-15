# 🚀 Quick Start — Harness Engineering Copilot Skill

> Use este guia para começar a usar a skill **AGORA** — em menos de 5 minutos.

---

## Opção 1: Modo Rápido (5 minutos)

Para quando você já sabe o que quer e precisa de uma spec rápida.

### Passo 1: Responda 5 perguntas

Copie e preencha:

```
1. Problema: {o que está tentando resolver?}
2. Usuários: {quem vai usar?}
3. NÃO PODE: {restrições críticas?}
4. SDD Level: L1 (spec antes) | L2 (spec gate) | L3 (spec source)
5. Sensors: lint | type-check | tests | architecture | security
```

### Passo 2: Copie os arquivos para seu projeto

```bash
# Na raiz do seu projeto:
cp harness-copilot-skill/AGENTS.md .
cp -r harness-copilot-skill/.github .
cp -r harness-copilot-skill/templates .
```

### Passo 3: Inicie com um template

```bash
cp templates/sdd-requirements.md specs/specs/{feature}/requirements.md
cp templates/sdd-design.md specs/specs/{feature}/design.md
cp templates/sdd-tasks.md specs/specs/{feature}/tasks.md
```

### Passo 4: Preencha a spec com suas respostas

Use as respostas das 5 perguntas para preencher os templates.

### Passo 5: Peça ao Copilot para gerar código

Com a spec preenchida, peça ao Copilot:
> "Gere o código seguindo a spec em `specs/specs/{feature}/`"

---

## Opção 2: Modo Profundo (15-30 minutos)

Para projetos complexos, enterprise, ou quando você não tem clareza total.

### Passo 1: Abra o protocolo completo

Leia `INTERACTIVE.md` — contém 4 fases com 13+ perguntas.

### Passo 2: Conduza a sessão interativa

O agente (Copilot) fará as perguntas automaticamente. Responda honestamente.

### Passo 3: Receba o resumo de descoberta

O agente vai apresentar um resumo. Confira e ajuste.

### Passo 4: Receba a spec gerada

O agente gera `requirements.md`, `design.md` e `tasks.md` baseado nas suas respostas.

### Passo 5: Configure o harness

Use o template `templates/harness-sensors.yaml` para configurar CI/CD.

### Passo 6: Implemente com validação

O agente gera código → sensors validam → se falha → agente corrige → repete.

---

## Estrutura de Arquivos Recomendada

```
seu-projeto/
├── AGENTS.md                          # ← Copie de harness-copilot-skill/
├── .github/
│   ├── copilot-instructions.md        # ← Copie de harness-copilot-skill/.github/
│   └── workflows/
│       └── harness-ci.yaml            # ← Baseado em templates/harness-sensors.yaml
├── specs/
│   └── specs/
│       └── {feature}/
│           ├── requirements.md        # ← Gerado a partir do template
│           ├── design.md              # ← Gerado a partir do template
│           └── tasks.md               # ← Gerado a partir do template
├── src/                               # ← Código gerado pelo agente
├── tests/                             # ← Tests gerados pelo agente
└── docs/                              # ← Docs gerados da spec
```

---

## Cheat Sheet: Comandos do Copilot

| O que você quer | O que dizer ao Copilot |
|---|---|
| Iniciar projeto novo | "Vamos fazer a descoberta interativa para um novo projeto" |
| Criar nova feature | "Preciso de uma spec para {feature}. Vamos fazer a descoberta?" |
| Gerar código | "Gere o código seguindo a spec em `specs/specs/{feature}/`" |
| Configurar CI/CD | "Configure os harness sensors baseado no meu projeto" |
| Corrigir bug | "Crie uma spec para este bug: {descrição}" |
| Data pipeline | "Vamos fazer a descoberta para um data pipeline" |
| Revisar código | "Valide este código contra a spec usando os sensors" |

---

## Referências Rápidas

| Arquivo | O que é | Quando ler |
|---|---|---|
| `AGENTS.md` | Instruções permanentes | Sempre (Copilot lê automaticamente) |
| `SKILL.md` | Guia completo do skill | Para entender todos os conceitos |
| `INTERACTIVE.md` | Protocolo de descoberta | Antes de qualquer spec nova |
| `templates/` | Templates reutilizáveis | Ao iniciar qualquer projeto/feature |
| `examples/` | Exemplos práticos | Para ver como funciona na prática |

---

## Checklist de Primeiro Uso

- [ ] Copiei `AGENTS.md` para a raiz do projeto
- [ ] Copiei `.github/copilot-instructions.md`
- [ ] Criei `specs/specs/{feature}/` com os 3 arquivos de spec
- [ ] Preenchi a spec com dados reais do projeto
- [ ] Configurei CI/CD com sensors (pelo menos lint + type-check + tests)
- [ ] Pedi ao Copilot para gerar código a partir da spec
- [ ] Validei o código gerado com sensors

---

*Para o guia completo, leia `SKILL.md`. Para o protocolo de descoberta, leia `INTERACTIVE.md`.*
