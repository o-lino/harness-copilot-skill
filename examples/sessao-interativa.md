# Exemplo de Sessão Interativa Completa

> Este exemplo demonstra como o agente conduz o protocolo de descoberta interativa
> do início ao fim, gerando uma spec precisa baseada em respostas reais.

---

## 🎬 Início da Sessão

**Usuário:** "Preciso criar um sistema de gestão de estoque para minha loja."

**Agente:** 🧭 *Entendi. Antes de gerar qualquer spec ou código, preciso entender profundamente seu contexto. Vou fazer algumas perguntas — quanto mais detalhadas as respostas, mais precisa será a solução.*

---

### FASE 1: Domínio e Contexto

**Agente — Pergunta 1:** *Qual problema de negócio você está resolvendo? Não me diga a solução técnica, me diga o problema real.*

**Usuário:** "Perdemos vendas porque às vezes o produto aparece como disponível no site mas não tem no estoque físico. Já perdemos uns 15 pedidos esse mês por isso."

**Agente:** *Ótimo, isso é concreto. Deixa eu aprofundar:*

**🔍 "Por quê?" em cascata:**
- *Por que o site mostra como disponível se não tem?*
- *O sistema do site não conversa com o sistema do estoque físico?*

**Usuário:** "Exato. O site é Shopify e o controle de estoque é numa planilha Excel que o gerente atualiza no fim do dia. Tem um gap de até 12 horas."

---

**Agente — Pergunta 2:** *Quem são os usuários finais?*

**Usuário:** "O gerente da loja (1 pessoa) que atualiza o estoque, e os clientes do site (indiretamente, porque vão parar de comprar se o produto estiver errado)."

**Agente:** *E quem vai manter o sistema depois de pronto? Tem equipe técnica?*

**Usuário:** "Não, só eu. Sou desenvolvedor full-stack mas trabalho sozinho."

---

**Agente — Pergunta 3:** *O que já existe?*

**Usuário:** "Shopify rodando, planilha Excel com 500 SKUs, e eu tenho uma conta AWS que uso pra hosting."

---

**Agente — Pergunta 4:** *O que define SUCESSO?*

**Usuário:** "Zero vendas de produtos sem estoque. E o gerente não pode gastar mais de 5 minutos por dia atualizando."

---

### FASE 2: Escala e Complexidade

**Agente — Pergunta 5:** *Qual o tamanho estimado do projeto?*

**Usuário:** "Solo dev, então quero algo simples. Provavelmente menos de 10K linhas."

**Agente:** *Ok, isso indica harness simples — AGENTS.md + contexto bom é suficiente.*

---

**Agente — Pergunta 6:** *Quantas pessoas trabalham nisso?*

**Usuário:** "Só eu, como disse."

---

**Agente — Pergunta 7:** *Qual nível SDD você quer?*

- **L1:** Você escreve a spec, eu gero o código, mas você pode ajustar depois
- **L2:** A spec é gate — não gero código sem spec aprovada
- **L3:** A spec é tudo — código 100% gerado, você só mantém a spec

**Usuário:** "L2. Quero garantir que a spec esteja certa antes de gerar código. Não quero surpresas."

---

### FASE 3: Restrições e Requisitos

**Agente — Pergunta 8:** *O que o sistema NÃO PODE fazer?*

**Usuário:** "Não pode substituir o Shopify — tem que integrar com ele. Não pode exigir que o gerente aprenda um sistema novo complicado. E não pode custar mais que $50/mês em infra."

---

**Agente — Pergunta 9:** *Quais são as dependências externas?*

**Usuário:** "Shopify API (Admin API), e a planilha Excel que o gerente já usa — no ideal, quero importar dela."

---

**Agente — Pergunta 10:** *Tem compliance ou regulamentação?*

**Usuário:** "Nada específico. LGPD talvez, mas não guardamos dados sensíveis — só SKU e quantidade."

---

### FASE 4: Design do Harness

**Agente — Pergunta 11:** *Quais sensors de validação são essenciais?*

- [x] **Maintainability** — ESLint + Prettier
- [x] **Computational** — TypeScript strict
- [x] **Behaviour** — Jest, testes de integração com Shopify
- [ ] **Architecture Fitness** — Não preciso, é projeto pequeno
- [ ] **Data Quality** — Talvez no futuro
- [ ] **Security** — Sim, verificar que não exponho API keys

