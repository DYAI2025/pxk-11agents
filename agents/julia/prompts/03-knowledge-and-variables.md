# Step 03 — Configure Julia Context Surface

Arbeite ausschliesslich auf der in Step 01 ermittelten Julia `agent_id`. Nutze `agents/julia/target-config.json` als Sollquelle.

## Ziel

Eine kleine, reproduzierbare Bootstrap-Surface konfigurieren. Der grosse Pixelkiez Batch-/Traceability-Contract wird nicht blind als LLM-Kontext injiziert.

## Dynamic Variables

Stelle exakt diese Custom Variables bereit:

- `company_name`
- `company_website`
- `prospect_name`
- `prospect_salutation`
- `call_compliance_status`
- `call_compliance_note`
- `do_not_contact`
- `lead_source`
- `consultant_name`
- `meeting_duration_minutes`
- `meeting_description`
- `offer_process`
- `website_analysis_report`
- `agency_name`
- `verified_finding`

Setze `agency_name=Pixelkiez`, falls Default-Werte providerseitig unterstuetzt werden. Alle lead-spezifischen Werte bleiben leer/default-neutral und werden spaeter pro Conversation geliefert. Keine Testpersonen oder realen Kundendaten als Defaults hinterlegen.

## Knowledge Base / RAG

1. Lies zuerst bestehende Knowledge Bindings der Julia.
2. Vermeide Duplikate.
3. Binde/erzeuge nur die kuratierten Pixelkiez Quellen aus `target-config.json`, soweit sie im Account erreichbar und unterstuetzt sind.
4. Aktiviere RAG mit:
   - embedding `multilingual_e5_large_instruct`;
   - optional_rag `false`;
   - max_vector_distance `0.6`;
   - max_documents_length `50000`;
   - max_retrieved_chunks `20`.
5. Lead-spezifische Website-Audits NICHT als dauerhafte Knowledge-Base-Dokumente speichern. Sie kommen spaeter pro Call ueber `website_analysis_report` bzw. scoped Tools.
6. Keine Tools, MCP oder Calendar-Integration in diesem Schritt.

## Readback Gate

Lies Dynamic Variables und KB/RAG Bindings erneut. Melde Duplikate oder unerwartete Quellen als Diff; loesche nichts, was nicht eindeutig von diesem Provisioning erzeugt wurde.

## Ausgabe

```json
{
  "status": "PASS|PARTIAL|BLOCKED_UNEXPECTED_DIFF",
  "agent_id": "...",
  "variables_readback": [],
  "knowledge_readback": [],
  "rag_readback": {},
  "created_resources": [],
  "existing_resources_reused": [],
  "capability_missing": [],
  "unexpected_diffs": [],
  "warnings": []
}
```
