---
trigger: always_on
alwaysApply: true
---

# Protocolo de Descoberta Interativa — Harness Engineering

> **Propósito:** Antes de gerar QUALQUER spec, template ou código, conduza uma sessão de descoberta interativa para desambiguar profundamente o domínio, contexto, restrições e necessidades do projeto.
>
> **Regra de Ouro:** NUNCA gere spec ou código sem antes passar por este protocolo de perguntas. Perguntas profundas geram specs precisas. Specs precisas geram código correto.

---

## Fluxo do Protocolo

O protocolo segue **4 fases sequenciais**. Cada fase tem perguntas obrigatórias e perguntas condicionais (que dependem das respostas anteriores).

```
FASE 1: Domínio e Contexto
    ↓ (respostas coletadas)
FASE 2: Escala e Complexidade
    ↓ (respostas coletadas)
FASE 3: Restrições e Requisitos
    ↓ (respostas coletadas)
FASE 4: Design do Harness
    ↓ (respostas coletadas)
SÍNTESE + CONFIRMAÇÃO
    ↓ (usuário aprova)
GERAÇÃO DA SPEC
```

---

## FASE 1: Domínio e Contexto

### Perguntas Obrigatórias

**1. Qual problema de negócio você está resolvendo?**
> Não me diga a solução técnica. Me diga o problema.
> Exemplo ruim: "Preciso de uma API REST."
> Exemplo bom: "Meus vendedores demoram 3 horas para encontrar a tabela certa no datalake. Preciso que encontrem em 30 segundos."

**2. Quem são os usuários finais deste sistema?**
> Quem vai interagir? Quem vai consumir os dados? Quem vai manter?
> Ex: "3 analistas de dados, 15 vendedores, o sistema de BI automático."

**3. Qual é o estado atual? O que já existe?**
> Código legado? Banco de dados? APIs? Documentação?
> Ex: "Temos 60k tabelas no Iceberg, um SDK proprietário de LLM, GitHub Actions."

**4. O que define SUCESSO para este projeto?**
> Métrica concreta. Algo mensurável.
> Ex: "Reduzir tempo de descoberta de tabelas de 3h para 30s com 95% de precisão."

### Perguntas Condicionais

**Se o domínio é DATA:**
- Qual o volume de dados? (MB, GB, TB, PB?)
- Qual a frequência de atualização? (tempo real, diário, semanal?)
- Existem contratos de dados definidos? SLAs de qualidade?

**Se o domínio é API/WEB:**
- Quantos endpoints esperados?
- Existe autenticação/autorização? Qual?
- Há integração com sistemas externos?

**Se o domínio é INFRA/CI-CD:**
- Qual a cloud provider? (AWS, GCP, Azure, on-premise?)
- Existe pipeline atual? O que faz? O que falta?
- Qual o tempo de deploy atual? Qual o target?

---

## FASE 2: Escala e Complexidade

### Perguntas Obrigatórias

**5. Qual o tamanho estimado da codebase?**
> - < 100K linhas → Harness simples (AGENTS.md + contexto)
> - 100K – 1M linhas → Thin harness (task routing + context scoping)
> - 1M – 10M linhas → Platform harness (serviços dedicados)
> - 10M+ linhas → Agent platform custom

**6. Quantas pessoas/equipes vão trabalhar neste projeto?**
> - Solo → Harness mínimo
> - 2-5 → Harness com sensors CI/CD
> - 5-20 → Harness com multi-agent
> - 20+ → Harness enterprise com governança

**7. Qual o nível de maturidade SDD desejado?**
> - **L1 (Spec-First):** Escrevo spec antes do código, mas posso divergir
> - **L2 (Spec-Anchored):** Spec é gate obrigatório — não toca código sem spec aprovada
> - **L3 (Spec-as-Source):** Spec é o ÚNICO artefato — código 100% gerado

### Perguntas Condicionais

**Se multi-equipe:**
- Como as equipes se comunicam hoje? (Slack, docs, reuniões?)
- Existe um padrão de code review?
- Há conflitos frequentes de merge?

**Se L3 (Spec-as-Source):**
- Você confia na IA para gerar 100% do código?
- Quem valida a spec antes da geração?
- Qual o processo de rollback se o código gerado estiver errado?

---

## FASE 3: Restrições e Requisitos

### Perguntas Obrigatórias

**8. O que o sistema NÃO PODE fazer?**
> Restrições são tão importantes quanto requisitos.
> Ex: "Não pode modificar GitHub Actions. Não pode usar boto3 direto. Não pode expor dados PII."

