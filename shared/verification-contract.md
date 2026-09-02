# Verification Contract

Ein Agent gilt nach Provisioning nur als `CONFIGURED_VERIFIED`, wenn der finale Readback mindestens folgende Punkte eindeutig bestaetigt:

- Agent ID und Name;
- Branch/Version, falls im Account verfuegbar;
- First Message;
- System Prompt oder dessen eindeutig vergleichbarer Hash/Readback;
- LLM und Generation Settings;
- Voice ID, TTS Model und Voice Parameter;
- ASR und Turn-Taking;
- Dynamic Variables;
- Knowledge/RAG Bindings;
- `tool_ids` und `built_in_tools`;
- MCP Bindings;
- Guardrails;
- Success Evaluations / Tests soweit vom Account/API unterstuetzt.

## Status Labels

- `CONFIGURED_VERIFIED` — Sollzustand im Provider gelesen und verglichen.
- `CONFIGURED_PARTIAL` — Kernzustand stimmt, einzelne nicht-kritische Providerfelder sind nicht lesbar.
- `BLOCKED_CAPABILITY` — Account/Plan/UI/API bietet benoetigte Funktion nicht.
- `BLOCKED_UNEXPECTED_DIFF` — Readback weicht unerwartet vom Soll ab.
- `NOT_CONFIGURED` — Provisioning nicht abgeschlossen.

## Was dieser Status nicht beweist

`CONFIGURED_VERIFIED` bedeutet nicht:

- Behavior-Evals bestanden;
- CRM/Calendar/Webhook real funktionsfaehig;
- Telefonie produktionsbereit;
- Live-Outbound rechtlich freigegeben;
- echte Calls erfolgreich.

Diese Gates werden separat behandelt.
