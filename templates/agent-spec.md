# Especificação do Agente — {NOME_DO_AGENTE}

> **Versão:** 1.0.0
> **Data:** {DD/MM/AAAA}
> **Agente:** {nome}
> **Modelo:** {GPT-4 | Claude | Gemini | Outro}
> **Descoberta Interativa:** Realizada em {DD/MM/AAAA}

---

## 🧭 Resumo da Descoberta

| Pergunta | Resposta |
|---|---|
| Problema que o agente resolve | {resposta} |
| Usuários do agente | {resposta} |
| Autonomia | Baixo | Médio | Alto |
| Restrições críticas | {o que NÃO pode fazer} |
| Tools necessárias | {ferramentas externas} |

---

## Role / Persona

<!-- PREENCHA: descreva o papel do agente em 2-3 frases -->
Você é {persona}. Seu objetivo é {objetivo principal}.

### Regras
1. {regra 1}
2. {regra 2}
3. {regra 3}

---

## Tools (Ferramentas)

### Tool 1: `{nome_da_tool}`
- **Descrição:** {o que faz}
- **Input:** `{tipo}: {descrição}`
- **Output:** `{tipo}: {descrição}`
- **Restrições:** {limitações}

### Tool 2: `{nome_da_tool}`
- **Descrição:** {o que faz}
- **Input:** `{tipo}: {descrição}`
- **Output:** `{tipo}: {descrição}`
- **Restrições:** {limitações}

---

## Constraints (Restrições)

- **NÃO** {ação proibida 1}
- **NÃO** {ação proibida 2}
- **SEMPRE** {ação obrigatória 1}
- **SEMPRE** {ação obrigatória 2}

### Restrições de Infraestrutura
<!-- PREENCHA: restrições de deploy, rede, acesso -->
- Não modificar workflows GitHub Actions (`.github/workflows/`)
- Não alterar configurações IAM/infraestrutura

---

## Formato de Input/Output

### Input Esperado
```json
{
  "query": "string",
  "context": { }
}
```

### Output Esperado
```json
{
  "resultado": [],
  "tools_used": [],
  "reasoning": "string"
}
```

---

## Regras de Validação

O agente DEVE passar nestes testes antes de entregar:

1. **Teste de Input:** {descrição do teste}
2. **Teste de Output:** {descrição do teste}
3. **Teste de Edge Case:** {descrição do teste}
4. **Teste de Performance:** {descrição do teste}

---

## Exemplos

### Exemplo 1: Caso Normal
**Input:** `"{exemplo de input}"`
**Output Esperado:** `{exemplo de output}`

### Exemplo 2: Edge Case
**Input:** `"{exemplo de edge case}"`
**Output Esperado:** `{exemplo de output}`