**9. Quais são as dependências externas?**
> APIs de terceiros? Bancos legados? Serviços internos?
> Ex: "SDK proprietário de LLM, AWS Athena, GitHub Actions imutável."

**10. Existe compliance/regulamentação aplicável?**
> LGPD? SOC2? HIPAA? PCI-DSS? Requisitos internos?
> Ex: "LGPD — dados pessoais devem ser anonimizados. Política interna de retenção de 90 dias."

### Perguntas Condicionais

**Se há dados sensíveis:**
- Quais campos são sensíveis?
- Como devem ser tratados? (criptografia, mask, hash?)
- Quem tem acesso?

**Se há integrações externas:**
- Qual o SLA do serviço externo?
- O que acontece se ficar indisponível?
- Existe fallback?

**Se há requisitos de performance:**
- Qual o tempo de resposta aceitável?
- Qual o throughput esperado? (req/s, queries/min?)
- Qual o pico previsto?

---

## FASE 4: Design do Harness

### Perguntas Obrigatórias

**11. Quais sensors de validação são essenciais para este projeto?**
> Marque todos que se aplicam:
> - [ ] **Maintainability** — Lint, formatação, estilo (ESLint, Prettier, ruff)
> - [ ] **Computational** — Type check, compilação (tsc, mypy, pyright)
> - [ ] **Behaviour** — Tests funcionais (Jest, pytest, Playwright)
> - [ ] **Architecture Fitness** — Conformidade arquitetural (ArchUnit, dependency-cruiser)
> - [ ] **Data Quality** — Validação de dados (Great Expectations, custom)
> - [ ] **Security** — Vulnerabilidades, secrets (SAST, DAST, git-secrets)

**12. Qual padrão multi-agente se aplica?**
> - **Sequential:** Tarefas com dependência linear
> - **Fan-Out:** Paralelização de sub-tarefas independentes
> - **Orchestrator-Worker:** Tarefas complexas com divisão dinâmica
> - **Hierarchical:** Multi-camadas de gestão
> - **Nenhum:** Projeto simples, agente único

**13. Qual o nível de autonomia do agente?**
> - **Baixo:** Agente sugere, humano aprova cada passo
> - **Médio:** Agente executa, humano revisa ao final
> - **Alto:** Agente executa e deploya, humano é notificado de problemas

### Perguntas Condicionais

**Se Data Quality foi marcado:**
- Quais regras de qualidade são críticas?
- O que acontece se a qualidade estiver abaixo do threshold?
- Existe processo de quarantine para dados ruins?

**Se Security foi marcado:**
- Quais tipos de vulnerabilidade são mais preocupantes?
- Existe processo de scan automatizado?
- Qual o SLA para correção de vulnerabilidades críticas?

---

## Após as Perguntas: Síntese e Confirmação

Depois de coletar todas as respostas, você DEVE:

### 1. Gerar um Resumo de Descoberta

```markdown
## Resumo de Descoberta

### Domínio
- Problema: {resposta da pergunta 1}
- Usuários: {resposta da pergunta 2}
- Estado atual: {resposta da pergunta 3}
- Sucesso = {resposta da pergunta 4}

### Escala
- Codebase: {resposta da pergunta 5}
- Equipe: {resposta da pergunta 6}
- SDD Level: {resposta da pergunta 7}

### Restrições
- NÃO PODE: {resposta da pergunta 8}
- Dependências: {resposta da pergunta 9}
- Compliance: {resposta da pergunta 10}

### Harness
- Sensors: {resposta da pergunta 11}
- Multi-Agent: {resposta da pergunta 12}
- Autonomia: {resposta da pergunta 13}
```

### 2. Pedir Confirmação

> "Com base nas suas respostas, projetei o seguinte harness. Confira se está correto antes de eu gerar a spec:
>
> - **Nível SDD:** L{1|2|3}
> - **Sensors:** {lista}
> - **Padrão:** {padrão multi-agente}
> - **Restrições críticas:** {lista}
>
> Está correto? Posso ajustar algo antes de gerar?"

### 3. Gerar a Spec

Só após confirmação, gerar:
- `specs/{feature}/requirements.md` (EARS)
- `specs/{feature}/design.md` (arquitetura)
- `specs/{feature}/tasks.md` (implementação)

---

## Modo Rápido vs. Modo Profundo

