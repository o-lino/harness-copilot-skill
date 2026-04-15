# Sessão de Descoberta — {NOME_DO_PROJETO}

> **Data:** {DD/MM/AAAA}
> **Facilitador:** {nome do agente}
> **Participante:** {nome do usuário}
> **Modo:** Rápido (5 perguntas) | Profundo (13+ perguntas)
> **Duração:** {X minutos}
> **Status:** Em andamento | Concluída | Confirmada

---

## 📋 Resumo Executivo

<!-- PREENCHA: 2-3 frases que resumem o projeto -->

| Campo | Valor |
|---|---|
| **Problema** | {qual problema de negócio está sendo resolvido} |
| **Sucesso =** | {métrica concreta que define sucesso} |
| **Nível SDD** | L1 | L2 | L3 |
| **Sensors** | {lista de sensors selecionados} |
| **Padrão** | {padrão multi-agente ou "agente único"} |
| **Autonomia** | Baixa | Média | Alta |

---

## FASE 1: Domínio e Contexto

### 1. Qual problema de negócio você está resolvendo?

**Resposta:**
> {resposta do usuário}

**Aprofundamento:**
| Técnica | Pergunta | Resposta |
|---|---|---|
| "Por quê?" | {pergunta} | {resposta} |
| "Por quê?" | {pergunta} | {resposta} |
| "Exemplo concreto" | {pergunta} | {resposta} |

---

### 2. Quem são os usuários finais?

**Resposta:**
> {resposta do usuário}

**Detalhes:**
| Papel | Quantidade | Frequência de uso | Nível técnico |
|---|---|---|---|
| {papel} | {número} | {diário/semanal/etc} | {baixo/médio/alto} |

---

### 3. O que já existe?

**Resposta:**
> {resposta do usuário}

**Inventário:**
| Componente | Tecnologia | Estado | Integrável? |
|---|---|---|---|
| {ex: Shopify} | {ex: SaaS} | {produção} | {sim via API} |

---

### 4. O que define SUCESSO?

**Resposta:**
> {resposta do usuário}

**Métricas:**
| Métrica | Valor atual | Target | Como medir |
|---|---|---|---|
| {ex: vendas perdidas/mês} | {15} | {0} | {relatório Shopify} |

---

### Perguntas Condicionais (FASE 1)

<!-- Preencha as que se aplicam ao domínio -->

**Se DATA:**
- Volume de dados? {MB/GB/TB/PB}
- Frequência de atualização? {tempo real/diário/semanal}
- Existem contratos de dados? {sim/não}

**Se API/WEB:**
- Quantos endpoints? {número estimado}
- Autenticação? {JWT/OAuth2/API Key}
- Integrações externas? {quais}

**Se INFRA/CI-CD:**
- Cloud provider? {AWS/GCP/Azure/on-premise}
- Pipeline atual? {o que faz}
- Tempo de deploy? {atual → target}

---

## FASE 2: Escala e Complexidade

### 5. Tamanho estimado da codebase?

**Resposta:**
> {resposta do usuário}

**Recomendação de Harness:**
| Tamanho | Abordagem | Aplicável? |
|---|---|---|
| < 100K linhas | AGENTS.md + contexto | {sim/não} |
| 100K – 1M linhas | Thin harness | {sim/não} |
| 1M – 10M linhas | Platform harness | {sim/não} |

---

### 6. Quantas pessoas/equipes?

**Resposta:**
> {resposta do usuário}

**Estrutura:**
| Equipe | Tamanho | Responsabilidade |
|---|---|---|
| {ex: Backend} | {número} | {o que fazem} |

---

### 7. Nível de maturidade SDD?

**Resposta:**
> {resposta do usuário}

**Justificativa:**
> {por que este nível foi escolhido}

---

### Perguntas Condicionais (FASE 2)

**Se multi-equipe:**
- Comunicação atual? {Slack/docs/reuniões}
- Code review? {processo}
- Conflitos de merge? {frequência}

**Se L3 (Spec-as-Source):**
- Confiança na IA? {sim/não/parcial}
- Quem valida a spec? {papel}
- Processo de rollback? {descrição}

---

## FASE 3: Restrições e Requisitos

### 8. O que o sistema NÃO PODE fazer?

**Resposta:**
> {resposta do usuário}

| Restrição | Tipo | Severidade |
|---|---|---|
| {ex: não modificar Shopify} | técnica | crítica |

---

### 9. Dependências externas?

**Resposta:**
> {resposta do usuário}

| Dependência | Tipo | SLA | Fallback |
|---|---|---|---|
| {ex: Shopify API} | REST | 99.9% | retry + cache |

---

### 10. Compliance/regulamentação?

**Resposta:**
> {resposta do usuário}

| Requisito | Tipo | Impacto |
|---|---|---|
| {ex: LGPD} | regulatório | anonimização de PII |

---

### Perguntas Condicionais (FASE 3)

**Se dados sensíveis:**
- Campos sensíveis? {quais}
- Tratamento? {criptografia/mask/hash}
- Acesso? {quem}

**Se integrações externas:**
- SLA do serviço? {número}
- Indisponibilidade? {o que acontece}
- Fallback? {existe?}

**Se requisitos de performance:**
- Tempo de resposta? {ms/s}
- Throughput? {req/s}
- Pico previsto? {número}

---

## FASE 4: Design do Harness

### 11. Sensors essenciais?

**Selecionados:**
- [ ] Maintainability — {ferramenta}
- [ ] Computational — {ferramenta}
- [ ] Behaviour — {ferramenta}
- [ ] Architecture Fitness — {ferramenta}
- [ ] Data Quality — {ferramenta}
- [ ] Security — {ferramenta}

---

### 12. Padrão multi-agente?

**Resposta:**
> {resposta do usuário}

**Justificativa:**
> {por que este padrão foi escolhido}

---

### 13. Nível de autonomia?

**Resposta:**
> {resposta do usuário}

**Implicações:**
| Nível | O que o agente faz | O que o humano faz |
|---|---|---|
| {Baixo/Médio/Alto} | {ações} | {ações} |

---

### Perguntas Condicionais (FASE 4)

**Se Data Quality:**
- Regras críticas? {quais}
- Threshold abaixo? {o que acontece}
- Quarantine? {existe?}

**Se Security:**
- Vulnerabilidades preocupantes? {quais}
- Scan automatizado? {sim/não}
- SLA correção crítica? {horas/dias}

---

## ✅ Síntese e Confirmação

### Resumo Apresentado ao Usuário

```markdown
**Domínio**
- Problema: {resumo}
- Usuários: {resumo}
- Estado atual: {resumo}
- Sucesso = {métrica}

**Escala**
- Codebase: {tamanho}
- Equipe: {número}
- SDD Level: L{1|2|3}

**Restrições**
- NÃO PODE: {lista}
- Dependências: {lista}
- Compliance: {lista}

**Harness**
- Sensors: {lista}
- Multi-Agent: {padrão}
- Autonomia: {nível}
```

### Confirmação

- [ ] Usuário confirmou o resumo
- [ ] Ajustes solicitados: {lista ou "nenhum"}
- [ ] Ajustes incorporados: {lista ou "nenhum"}

---

## 📝 Próximos Passos

Após confirmação desta sessão:

1. [ ] Gerar `requirements.md` (EARS)
2. [ ] Gerar `design.md` (arquitetura)
3. [ ] Gerar `tasks.md` (implementação)
4. [ ] Configurar sensors no CI/CD
5. [ ] Iniciar implementação

---

## 📎 Notas Adicionais

<!-- Observações, insights, ou informações que surgiram durante a sessão -->

{notas}
