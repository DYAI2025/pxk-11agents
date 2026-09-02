# Julia Provisioning Execution Plan

Default profile: `candidate-safe`.

## Reihenfolge

| Step | Prompt | Zweck | Gate |
| --- | --- | --- | --- |
| 01 | `prompts/01-discover-and-create.md` | Workspace lesen, Julia eindeutig aufloesen oder neu anlegen | Agent ID vorhanden |
| 02 | `prompts/02-core-config.md` | LLM, Voice, ASR, Turn Taking, First Message, System Prompt | Core Readback match |
| 03 | `prompts/03-knowledge-and-variables.md` | Dynamic Variables + kuratierte KB/RAG-Bindings | Context Readback match |
| 04 | `prompts/04-evals-and-guardrails.md` | Router fuer vollstaendige Test-/Eval-Provisionierung | Test Coverage dokumentiert |
| 04a | `prompts/04a-guardrails-and-evaluators.md` | Guardrails + Success Evaluators | Readback |
| 04b | `prompts/04b-tests-opening-role-audit.md` | Opening/Role/Audit Tests | Readback |
| 04c | `prompts/04c-tests-adaptivity-state.md` | Multi-Turn Adaptivity/State Tests | Readback |
| 04d | `prompts/04d-tests-company-privacy.md` | Company/Privacy Tests | Readback |
| 04e | `prompts/04e-tests-boundaries-data.md` | Boundary/Data-Capture Tests | Readback |
| 04f | `prompts/04f-tests-booking-tools.md` | Booking/Tool/Fallback Tests | Readback |
| 04g | `prompts/04g-tests-knowledge-memory-compliance.md` | Knowledge/Memory/Compliance Tests | Readback |
| 05 | `prompts/05-final-verify.md` | Gesamten Agenten read-only vergleichen und Receipt erzeugen | CONFIGURED_VERIFIED/PARTIAL |

## Test Source of Truth

`agents/julia/tests/TEST_CATALOG.md` enthaelt aktuell 64 Tests und ist fuer Step 04 verbindlich.

Step 04a–04g muessen einzeln ausgefuehrt werden. Nicht zu einem Mega-Prompt zusammenfassen.

## Regeln

- Keine Schritte parallelisieren.
- Keine Live Calls.
- Testdefinitionen duerfen provisioniert werden; automatische Testausfuehrung ist nicht Teil dieses Plans.
- Keine CRM-/Calendar-/External-MCP-Tools in v1 binden.
- Bei bestehender Julia nicht blind duplizieren: zuerst vergleichen.
- Wenn `candidate-safe` und ein bestehender Agent offensichtlich die historische Julia mit bekannten Defekten ist, veraendere ihn nur, wenn der User explizit "aktualisieren" statt "neu anlegen" gewaehlt hat. Sonst neue Julia-Kopie im Account anlegen.
- `replica-current` muss explizit verlangt werden und ist nicht der Default dieses Plans.

## Abschluss

Speichere/zeige nach Step 05 einen Receipt gemaess `/receipts/RECEIPT_TEMPLATE.md`.
