# Step 05 — Final Julia Verification

Fuehre jetzt ausschliesslich einen vollstaendigen READ-ONLY Readback der in Step 01 bestimmten Julia durch. Keine weiteren Mutationen.

## Sollquellen

- `agents/julia/manifest.json`
- `agents/julia/target-config.json`
- `agents/julia/system-prompt.md`
- `shared/verification-contract.md`

## Verifizieren

1. Agent Name und ID.
2. Branch/Version soweit verfuegbar.
3. First Message.
4. System Prompt / eindeutiger Prompt-Readback.
5. LLM + Generation Settings.
6. Voice/TTS/Expressive Mode.
7. ASR + Turn Taking.
8. Conversation Surface.
9. Dynamic Variables.
10. Knowledge Bindings + RAG.
11. `tool_ids` — fuer v1 weiterhin keine externen CRM/Calendar Tools.
12. `built_in_tools` — nur was in Step 02/04 explizit gesetzt wurde.
13. MCP Bindings — fuer v1 leer.
14. Guardrails.
15. Success Evaluations / Tests, soweit im Account verwaltbar.

## Diff-Regeln

- Vergleiche Wert fuer Wert gegen `target-config.json`.
- Erwarte KEINEN statischen Namen `Herr Schnetzer`.
- Erwarte KEINE menschliche Stuttgart-/Herkunftsbiografie im Prompt.
- Erwarte keine gebundenen externen CRM-, Calendar- oder MCP-Tools in diesem v1-Slice.
- Nicht lesbare Felder sind `SOURCE_NEEDED`, nicht automatisch Fehler.
- Unerwartete veraenderte Felder sind `unexpected_diffs`.

## Abschlussstatus

Nutze nur:

- `CONFIGURED_VERIFIED`
- `CONFIGURED_PARTIAL`
- `BLOCKED_CAPABILITY`
- `BLOCKED_UNEXPECTED_DIFF`
- `NOT_CONFIGURED`

## Ausgabe

```json
{
  "status": "CONFIGURED_VERIFIED|CONFIGURED_PARTIAL|BLOCKED_CAPABILITY|BLOCKED_UNEXPECTED_DIFF|NOT_CONFIGURED",
  "agent_key": "julia",
  "agent_id": "...",
  "profile": "candidate-safe",
  "branch_id": "...|SOURCE_NEEDED",
  "version_id": "...|SOURCE_NEEDED",
  "verified_sections": [],
  "source_needed": [],
  "capability_missing": [],
  "unexpected_diffs": [],
  "known_unwired_capabilities": ["crm_tools", "calendar_tools", "external_mcp", "live_calling"],
  "live_call_authorized": false,
  "receipt_ready": true,
  "warnings": []
}
```

Anschliessend formatiere denselben Befund gemaess `receipts/RECEIPT_TEMPLATE.md` fuer die Ablage im Repository oder die Rueckgabe an den User.
