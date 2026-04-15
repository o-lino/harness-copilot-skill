# Tasks de Implementação — {NOME_DA_FEATURE}

> **Spec:** `specs/{feature}/tasks.md`  
> **Data:** {DD/MM/AAAA}  
> **SDD Level:** L1 | L2 | L3

---

## Tasks

<!-- GUIA: Cada task deve:
- Corresponder a NO MÍNIMO 1 requisito da requirements.md (traceabilidade)
- Ser pequena o suficiente para ser validada por sensors em < 30min
- Ter critérios de done verificáveis mecanicamente (não subjetivos)
- Ter NO MÁXIMO 2 dependências diretas (se mais, divida a task) -->

### T-001: {Nome da Task}
- **Descrição:** {o que precisa ser feito}
- **Requisito relacionado:** RF-XXX | RNF-XXX
- **Depende de:** Nenhuma | T-XXX
- **Pode ser paralelizada com:** T-XXX
- **Estimativa:** {XS | S | M | L | XL}

**Critérios de Done:**
- [ ] Código implementado
- [ ] Tests escritos e passando
- [ ] Lint limpo
- [ ] Type-check limpo
- [ ] Documentação atualizada

**Comando de Verificação:**
```bash
# PREENCHA: comando para validar esta task
npm run test -- {arquivo}
```

---

### T-002: {Nome da Task}
- **Descrição:** {o que precisa ser feito}
- **Depende de:** T-001
- **Pode ser paralelizada com:** T-XXX

**Critérios de Done:**
- [ ] Código implementado
- [ ] Tests escritos e passando
- [ ] Lint limpo
- [ ] Type-check limpo
- [ ] Documentação atualizada

**Comando de Verificação:**
```bash
# PREENCHA
```

---

### T-003: {Nome da Task}
- **Descrição:** {o que precisa ser feito}
- **Depende de:** T-001, T-002
- **Pode ser paralelizada com:** Nenhuma

**Critérios de Done:**
- [ ] Código implementado
- [ ] Tests escritos e passando
- [ ] Lint limpo
- [ ] Type-check limpo
- [ ] Documentação atualizada

**Comando de Verificação:**
```bash
# PREENCHA
```

---

## Order de Execução

```
T-001 (independente)
  ├── T-002 (depende de T-001)
  │     └── T-003 (depende de T-002)
  └── T-XXX (paralela com T-002)
```

---

## Notas de Paralelização

<!-- PREENCHA: quais tasks podem rodar simultaneamente e quais devem ser sequenciais -->