---

**Agente — Pergunta 12:** *Qual padrão multi-agente?*

**Usuário:** "Nenhum. É projeto solo, agente único."

---

**Agente — Pergunta 13:** *Qual nível de autonomia do agente?*

- **Baixo:** Eu sugiro, você aprova cada passo
- **Médio:** Eu executo, você revisa ao final
- **Alto:** Eu executo e deployo, você é notificado de problemas

**Usuário:** "Médio. Gere o código, eu reviso no final."

---

## 📋 Síntese e Confirmação

**Agente:**

> *Com base nas suas respostas, projetei o seguinte:*
>
> ### Resumo de Descoberta
>
> **Domínio**
> - Problema: Gap de até 12h entre estoque físico e site causa ~15 vendas perdidas/mês
> - Usuários: 1 gerente (atualiza estoque), clientes do site (indiretos)
> - Estado atual: Shopify + planilha Excel com 500 SKUs, AWS hosting
> - Sucesso = Zero vendas sem estoque + gerente gasta ≤5min/dia
>
> **Escala**
> - Codebase: < 10K linhas (projeto solo)
> - Equipe: 1 pessoa (você)
> - SDD Level: L2 (Spec-Anchored — spec é gate)
>
> **Restrições**
> - NÃO PODE: Substituir Shopify, complicar UX do gerente, custar > $50/mês
> - Dependências: Shopify Admin API, importação de planilha Excel
> - Compliance: LGPD leve (só SKU + quantidade)
>
> **Harness**
> - Sensors: ESLint + Prettier, TypeScript strict, Jest, Security (API keys)
> - Multi-Agent: Nenhum (agente único)
> - Autonomia: Média (executo, você revisa)
>
> *Está correto? Quer ajustar algo antes de eu gerar a spec?*

**Usuário:** "Perfeito. Pode gerar."

---

## 📝 Geração da Spec

*(O agente agora gera requirements.md, design.md e tasks.md com base nas respostas precisas)*

### requirements.md (gerado)
```markdown
## User Stories
- Como gerente, quero atualizar o estoque em ≤5 minutos para que o site reflita a realidade.
- Como cliente, quero ver disponibilidade real para não tentar comprar produto indisponível.

## Requisitos
### RF-001: Sincronizar Estoque
- Quando o gerente subir a planilha Excel atualizada,
- O sistema SHALL processar os 500 SKUs em menos de 30 segundos,
- O sistema SHALL atualizar o estoque no Shopify via Admin API,
- O sistema SHALL retornar relatório de sucesso/falha por SKU.

### RF-002: Webhook de Baixo Estoque
- Quando o estoque de um SKU cair abaixo de 5 unidades,
- O sistema SHALL notificar o gerente por email.

## Restrições
- Custo de infra ≤ $50/mês
- Não modificar o Shopify, apenas integrar via API
- Não expor API keys no código
```

### design.md (gerado)
```markdown
- Arquitetura: Serverless na AWS (Lambda + S3 + EventBridge)
- Fluxo: Gerente sobe Excel no S3 → Lambda processa → Shopify API atualiza
- Custo estimado: ~$5/mês (Lambda + S3 + EventBridge)
- Segurança: API keys no AWS Secrets Manager
```

---

## ✅ Resultado

O usuário obteve:
1. **Uma spec precisa** baseada no problema real (15 vendas perdidas/mês)
2. **Restrições claras** (não substituir Shopify, ≤$50/mês, ≤5min do gerente)
3. **Sensors definidos** (lint, type check, tests, security)
4. **Arquitetura adequada** (serverless barato, integração com Shopify)

**Tudo isso sem escrever uma linha de código.** A spec é o ponto de partida. O código será gerado a partir dela e validado pelos sensors.

---

## Lições Desta Sessão

- **Técnica que funcionou:** "Por quê?" em cascata revelou a causa raiz (gap de 12h entre sistemas)
- **Informação crítica descoberta:** O gerente já tem um workflow (planilha Excel) — o sistema precisa se adaptar a ele, não o contrário
- **Restrição importante:** Custo ≤ $50/mês → levou à decisão de serverless em vez de servidor dedicado
- **Se tivesse pulado a descoberta:** Teria gerado um sistema genérico de estoque que não integrava com Shopify, não importava Excel, e custaria $200/mês
