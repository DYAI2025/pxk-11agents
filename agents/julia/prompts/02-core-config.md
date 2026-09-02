# Step 02 — Apply Julia Core Configuration

Arbeite ausschliesslich auf der in Step 01 ermittelten Julia `agent_id`. Lade als Sollquelle `agents/julia/target-config.json` und `agents/julia/system-prompt.md`.

## Autorisiert in diesem Schritt

- First Message setzen;
- System Prompt setzen;
- LLM/Generation Settings setzen;
- Voice/TTS Settings setzen;
- ASR Settings setzen;
- Turn-Taking / Conversation Flow setzen;
- Conversation Surface setzen, soweit providerseitig verfuegbar.

## Nicht autorisiert

- Tools/Webhooks/MCP anlegen oder binden;
- Google Calendar/CRM anbinden;
- Tests/Evals anlegen;
- Calls starten;
- Secrets setzen oder ausgeben;
- andere Agenten veraendern.

## Candidate-Safe Sollwerte

Nutze die Werte aus `target-config.json` exakt, insbesondere:

- LLM `gemini-3.7-flash`, reasoning `low`, temperature `0.66`;
- Backup LLMs `gemini-2.5-flash`, `qwen35-397b-a17b`, sofern diese im Account unterstuetzt werden;
- Voice ID `6u6JbqKdaQy89ENzLSju`;
- TTS `eleven_v3_conversational`;
- Expressive Mode `true`;
- stability `0.46`, speed `1.04`, similarity `0.8`;
- ASR `scribe_realtime`, quality `high`;
- Turn Model `turn_v3`, timeout `7`, eagerness `normal`, speculative turn `true`;
- max conversation duration `600s`;
- file input fuer candidate-safe deaktiviert;
- keine menschliche Stuttgart-/Herkunftsbiografie;
- keine statische Person `Herr Schnetzer` in der First Message.

Wenn `{{prospect_name}}` oder `{{prospect_salutation}}` leer sein kann, muss die Konfiguration eine neutrale Begruessung erlauben; niemals einen festen fremden Namen als Fallback verwenden.

## Readback Gate

Lies nach der Mutation den Agenten erneut und vergleiche jedes in diesem Schritt gesetzte Feld mit dem Soll.

Wenn ein Sollfeld providerseitig nicht verfuegbar ist, melde `CAPABILITY_MISSING` fuer dieses Feld. Veraendere nicht eigenmaechtig einen Ersatzwert.

## Ausgabe

```json
{
  "status": "PASS|PARTIAL|BLOCKED_UNEXPECTED_DIFF",
  "agent_id": "...",
  "mutations_performed": [],
  "core_readback": {},
  "capability_missing": [],
  "unexpected_diffs": [],
  "warnings": []
}
```
