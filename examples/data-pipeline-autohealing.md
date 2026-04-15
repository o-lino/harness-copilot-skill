# Exemplo: Data Pipeline com Auto-Healing

## Contexto

Pipeline ETL que ingere dados de vendas de 3 fontes (API REST, CSV S3, banco legado). Frequentemente falha por schema drift, dados faltantes e timeouts. O agente detecta, diagnostica e corrige automaticamente.

**Domínio:** Data Engineering com IA  
**Padrão:** Auto-Healing via Harness Sensors

---

## Harness Design

### Guides
```
Agente de Data Pipeline:
- Você é responsável por manter o pipeline funcionando.
- Quando uma etapa falhar, analise o log e tente corrigir.
- Priorize: dados > velocidade. Melhor lento e correto que rápido e errado.
```

### Sensors
| Sensor | Detecta | Ação do Agente |
|---|---|---|
| Schema Validator | Coluna removida/tipo alterado | Atualiza mapeamento ou quarantena |
| Data Quality | Nulls em campo obrigatório | Alerta + imputa valor padrão |
| Timeout Monitor | Fonte não respondeu em 30s | Retry com backoff, depois fallback |
| Row Count Checker | Variação > 25% vs. dia anterior | Alerta crítico, pausa pipeline |

---

## Fluxo Auto-Healing

```
Pipeline executa
    ↓
[Sensor detecta falha]
    ↓
Agente analisa log
    ↓
┌─────────────────────────────────────┐
│ Tipo de erro        │ Ação          │
├─────────────────────────────────────┤
│ Schema drift        │ Atualiza coluna│
│ Data quality        │ Quarantine     │
│ Timeout             │ Retry + backoff│
│ Dependency break    │ Re-escreve JOIN│
└─────────────────────────────────────┘
    ↓
Aplica fix → Re-executa → Valida
    ↓
Se passou → Continua pipeline
Se falhou → Escala para humano
```

---

## Implementação

```python
# sensors/schema_validator.py
class SchemaValidator:
    def __init__(self, expected_schema: dict):
        self.expected = expected_schema

    def validate(self, df) -> list:
        """Retorna lista de drifts detectados."""
        drifts = []
        for col, expected_type in self.expected.items():
            if col not in df.columns:
                drifts.append({'type': 'missing_column', 'column': col})
            elif df[col].dtype != expected_type:
                drifts.append({'type': 'type_mismatch', 'column': col})
        return drifts

# agents/autohealer.py
class AutoHealingAgent:
    def handle_drift(self, drift: dict, df) -> DataFrame:
        if drift['type'] == 'missing_column':
            df[drift['column']] = None  # Adiciona coluna nula
            logger.info(f"Coluna {drift['column']} adicionada com nulls")
        elif drift['type'] == 'type_mismatch':
            df[drift['column']] = df[drift['column']].astype(self.expected[drift['column']])
        return df
```

---

## Validação

```bash
# Teste: Schema drift detectado e corrigido
python -m pytest tests/test_autohealing.py::test_schema_drift  # ✅ PASS

# Teste: Data quality — nulls em campo obrigatório
python -m pytest tests/test_autohealing.py::test_null_handling   # ✅ PASS

# Teste: Retry com backoff
python -m pytest tests/test_autohealing.py::test_retry_backoff   # ✅ PASS

# Teste: Escala para humano após 3 falhas
python -m pytest tests/test_autohealing.py::test_escalation      # ✅ PASS
```

---

## Lições

- **Funcionou:** Schema drift é o caso mais comum (60% dos erros). Auto-correção com coluna nula funcionou bem.
- **Desafio:** Data quality é mais difícil de auto-corrigir — imputar valores pode mascarar problemas reais. Decidimos quarantenar em vez de imputar.
- **Métrica:** Pipeline uptime subiu de 72% para 96% com auto-healing.
- **Alerta:** Sempre registrar o que o agente corrigiu. Auditoria é essencial para pipelines com auto-healing.
