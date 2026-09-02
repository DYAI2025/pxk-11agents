# Julia Provisioning Execution Plan

Default profile: `candidate-safe`.

## Reihenfolge

| Step | Prompt | Zweck | Gate |
| --- | --- | --- | --- |
| 01 | `prompts/01-discover-and-create.md` | Workspace lesen, Julia eindeutig aufloesen oder neu anlegen | Agent ID vorhanden |
| 02 | `prompts/02-core-config.md` | LLM, Voice, ASR, Turn Taking, First Message, System Prompt | Core Readback match |
| 03 | `prompts/03-knowledge-and-variables.md` | Dynamic Variables + kuratierte KB/RAG-Bindings | Context Readback match |
| 04 | `prompts/04-evals-and-guardrails.md` | Guardrails, Success Evals und Tests soweit Providerfaehigkeit vorhanden | Eval Surface dokumentiert |
| 05 | `prompts/05-final-verify.md` | Gesamten Agenten read-only vergleichen und Receipt erzeugen | CONFIGURED_VERIFIED/PARTIAL |

## Regeln

- Keine Schritte parallelisieren.
- Keine Live Calls.
- Keine CRM-/Calendar-/External-MCP-Tools in v1 binden.
- Bei bestehender Julia nicht blind duplizieren: zuerst vergleichen.
- Wenn `candidate-safe` und ein bestehender Agent offensichtlich die historische Julia mit bekannten Defekten ist, veraendere ihn nur, wenn der User explizit "aktualisieren" statt "neu anlegen" gewaehlt hat. Sonst neue Julia-Kopie im Account anlegen.
- `replica-current` muss explizit verlangt werden und ist nicht der Default dieses Plans.

## Abschluss

Speichere/zeige nach Step 05 einen Receipt gemaess `/receipts/RECEIPT_TEMPLATE.md`.