### Modo Rápido (5 perguntas)
Para projetos simples ou quando o usuário já tem clareza:

1. Qual o problema?
2. Quem são os usuários?
3. O que NÃO pode fazer?
4. Qual nível SDD? (L1/L2/L3)
5. Quais sensors?

### Modo Profundo (13+ perguntas)
Para projetos complexos, enterprise, ou quando o usuário não tem clareza:

→ Seguir o protocolo completo (Fases 1-4)

Você deve sugerir o modo profundo quando detectar:
- Múltiplas equipes envolvidas
- Dados sensíveis ou compliance
- Integrações complexas
- Codebase > 100K linhas
- Usuário responde com vagueza

---

## Técnicas de Aprofundamento

### 1. "Por quê?" em Cascata
Quando o usuário dá uma resposta vaga, pergunte "por quê?" até chegar na raiz.

> Usuário: "Preciso de uma API."
> Você: "Por quê? O que essa API vai habilitar?"
> Usuário: "Para o app mobile acessar dados."
> Você: "Por que o app precisa desses dados? O que o usuário faz com eles?"
> Usuário: "Consulta o status do pedido."
> Você: "Entendi. Então o problema é: usuários não conseguem acompanhar pedidos no mobile. Correto?"

### 2. Cenário "E se..."
Teste limites do sistema com cenários hipotéticos.

> "E se o serviço de pagamento ficar indisponível por 1 hora?"
> "E se o volume de dados triplicar amanhã?"
> "E se a equipe dobrar de tamanho em 3 meses?"

### 3. Trade-off Explícito
Force o usuário a escolher entre opções conflitantes.

> "Você prefere: velocidade de entrega ou qualidade do código? Ambos não são possíveis simultaneamente neste prazo."
> "Para este caso: consistência forte ou disponibilidade alta?"

### 4. Exemplo Concreto
Peça um exemplo real para entender o padrão.

> "Me dê um exemplo concreto de um pedido que falharia no sistema atual."
> "Me mostre uma query que seus analistas fazem manualmente hoje."

### 5. Anti-Exemplo
Peça o que NÃO é para entender os limites.

> "O que este sistema definitivamente NÃO deve fazer?"
> "Qual seria o pior resultado possível?"

---

## Bancos de Perguntas por Domínio

> Use estas perguntas adicionais após o protocolo base (13 perguntas) para aprofundar no domínio específico.

### Data Engineering / Data Lakes

| # | Pergunta | Por que perguntar |
|---|---|---|
| D1 | Qual o volume total de dados? (MB, GB, TB, PB?) | Define arquitetura de processamento |
| D2 | Quantos ativos de dados? (tabelas, views, streams?) | Define complexidade de descoberta/gestão |
| D3 | Qual a frequência de ingestão? (streaming, batch diário, semanal?) | Define pipeline architecture |
| D4 | Existem dados PII ou sensíveis? Quais campos? | Define compliance e segurança |
| D5 | Qual o formato dos dados? (Parquet, CSV, JSON, Iceberg?) | Define compatibilidade de tools |
| D6 | Existem Golden Sources definidos? Quem os nomeia? | Define governança de dados |
| D7 | Qual a qualidade atual dos dados? (tem métricas?) | Define necessidade de data quality sensors |
| D8 | Existe schema drift? Com que frequência? | Define necessidade de auto-healing |
| D9 | Quem são os Data Owners? Como são contactados? | Define processo de governança |
| D10 | Qual o SLA de freshness? (dados atualizados em quanto tempo?) | Define métrica de sucesso |
| D11 | Existem contratos de dados entre equipes? | Define acoplamento organizacional |
| D12 | O que acontece se um pipeline falhar? Qual o impacto? | Define criticalidade e retry strategy |

### API / Web Applications

| # | Pergunta | Por que perguntar |
|---|---|---|
| W1 | Quantos endpoints esperados? | Define escopo da API |
| W2 | Qual o padrão de autenticação? (JWT, OAuth2, API Key, session?) | Define security design |
| W3 | Existe rate limiting? Qual o threshold? | Define infra requirements |
| W4 | Qual o tempo de resposta aceitável? (p95, p99?) | Define performance targets |
| W5 | Existe paginação? Filtros? Ordenação? | Define complexidade de queries |
| W6 | A API é pública ou interna? | Define security posture |
| W7 | Existe versionamento de API? Qual estratégia? | Define backward compatibility |
| W8 | Há integração com sistemas externos? Quais? | Define dependências críticas |
| W9 | Qual o throughput esperado? (req/s, req/min?) | Define scaling requirements |
| W10 | Existe cache? Qual estratégia? (CDN, Redis, in-memory?) | Define performance optimization |
| W11 | Há webhooks ou eventos em tempo real? | Define architecture pattern |
| W12 | Qual o plano de rollback se um deploy falhar? | Define deploy strategy |

