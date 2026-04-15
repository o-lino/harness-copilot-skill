---
trigger: always_on
applyTo: '**/*.md'
---

# Spec-Driven Development (SDD) - Instrucoes

> Estas instrucoes se aplicam a todos os arquivos Markdown do repositorio.
> Definem como specs devem ser criadas, mantidas e usadas como fonte de verdade.

---

## Principio Fundamental

TRADICIONAL:  Codigo - Testes - Documentacao
SDD:          Spec - IA gera Codigo - Spec e a Verdade

**A spec e a unica fonte de verdade.** Todo codigo implementado deve ser rastreavel a um requisito da spec. Codigo sem spec correspondente e divida tecnica.

---

## Niveis de Maturidade SDD

| Nivel | Nome | Descricao | Quando usar |
|---|---|---|---|
| **L1** | Spec-First | Escreve spec antes do codigo (manual) | Times iniciando SDD |
| **L2** | Spec-Anchored | Spec e gate obrigatoria antes do codigo | Times com maturidade |
| **L3** | Spec-as-Source | Spec e o unico artefato; codigo 100%% gerado | Automacao avancada |

---

## Quatro Pilares do SDD

1. **Traceability** - Cada linha de codigo rastreia ate um requisito da spec
2. **DRY** - Spec e a unica fonte de verdade, nao duplicada em documentacao
3. **Deterministic Enforcement** - Regras verificaveis mecanicamente via sensors
4. **Parsimony** - Specs minimas: necessario sem over-specifying

---

## Anatomia de Spec

Toda spec vive em specs/feature/ com exatamente 3 arquivos:

specs/feature/
- requirements.md    # Requisitos em formato EARS
- design.md          # Arquitetura, decisoes, trade-offs
- tasks.md           # Checklist implementavel

---

## Formato EARS (Easy Approach to Requirements Syntax)

Use o formato EARS para escrever requisitos verificaveis:

Quando CONDICAO, o sistema SHALL RESPOSTA.

### Exemplos Corretos

- Quando o usuario submete uma query, o sistema SHALL retornar as top 10 tabelas mais relevantes em ate 2 segundos.
- Quando um pipeline falha, o sistema SHALL registrar o erro e notificar o Data Owner em ate 5 minutos.

### Exemplos Incorretos

- O sistema deve ser rapido. (vago, nao verificavel)
- O sistema devera processar dados. (sem condicao, sem resposta especifica)

---

## Regras de Ouro

1. **SEMPRE verifique se existe spec antes de escrever codigo.**
   - Se nao existe - guie a criacao primeiro (requirements.md minimo)
   - Se existe - use-a como unica fonte de verdade (DRY)
   - Apos implementacao - valide com sensors

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

*Instrucoes SDD - Parte da Harness Engineering Skill v2.0*
