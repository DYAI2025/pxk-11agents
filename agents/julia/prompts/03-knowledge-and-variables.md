# Step 03 — Configure Julia Context + v1.3 Contract Surface

Arbeite ausschliesslich auf der in Step 01 ermittelten Julia `agent_id`.

Sollquellen:
- `agents/julia/target-config.json`
- `contracts/pixelkiez-v1.3-variable-map.md`

## 1. Contract Gate

Pruefe zuerst, dass der Sollvertrag exakt ist:
- contract: `pixelkiez-elevenlabs-batch-contract-v1.3`
- version: `1.3.0`
- 96 Felder gesamt
- `phone_number` = Transportfeld
- 95 case-sensitive Custom Dynamic Variables
- source SHA-256 = `ed9924084c479c3627ceb2648ef301162d5b99bbfddfe3fefe265c7cec915d38`

Kein stilles Umbenennen, Weglassen oder Hinzufuegen von Contract-Feldern.

## 2. Provider Dynamic Variable Surface

Stelle am Provider-/Batch-Rand alle 95 Custom Dynamic Variables aus `contracts/pixelkiez-v1.3-variable-map.md` bereit, soweit ElevenLabs die Variable-Definition auf Agentebene erwartet/unterstuetzt.

WICHTIG: 95 Provider-Variablen bedeuten NICHT 95 Prompt-Injektionen.

Der stabile Julia-Systemprompt referenziert nur den in `target-config.json` definierten `prompt_bootstrap_variables`-Subset. INTERNAL_RECORD, OPTIONAL und PRODUCTION_GATE_ONLY Daten werden nicht automatisch gesprochen oder in jeden Turn injiziert.

Nutze Runtime-Defaults nur gemaess dem v1.3-Vertrag. Keine realen Kundendaten als statische Defaults speichern.

Wenn die Provider-Oberflaeche keine explizite Definition aller 95 Variablen verlangt, dokumentiere dies als Provider-Verhalten; veraendere den kanonischen Contract deshalb nicht.

## 3. Knowledge Base / RAG

1. Lies bestehende Knowledge Bindings.
2. Vermeide Duplikate.
3. Binde nur die kuratierten Pixelkiez-Quellen aus `target-config.json`.
4. RAG Soll:
   - `multilingual_e5_large_instruct`
   - optional_rag `false`
   - max_vector_distance `0.6`
   - max_documents_length `50000`
   - max_retrieved_chunks `20`
5. Lead-spezifische Audits NICHT als permanente KB-Dokumente speichern; per Conversation/Tool liefern.
6. Keine CRM-, Calendar- oder MCP-Tools in diesem Schritt.

## Readback Gate

Lies Variable-Surface und KB/RAG erneut.

PASS nur wenn:
- der v1.3 Contract nicht reduziert/umbenannt wurde;
- der Bootstrap-Subset weiterhin bounded ist;
- keine fremden Kundendaten als Defaults gespeichert wurden;
- Knowledge keine offensichtlichen Duplikate/unerwarteten Bindings enthaelt.

## Ausgabe

```json
{
  "status": "PASS|PARTIAL|BLOCKED_CONTRACT_DRIFT|BLOCKED_UNEXPECTED_DIFF",
  "agent_id": "...",
  "contract_id": "pixelkiez-elevenlabs-batch-contract-v1.3",
  "contract_field_count": 96,
  "provider_custom_variable_count_expected": 95,
  "provider_custom_variable_count_readback": null,
  "prompt_bootstrap_variables_readback": [],
  "knowledge_readback": [],
  "rag_readback": {},
  "capability_missing": [],
  "unexpected_diffs": [],
  "warnings": []
}
```