### Infrastructure / CI-CD

| # | Pergunta | Por que perguntar |
|---|---|---|
| I1 | Qual cloud provider? (AWS, GCP, Azure, on-premise?) | Define tooling e IaC |
| I2 | Existe IaC atual? (Terraform, CloudFormation, Pulumi?) | Define baseline de infra |
| I3 | Qual o pipeline de CI/CD atual? O que faz? | Define ponto de partida |
| I4 | Qual o tempo de build atual? Qual o target? | Define optimization priority |
| I5 | Existe ambiente de staging? QA? Produção? | Define deployment strategy |
| I6 | Há blue-green ou canary deployment? | Define release strategy |
| I7 | Existe monitoring? (Datadog, New Relic, CloudWatch?) | Define observability |
| I8 | Há alerting configurado? Quais métricas? | Define incident response |
| I9 | Qual o RTO (Recovery Time Objective)? | Define disaster recovery |
| I10 | Qual o RPO (Recovery Point Objective)? | Define backup strategy |
| I11 | Existe compliance de infra? (SOC2, HIPAA, PCI?) | Define security controls |
| I12 | Quem aprova deploys em produção? | Define governance |

### Mobile Applications

| # | Pergunta | Por que perguntar |
|---|---|---|
| M1 | Qual plataforma? (iOS, Android, cross-platform?) | Define tech stack |
| M2 | Qual framework? (React Native, Flutter, native?) | Define development approach |
| M3 | A app funciona offline? Quais features? | Define data sync strategy |
| M4 | Existe push notification? Qual provider? | Define integration requirements |
| M5 | Qual a frequência de release? (semanal, quinzenal, mensal?) | Define CI/CD cadence |
| M6 | Existe app review da store? Quanto tempo leva? | Define release planning |
| M7 | Há A/B testing? Qual ferramenta? | Define experimentation |
| M8 | Qual o mínimo OS version suportado? | Define compatibility scope |
| M9 | Existe deep linking? Universal links? | Define navigation architecture |
| M10 | Há analytics? Qual ferramenta? | Define tracking requirements |

### AI / Machine Learning

| # | Pergunta | Por que perguntar |
|---|---|---|
| A1 | Qual o tipo de modelo? (LLM, classificação, regressão, visão?) | Define ML approach |
| A2 | Existe dataset de treino? Qual tamanho? | Define data requirements |
| A3 | Qual a métrica de avaliação? (accuracy, F1, BLEU, ROUGE?) | Define success criteria |
| A4 | O modelo roda em tempo real ou batch? | Define inference architecture |
| A5 | Existe drift de dados? Como é monitorado? | Define model monitoring |
| A6 | Qual a frequência de retreinamento? | Define MLOps pipeline |
| A7 | Há A/B testing de modelos? | Define deployment strategy |
| A8 | Existe viés a ser mitigado? | Define fairness requirements |
| A9 | O modelo precisa de explainability? | Define model complexity trade-off |
| A10 | Qual o custo de inferência por request? | Define cost optimization |

### Security / Compliance

| # | Pergunta | Por que perguntar |
|---|---|---|
| S1 | Quais frameworks de compliance aplicáveis? (LGPD, SOC2, HIPAA, PCI?) | Define controles necessários |
| S2 | Existem dados PII? Como são tratados? | Define encryption/masking |
| S3 | Qual a política de retenção de dados? | Define lifecycle management |
| S4 | Existe processo de penetration testing? Frequência? | Define security validation |
| S5 | Há gestão de secrets? Qual ferramenta? | Define credential management |
| S6 | Existe SAST/DAST no pipeline? | Define security sensors |
| S7 | Qual o processo de resposta a incidentes? | Define incident readiness |
| S8 | Há audit logging? O que é logado? | Define compliance tracking |
| S9 | Existe gestão de vulnerabilidades? SLA de correção? | Define patch management |
| S10 | Há controle de acesso por role? (RBAC, ABAC?) | Define authorization model |

---

*Protocolo de Descoberta Interativa — Parte da Harness Engineering Skill v2.0*
