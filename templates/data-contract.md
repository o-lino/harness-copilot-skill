# Contrato de Dados — {NOME_DO_CONTRATO}

> **Versão:** 1.0.0
> **Data:** {DD/MM/AAAA}
> **Owner:** {nome ou equipe}
> **Status:** Rascunho | Aprovado | Depreciado
> **Descoberta Interativa:** Realizada em {DD/MM/AAAA}

---

## 🧭 Resumo da Descoberta

| Pergunta | Resposta |
|---|---|
| Volume de dados | {MB/GB/TB/PB} |
| Frequência de atualização | {tempo real/diário/semanal} |
| Dados sensíveis? | {sim/não — quais campos} |
| SLA existente | {métrica atual} |
| Problemas de qualidade | {quais problemas existem hoje} |

---

## Schema

### Tabela: `{database}.{tabela}`

| Coluna | Tipo | Nullable | Descrição | Exemplo |
|---|---|---|---|---|
| id | UUID | Não | Identificador único | `a1b2c3d4-...` |
| {coluna} | {tipo} | {sim/não} | {descrição} | {exemplo} |

---

## Regras de Qualidade

| Regra | Coluna | Condição | Ação se Violada |
|---|---|---|---|
| RQ-001 | email | Formato email válido | Quarantine + alerta |
| RQ-002 | {coluna} | {condição} | {ação} |

### Níveis de Qualidade

| Nível | Descrição | Critério |
|---|---|---|
| **A** | Golden Source | Qualidade aferida > 99%, update diário |
| **B** | Confiável | Qualidade > 95%, update semanal |
| **C** | Provisório | Qualidade < 95%, uso com cautela |

---

## SLA / SLO

| Métrica | Target | Alerta |
|---|---|---|
| Freshness (atraso máximo) | {ex: 24h} | {ex: 48h} |
| Volume (variação aceitável) | {ex: ±10%} | {ex: ±25%} |
| Disponibilidade | {ex: 99.9%} | {ex: 99%} |

---

## Classificação

| Campo | Valor |
|---|---|
| Golden Source | Sim / Não |
| SOR (System of Record) | Sim / Não |
| Domínio | {ex: vendas, risco, marketing} |
| Sensibilidade | Público | Interno | Confidencial | Restrito |

---

## Change Management

| Campo | Valor |
|---|---|
| Owner do Dado | {nome/equipe} |
| Channel de Comunicação | {slack, email} |
| Lead Time para Mudança | {ex: 2 semanas} |
| Breaking Changes | Devem ser comunicados com {X} dias de antecedência |

### Histórico de Versões

| Versão | Data | Autor | Mudança |
|---|---|---|---|
| 1.0.0 | {data} | {autor} | Versão inicial |
