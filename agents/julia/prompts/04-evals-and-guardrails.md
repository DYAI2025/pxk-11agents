# Step 04 — Julia ElevenLabs Test Provisioning Router

Dieser Step ist ein **Orchestrator**, kein Mega-Prompt fuer den ElevenLabs Architect.

## Source of Truth

Lies zuerst:

`agents/julia/tests/TEST_CATALOG.md`

Der Katalog enthaelt 64 konkrete Tests aus:
- Confluence E01–E41;
- Transcript EVAL-T01–T15;
- Pre-Test-Repair;
- zusaetzlichen Multi-Turn-State-/Drift-Grenzfaellen.

## Pflichtreihenfolge

Fuehre diese Dateien **einzeln und sequenziell** gegen dieselbe Julia `agent_id` aus:

1. `04a-guardrails-and-evaluators.md`
2. `04b-tests-opening-role-audit.md`
3. `04c-tests-adaptivity-state.md`
4. `04d-tests-company-privacy.md`
5. `04e-tests-boundaries-data.md`
6. `04f-tests-booking-tools.md`
7. `04g-tests-knowledge-memory-compliance.md`

Nach jedem Shard:
- Provider-Readback pruefen;
- angelegte/reused Test-IDs dokumentieren;
- bei unerwartetem Diff STOP;
- bei fehlender Providerfunktion `CAPABILITY_MISSING` dokumentieren;
- niemals fehlende Tests als erfolgreich angelegt behaupten.

## Wichtige Regel

**Niemals alle sieben Shards zu einem einzigen ElevenLabs-Architect-Prompt zusammenfassen.**

Die Konfiguration darf Tests anlegen/reusen, aber **keine Tests automatisch ausfuehren** und keine Live Calls starten. Testausfuehrung braucht separate Autorisierung.

## Abschluss von Step 04

Erstelle eine Coverage-Zusammenfassung:

```json
{
  "status": "PASS|PARTIAL|BLOCKED",
  "catalog_test_count": 64,
  "tests_created_or_reused": [],
  "missing_test_ids": [],
  "success_evaluators_created_or_reused": [],
  "capability_missing": [],
  "unexpected_diffs": [],
  "tests_executed": false,
  "behavior_tested": false
}
```

`PASS` fuer die Provisioning-Surface bedeutet: alle providerseitig unterstuetzten Tests wurden angelegt/reused und nicht unterstuetzte Familien sind explizit als Capability Gap dokumentiert. Es bedeutet nicht, dass Verhalten bestanden wurde.
