# Skill: Spec-Driven Development (SDD)

> **Tipo:** Skill reutilizavel
> **Local:** `.github/skills/sdd/SKILL.md`
> **Uso:** Invocar durante a fase de geracao de specs, apos a descoberta interativa.
> **Pre-requisito:** `.github/skills/discovery/SKILL.md` (sempre descubra antes de gerar specs)

---

## Quando Usar

Use esta skill quando:
- O usuario confirmou o resumo de descoberta e autorizou a geracao de specs
- Precisa criar `requirements.md`, `design.md` ou `tasks.md` para uma feature
- Precisa aplicar formato EARS em requisitos
- Precisa estabelecer traceabilidade entre codigo e specs
- Precisa validar se uma spec esta completa e correta

## Quando NAO Usar

Nao use quando:
- A descoberta interativa ainda nao foi concluida (use `.github/skills/discovery/SKILL.md` primeiro)
- O usuario pede uma correcao trivial sem impacto em requisitos
- Uma spec ja existe e esta atualizada - apenas siga-a

---

## Os 4 Pilares do SDD

### 1. Traceability
Cada linha de codigo rastreia ate um requisito da spec. Nao existe codigo sem spec correspondente.

### 2. DRY (Don't Repeat Yourself)
A spec e a **unica** fonte de verdade. Nao duplique requisitos em documentacao, comentarios ou tickets.

### 3. Deterministic Enforcement
Regras devem ser verificaveis mecanicamente via sensors (lint, type check, tests). Se nao pode ser validado automaticamente, nao e um requisito.

### 4. Parsimony
Specs devem ser minimas: inclua o necessario, nao o desejavel. Over-specifying gera codigo over-engineered.

---

## Anatomia de Spec

Toda spec vive em `specs/{feature}/` com exatamente 3 arquivos:

```
specs/{feature}/
├── requirements.md    # Requisitos em formato EARS
├── design.md          # Arquitetura, decisoes, trade-offs, diagramas
└── tasks.md           # Checklist implementavel com dependencias e criterios
```

### requirements.md
- Lista de requisitos funcionais (RF) e nao-funcionais (RNF)
- Todos em formato EARS
- Cada requisito tem um identificador unico (RF-001, RF-002...)

### design.md
- Arquitetura proposta
- Decisoes arquiteturais com trade-offs
- Diagramas (ASCII ou referencias)
- Riscos e mitigacoes

### tasks.md
- Lista de tasks implementaveis (T-001, T-002...)
- Cada task referencia um ou mais requisitos
- Dependencias entre tasks
- Criterios de aceite por task

---

## Formato EARS (Easy Approach to Requirements Syntax)

### Template
```
Quando CONDICAO, o sistema SHALL RESPOSTA.
```

### Tipos de EARS

| Tipo | Template | Exemplo |
|---|---|---|
| **Ubiquitous** | O sistema SHALL resposta. | O sistema SHALL registrar todas as queries executadas. |
| **Event-Driven** | Quando condicao, o sistema SHALL resposta. | Quando o usuario submete uma query, o sistema SHALL retornar as top 10 tabelas em ate 2s. |
| **State-Driven** | Enquanto estado, o sistema SHALL resposta. | Enquanto o pipeline estiver em execucao, o sistema SHALL atualizar o status a cada 30s. |
| **Optional** | Onde feature esta ativa, o sistema SHALL resposta. | Onde o modulo de cache esta ativo, o sistema SHALL invalidar o cache apos 5min. |
| **Unwanted** | O sistema NAO SHALL resposta. | O sistema NAO SHALL expor dados PII em logs. |

### Exemplos Corretos

- Quando o usuario submete uma query, o sistema SHALL retornar as top 10 tabelas mais relevantes em ate 2 segundos.
- Quando um pipeline falha, o sistema SHALL registrar o erro e notificar o Data Owner em ate 5 minutos.
- O sistema NAO SHALL armazenar senhas em texto puro.
- Enquanto a conexao com o banco estiver ativa, o sistema SHALL manter um health check a cada 10 segundos.

### Exemplos Incorretos

- O sistema deve ser rapido. (vago, nao verificavel)
- O sistema devera processar dados. (sem condicao, sem resposta especifica)
- O sistema precisa ser seguro. (subjetivo, nao testavel)
- Boa performance e essencial. (sem metrica)

### Checklist de Qualidade EARS

- [ ] Comeca com "Quando", "Enquanto", "Onde" ou "O sistema"
- [ ] Contem "SHALL" (obrigatorio) ou "NAO SHALL" (proibicao)
- [ ] A resposta e verificavel mecanicamente
- [ ] Contem metricas quando aplicavel (tempo, volume, percentual)
- [ ] Nao usa termos vagos (rapido, bom, eficiente, robusto)

---

## Niveis de Maturidade SDD

