# Harness Engineering — GitHub Copilot Skill (v2.0)

> **O estado da arte em Spec-Driven Development, Multi-Agent Workflows e AI-Augmented Software Engineering.**
>
> Uma configuracao nativa para GitHub Copilot que transforma qualquer agente de IA em um arquiteto de Harness Engineering — projetando sistemas que ensinam, corrigem e validam agentes na construcao de software.

![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)
![Status: State of the Art](https://img.shields.io/badge/Status-State%20of%20the%20Art-brightgreen)
![Research: ~6,000 lines](https://img.shields.io/badge/Research-%7E6,000%20lines-blue)
![Date: April 2026](https://img.shields.io/badge/Date-April%202026-orange)

---

## O que e isto

Este projeto e uma **configuracao nativa para GitHub Copilot** baseada em ~6.000 linhas de pesquisa extensiva sobre as tres metodologias emergentes de engenharia de software com IA:

1. **Harness Engineering** — Projetar sistemas que ensinam e corrigem agentes
2. **Spec-Driven Development (SDD)** — Specs como fonte de verdade, nao documentacao pos-fato
3. **Multi-Agent Workflows** — Orquestracao inteligente de multiplos agentes

A equacao fundamental:

```
Agent = Model + Harness
```

O **modelo** (GPT-4, Claude, Gemini) e uma caixa preta que voce nao controla. O **harness** e tudo que voce constroi ao redor: prompts, ferramentas, contexto, restricoes, feedback loops, scaffolding.

> **Tese central:** A qualidade do software gerado por IA e determinada pela qualidade do harness, NAO pelo modelo em si.

---

## Arquitetura Copilot-Nativa

Este repositorio usa a arquitetura oficial do GitHub Copilot (2025/2026):

| Arquivo | Escopo | Funcao |
|---|---|---|
| `.github/copilot-instructions.md` | **Repositorio inteiro** | Contexto permanente: equacao fundamental, taxonomia do harness, fluxos de trabalho |
| `.github/instructions/discovery.instructions.md` | `**` (todos os arquivos) | Protocolo interativo de descoberta (4 fases, 13+ perguntas, 60+ por dominio) |
| `.github/instructions/sdd.instructions.md` | `**/*.md` | Regras SDD: formato EARS, anatomia de spec, quatro pilares |
| `.github/agents.md` | **Copilot Coding Agent** | Instrucoes especificas para o agente de implementacao |
| `AGENTS.md` | **Raiz (padrao aberto)** | Instrucoes permanentes para qualquer agente de IA |

### Por que esta estrutura?

- **Copilot detecta automaticamente** `.github/copilot-instructions.md` como contexto permanente
- **Instructions modulares** (`.github/instructions/`) permitem regras especificas por tipo de arquivo
- **`AGENTS.md` na raiz** segue o padrao aberto adotado por Claude Code, Cursor, e outros
- **Sem formato proprietario** — nao usa `.kiro/` (AWS Kiro) ou qualquer formato vendor-lock

---

## Funcionalidades

### Descoberta Interativa Profunda

Antes de gerar qualquer spec ou codigo, o agente conduz uma sessao de descoberta com **13+ perguntas em 4 fases**, mais **60+ perguntas condicionais por dominio**:

| Fase | Foco | Perguntas |
|---|---|---|
| **Fase 1** | Dominio e Contexto | 4 obrigatorias + condicionais |
| **Fase 2** | Escala e Complexidade | 3 obrigatorias + condicionais |
| **Fase 3** | Restricoes e Requisitos | 3 obrigatorias + condicionais |
| **Fase 4** | Design do Harness | 3 obrigatorias + condicionais |

**5 tecnicas de aprofundamento:**
- "Por que?" em cascata — chega na raiz do problema
- Cenário "E se..." — testa limites do sistema
- Trade-off explicito — forca escolhas conscientes
- Exemplo concreto — pede casos reais
- Anti-exemplo — descobre o que NAO fazer

### Spec-Driven Development (3 Niveis)

| Nivel | Nome | Descricao |
|---|---|---|
| **L1** | Spec-First | Escreve spec antes do codigo |
| **L2** | Spec-Anchored | Spec e gate obrigatorio |
| **L3** | Spec-as-Source | Spec e o unico artefato; codigo 100% gerado |

### Anatomia de Spec (Generico, sem vendor-lock)

```
specs/{feature}/
├── requirements.md    # EARS: "Quando <condicao>, o sistema SHALL <resposta>"
├── design.md          # Arquitetura, decisoes, trade-offs
└── tasks.md           # Checklist implementavel com traceabilidade
```

### Harness Sensors (Taxonomia Bockeler)

| Categoria | O que mede | Ferramentas |
|---|---|---|
| **Maintainability** | Legibilidade, estilo | ESLint, Prettier, SonarQube |
| **Architecture Fitness** | Conformidade arquitetural | ArchUnit, Dependency Cruiser |
| **Behaviour** | Correcao funcional | Jest, pytest, Playwright |
| **Computational** | Type safety, compilacao | tsc, mypy, pyright |
| **Inferencial** | Qualidade via LLM | LLM-as-judge, code review por agente |

### Multi-Agent Workflows (5 Padroes)

- **Sequential** — Dependencia linear
- **Fan-Out / Fan-In** — Paralelizacao de sub-tarefas
- **Orchestrator-Worker** — Divisao dinamica
- **Hierarchical** — Multi-camadas de gestao
- **Event-Driven** — Sistemas reativos assincronos

### Dominios Cobertos

- Data Engineering / Data Lakes (A-RAG, NL2SQL, auto-healing)
- API / Web Applications
- Infrastructure / CI-CD
- Mobile Applications
- AI / Machine Learning
- Security / Compliance

---

## Quick Start

### 1. Clone o projeto

```bash
git clone https://github.com/o-lino/harness-copilot-skill.git
cd harness-copilot-skill
```

### 2. Copie para seu projeto

```bash
# Na raiz do seu projeto:
cp harness-copilot-skill/AGENTS.md .
cp -r harness-copilot-skill/.github .
cp -r harness-copilot-skill/templates .
cp -r harness-copilot-skill/specs .
```

### 3. Inicie a descoberta interativa

Abra o Copilot e diga:

> "Vamos fazer a descoberta interativa para um novo projeto."

O agente fara as perguntas do protocolo, sintetizara suas respostas, e gerara specs precisas.

### 4. Para o guia completo

Leia `QUICKSTART.md` para inicio em 5 minutos.

---

## Estrutura do Projeto

```
harness-copilot-skill/
├── AGENTS.md                          # Instrucoes permanentes (padrao aberto)
├── QUICKSTART.md                      # Guia de inicio rapido (5 minutos)
├── README.md                          # Esta documentacao
├── CONTRIBUTING.md                    # Guia de contribuicao
├── LICENSE                            # Licenca MIT
│
├── .github/
│   ├── copilot-instructions.md        # Copilot: contexto permanente do repositorio
│   ├── agents.md                      # Copilot Coding Agent: regras de implementacao
│   └── instructions/
│       ├── discovery.instructions.md  # Protocolo interativo (4 fases, 70+ perguntas)
│       └── sdd.instructions.md        # Regras SDD, formato EARS, anatomia de spec
│
├── templates/
│   ├── sdd-requirements.md            # Template de requisitos EARS
│   ├── sdd-design.md                  # Template de design arquitetural
│   ├── sdd-tasks.md                   # Template de tasks implementaveis
│   ├── harness-sensors.yaml           # GitHub Actions com 5 sensors
│   ├── data-contract.md               # Template de contrato de dados
│   ├── agent-spec.md                  # Template de especificacao de agente
│   ├── multi-agent-workflow.md        # Template de orquestracao multi-agente
│   └── DISCOVERY-OUTPUT.md            # Template de captura de sessao de descoberta
│
├── examples/
│   ├── nivel1-ecommerce.md            # SDD L1 — Catalogo de produtos
│   ├── nivel2-api-microservice.md     # SDD L2 — Microservico de pedidos
│   ├── nivel3-full-system.md          # SDD L3 — Sistema de biblioteca
│   ├── data-pipeline-autohealing.md   # Pipeline com auto-healing
│   └── sessao-interativa.md           # Sessao interativa completa
│
└── specs/                             # Specs de features (formato generico)
    └── {feature}/
        ├── requirements.md
        ├── design.md
        └── tasks.md
```

---

## Como Funciona a Descoberta Interativa

### Fluxo Completo

```
FASE 1: Dominio e Contexto
  "Qual problema de negocio voce esta resolvendo?"
  "Quem sao os usuarios finais?"
  "O que ja existe?"
  "O que define SUCESSO?"
  + Perguntas condicionais por dominio
        |
        v
FASE 2: Escala e Complexidade
  "Qual o tamanho da codebase?"
  "Quantas pessoas/equipes?"
  "Qual nivel SDD? (L1/L2/L3)"
  + Perguntas condicionais por equipe
        |
        v
FASE 3: Restricoes e Requisitos
  "O que o sistema NAO PODE fazer?"
  "Quais sao as dependencias externas?"
  "Existe compliance/regulamentacao?"
  + Perguntas condicionais por risco
        |
        v
FASE 4: Design do Harness
  "Quais sensors de validacao sao essenciais?"
  "Qual padrao multi-agente se aplica?"
  "Qual o nivel de autonomia do agente?"
  + Perguntas condicionais por sensor
        |
        v
SINTESE + CONFIRMACAO
  1. Agente apresenta resumo das respostas
  2. Usuario confirma ou ajusta
  3. Agente gera spec (requirements.md, design.md, tasks.md)
        |
        v
GERACAO DA SPEC
  requirements.md (EARS)
  design.md (arquitetura)
  tasks.md (implementacao)
```

### Exemplo Real

Veja `examples/sessao-interativa.md` para uma sessao completa — de "Preciso de um sistema de estoque" ate uma spec precisa com arquitetura serverless, integracao Shopify e custo de ~$5/mes.

---

## Guia de Arquivos

| Arquivo | Quando usar | Conteudo |
|---|---|---|
| **QUICKSTART.md** | Primeiro acesso | Guia de 5 minutos para comecar |
| **AGENTS.md** | Sempre (Copilot le auto) | Instrucoes permanentes para agentes |
| `.github/copilot-instructions.md` | Automatico (Copilot) | Contexto permanente do repositorio |
| `.github/instructions/discovery.instructions.md` | Automatico (todos arquivos) | Protocolo de descoberta interativa |
| `.github/instructions/sdd.instructions.md` | Automatico (*.md) | Regras SDD e formato EARS |
| `.github/agents.md` | Automatico (Coding Agent) | Regras de implementacao |
| **templates/** | Ao iniciar projeto/feature | Templates reutilizaveis com guided questions |
| **examples/** | Para ver na pratica | 5 exemplos de SDD L1-L3 e auto-healing |

---

## Harness por Escala

| Tamanho da Codebase | Abordagem Recomendada |
|---|---|
| Menos de 100K linhas | AGENTS.md + bom contexto |
| 100K a 1M linhas | Thin harness: task routing + context scoping |
| 1M a 10M linhas | Platform harness (servicos dedicados) |
| 10M+ linhas | Build your own agent platform |

---

## Referencias da Pesquisa

Esta skill foi construida a partir de ~6.000 linhas de pesquisa extensiva:

| Arquivo Original | Conteudo |
|---|---|
| 01_pesquisa_harness_sdd_multiagent.md | Fundamentos teoricos de Harness, SDD e Multi-Agent |
| 02_padroes_templates_implementacao.md | Templates, patterns e guias de implementacao |
| 03_implementacao_consultoria_dados.md | Data consulting: NL2SQL, auto-healing, dashboards |
| 04_implementacao_empresa.md | Enterprise rollout: GitHub Actions a Harness.io |
| 05_harness_engineering_data_discovery_agent.md | Blueprint A-RAG para Data Discovery com 60k ativos |
| exemplos/01_nivel1_simples.md | Exemplo SDD L1 — Projeto simples |
| exemplos/02_nivel2_intermediario.md | Exemplo SDD L2 — Projeto intermediario |
| exemplos/03_nivel3_avancado.md | Exemplo SDD L3 — Projeto avancado |
| exemplos/04_problemas_negocio.md | Problemas de negocio resolvidos com Harness |

### Fontes Academicas e Industriais

- **Mitchell Hashimoto** (HashiCorp co-founder) — "Harness Engineering" blog post, Feb 2026
- **Ryan Lopopolo / OpenAI** — Internal software construction process, Feb 2026
- **Birgitta Bockeler / ThoughtWorks** — Harness taxonomy (Guides + Sensors), Martin Fowler Blog
- **Alex Rezvov** — Spec-Driven Development four pillars
- **Temporal + LangGraph** — Outer/inner loop architecture for multi-agent orchestration

---

## Licenca

MIT License. Veja [LICENSE](LICENSE) para detalhes.

---

*Esta skill foi gerada a partir de ~6.000 linhas de pesquisa extensiva sobre o estado da arte em Harness Engineering, Spec-Driven Development e Multi-Agent Workflows — Abril 2026.*
