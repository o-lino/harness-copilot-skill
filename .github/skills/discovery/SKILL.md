# Skill: Descoberta Interativa — Harness Engineering

> **Tipo:** Skill reutilizavel
> **Local:** .github/skills/discovery/SKILL.md
> **Uso:** Invocar antes de gerar qualquer spec ou codigo.

## Quando Usar

Use esta skill quando o usuario solicitar:
- Criar um novo projeto ou feature
- Resolver um problema complexo
- Construir um agente ou pipeline
- Qualquer situacao onde os requisitos nao estao claros

## Quando NAO Usar

Nao use quando:
- O usuario pede uma correcao simples de bug (crie spec do bug direto)
- Os requisitos ja estao documentados em uma spec existente
- E uma tarefa trivial (ex: renomear variavel)

## Protocolo de Descoberta

### Fluxo

```
FASE 1: Dominio e Contexto (4 perguntas obrigatorias)
    -> FASE 2: Escala e Complexidade (3 perguntas obrigatorias)
        -> FASE 3: Restricoes e Requisitos (3 perguntas obrigatorias)
            -> FASE 4: Design do Harness (3 perguntas obrigatorias)
                -> SINTESE + CONFIRMACAO
                    -> GERACAO DA SPEC
```

### FASE 1: Dominio e Contexto

**1. Qual problema de negocio voce esta resolvendo?**
Nao a solucao tecnica. O problema real.

**2. Quem sao os usuarios finais deste sistema?**

**3. Qual e o estado atual? O que ja existe?**

**4. O que define SUCESSO para este projeto?**
Metrica concreta. Algo mensuravel.

### FASE 2: Escala e Complexidade

**5. Qual o tamanho estimado da codebase?**
- < 100K linhas -> Harness simples
- 100K - 1M linhas -> Thin harness
- 1M - 10M linhas -> Platform harness
- 10M+ linhas -> Agent platform custom

**6. Quantas pessoas/equipes vao trabalhar neste projeto?**

**7. Qual o nivel de maturidade SDD desejado?**
- L1: Spec-First (escrevo spec antes do codigo)
- L2: Spec-Anchored (spec e gate obrigatorio)
- L3: Spec-as-Source (spec e o unico artefato)

### FASE 3: Restricoes e Requisitos

**8. O que o sistema NAO PODE fazer?**

**9. Quais sao as dependencias externas?**

**10. Existe compliance/regulamentacao aplicavel?**

### FASE 4: Design do Harness

**11. Quais sensors de validacao sao essenciais?**
- Maintainability (ESLint, Prettier)
- Computational (tsc, mypy, pyright)
- Behaviour (Jest, pytest, Playwright)
- Architecture Fitness (ArchUnit, dependency-cruiser)
- Data Quality (Great Expectations)
- Security (SAST, DAST, git-secrets)

**12. Qual padrao multi-agente se aplica?**
- Sequential, Fan-Out, Orchestrator-Worker, Hierarchical, ou Nenhum

**13. Qual o nivel de autonomia do agente?**
- Baixo (sugere), Medio (executa, humano revisa), Alto (executa e deploya)

## Pos-Descoberta

### 1. Gerar Resumo de Descoberta

```markdown
## Resumo de Descoberta

### Dominio
- Problema: {resposta 1}
- Usuarios: {resposta 2}
- Estado atual: {resposta 3}
- Sucesso = {resposta 4}

### Escala
- Codebase: {resposta 5}
- Equipe: {resposta 6}
- SDD Level: {resposta 7}

### Restricoes
- NAO PODE: {resposta 8}
- Dependencias: {resposta 9}
- Compliance: {resposta 10}

### Harness
- Sensors: {resposta 11}
- Multi-Agent: {resposta 12}
- Autonomia: {resposta 13}
```

### 2. Pedir Confirmacao

Com base nas suas respostas, projetei o seguinte harness. Confira se esta correto antes de eu gerar a spec:

- Nivel SDD: L1/L2/L3
- Sensors: lista
- Padrao: padrao multi-agente
- Restricoes criticas: lista

Esta correto? Posso ajustar algo antes de gerar?

### 3. Gerar a Spec

So apos confirmacao, gerar specs usando `.github/skills/sdd/SKILL.md`:
- specs/feature/requirements.md
- specs/feature/design.md
- specs/feature/tasks.md

## Tecnicas de Aprofundamento

### 1. Por que? em Cascata
Pergunte por que ate chegar na raiz.

### 2. Cenario E se...
Teste limites comenarios hipoteticos.

### 3. Trade-off Explicito
Force escolhas conscientes.

### 4. Exemplo Concreto
Peca casos reais.

### 5. Anti-Exemplo
Descubra o que NAO deve acontecer.

## Modo Rapido (5 perguntas)

Para projetos simples:
1. Qual o problema?
2. Quem sao os usuarios?
3. O que NAO pode fazer?
4. Qual nivel SDD? (L1/L2/L3)
5. Quais sensors?

## Gatilhos para Modo Profundo

Use modo profundo quando detectar:
- Multiplas equipes envolvidas
- Dados sensiveis ou compliance (LGPD, SOC2)
- Integracoes complexas ou sistemas legados
- Codebase > 100K linhas
- Usuario responde com vagueza ou incerteza

---

*Discovery Skill — Harness Engineering v3.0*