| Nivel | Nome | Descricao | Quando usar |
|---|---|---|---|
| **L1** | Spec-First | Escreve spec antes do codigo (manual) | Times iniciando SDD |
| **L2** | Spec-Anchored | Spec e gate obrigatorio antes do codigo | Times com maturidade |
| **L3** | Spec-as-Source | Spec e o unico artefato; codigo 100% gerado | Automacao avancada |

### Como identificar o nivel do projeto

Durante a descoberta (fase 2, pergunta 7), o usuario seleciona o nivel. Aplique as regras correspondentes:

**L1 (Spec-First):**
- Gere requirements.md minimo antes de qualquer codigo
- Permita divergencia com anotacao de motivo
- Encoraje evolucao para L2

**L2 (Spec-Anchored):**
- Spec e gate obrigatorio - sem spec aprovada, sem codigo
- Cada PR deve referenciar a spec correspondente
- CI rejeita PRs sem link para spec

**L3 (Spec-as-Source):**
- Spec e o unico artefato de entrada
- Codigo e 100% gerado pela IA
- Validacao feita exclusivamente via sensors
- Rollback automatico se sensors falharem

---

## Protocolo de Geracao de Spec

### Passo 1: Leia o Resumo de Descoberta
O resumo de descoberta (gerado pela discovery skill) contem: dominio, escala, restricoes, e design do harness.

### Passo 2: Crie requirements.md
- Liste requisitos funcionais (RF-001, RF-002...) em formato EARS
- Liste requisitos nao-funcionais (RNF-001...) com metricas
- Defina prioridades: Alta, Media, Baixa

### Passo 3: Crie design.md
- Descreva a arquitetura proposta
- Documente decisoes com trade-offs
- Liste riscos e mitigacoes

### Passo 4: Crie tasks.md
- Liste tasks implementaveis (T-001, T-002...)
- Cada task referencia um ou mais requisitos
- Mapeie dependencias entre tasks
- Defina criterios de aceite

### Passo 5: Estabeleca Traceabilidade
Verifique que:
- [ ] Cada task referencia pelo menos um requisito
- [ ] Cada requisito tem pelo menos uma task
- [ ] Nao existem tasks orfas (sem requisito)
- [ ] Nao existem requisitos orfos (sem task)

### Passo 6: Apresente para Confirmacao
Antes de implementar, apresente as specs ao usuario e aguarde aprovacao.

---

## Traceabilidade em Codigo

Todo arquivo de codigo gerado a partir de uma spec DEVE incluir no topo:

```
# Task: T-001 - Data source connector
# Spec: specs/data-discovery/requirements.md
# Requisito: RF-001, RF-002
```

Cada funcao publica deve referenciar o requisito na docstring.

---

## Regras de Ouro

1. **SEMPRE verifique se existe spec antes de escrever codigo.**
   - Se nao existe -> guie a criacao primeiro (requirements.md minimo)
   - Se existe -> use-a como unica fonte de verdade (DRY)
   - Apos implementacao -> valide com sensors

2. **NUNCA modifique codigo sem atualizar a spec correspondente.**
   - Mudanca no codigo sem atualizar a spec = divida tecnica
   - Spec desatualizada e pior que sem spec

3. **Traceabilidade e obrigatoria.**
   - Cada task em tasks.md deve rastrear para um RF em requirements.md
   - Cada arquivo de codigo deve mencionar a task implementada

4. **Specs devem ser minimas mas completas.**
   - Inclua o necessario, nao o desejavel
   - Se um requisito nao e verificavel mecanicamente, nao e um requisito

---

## Validacao de Spec

### Checklist de requirements.md
- [ ] Todos os requisitos usam formato EARS
- [ ] Cada requisito tem identificador unico (RF-XXX ou RNF-XXX)
- [ ] Nao ha requisitos vagos ou nao-verificaveis
- [ ] Metricas estao definidas quando aplicavel

### Checklist de design.md
- [ ] Arquitetura esta descrita claramente
- [ ] Trade-offs foram documentados
- [ ] Riscos foram identificados com mitigacoes

### Checklist de tasks.md
- [ ] Cada task referencia pelo menos um requisito
- [ ] Dependencias entre tasks estao mapeadas
- [ ] Criterios de aceite estao definidos
- [ ] Nao ha tasks orfas ou requisitos orfos

---

## Referencias Cruzadas

| Arquivo | Caminho | Funcao |
|---|---|---|
| Agente Principal | `.github/agents/harness-architect.agent.md` | Orquestrador do fluxo |
| Discovery Skill | `.github/skills/discovery/SKILL.md` | Protocolo de descoberta (use PRIMEIRO) |
| SDD Instructions | `.github/instructions/sdd.instructions.md` | Regras contextuais SDD |
| Copilot Instructions | `.github/copilot-instructions.md` | Instrucoes gerais do repositorio |
| AGENTS.md | `AGENTS.md` (raiz) | Instrucoes permanentes |
| Templates | `templates/sdd-*.md` | Templates de spec reutilizaveis |

---

*SDD Skill - Harness Engineering v3.0*