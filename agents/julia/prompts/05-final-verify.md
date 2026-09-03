# Step 05 — Final Julia Pre-Test Verification

Fuehre ausschliesslich einen vollstaendigen READ-ONLY Readback der in Step 01 bestimmten Julia durch. Keine weiteren Mutationen.

## Sollquellen
- `agents/julia/manifest.json`
- `agents/julia/target-config.json`
- `agents/julia/system-prompt.md`
- `contracts/pixelkiez-v1.3-variable-map.md`
- `agents/julia/tests/TEST_CATALOG.md`
- `shared/verification-contract.md`

## Provider-Konfiguration verifizieren
1. Agent Name/ID und Branch/Version.
2. First Message ohne statischen Fremdnamen.
3. System Prompt entspricht candidate-safe Pre-Test-Repair.
4. LLM + Generation Settings.
5. Voice/TTS/Expressive Mode.
6. ASR + Turn Taking.
7. Conversation Surface.
8. v1.3 Contract Binding: 96 Felder, `phone_number` Transport, 95 Custom Dynamic Variables bzw. providerseitig aequivalente Batch-Surface.
9. Prompt-Bootstrap bleibt bounded; keine 95-fache Blindinjektion in Stable Policy.
10. Knowledge Bindings + RAG ohne offensichtliche Duplikate.
11. Externe CRM/Calendar/MCP Tools fuer diesen Slice weiterhin nicht gebunden.
12. Guardrails.
13. Success Evaluations / Regression Tests.

## Test-Coverage Gate

Der kanonische Repo-Katalog enthaelt **64 Tests**. Pruefe die Step-04-Coverage gegen `agents/julia/tests/TEST_CATALOG.md`.

Besonders explizit vorhanden sein muessen:
- E11 starker Themen-/Gespraechsdrift;
- M01 interessiert -> Termin ploetzlich abgelehnt;
- M02 interessiert -> Hard No;
- M03 interessiert -> spaeter `doch kein Interesse mehr`;
- M04 wechselnde Zustandslage skeptisch/interessiert/unsicher;
- M05 wiederholter persoenlicher/off-topic Drift;
- E14 Busy/Callback;
- E31/E32 Booking Success/Failure Spezifikation;
- E40 Memory Recall;
- E41 widerspruechliche Prospect-Aussagen.

Wenn ElevenLabs bestimmte Testfamilien nicht erstellen kann, duerfen diese als `CAPABILITY_MISSING` gelten, aber nicht stillschweigend fehlen.

## Pre-Test Policy Assertions
Der installierte Prompt muss eindeutig enthalten bzw. bewirken:
- FIRST_CONTACT_DISCLOSURE -> PERMISSION_CHECK -> ROLE_CHECK vor substanziellem Pitch;
- falsche nicht-zustaendige Person bekommt keinen Audit-Pitch und hoechstens eine Routingfrage;
- direkte Fragen werden vor Meeting-Bridging beantwortet;
- SOFT_RESISTANCE != APPOINTMENT_REFUSAL != HARD_NO;
- der neueste Gespraechszustand gewinnt; fruehere Zustimmung wird nicht als dauerhaft behandelt;
- Hard No beendet Persuasion und unterdrueckt jeden Fallback;
- Appointment Refusal darf hoechstens einmal den kostenlosen Analyse-Fallback ausloesen;
- nach drei non-committalen Meeting-Reaktionen kein vierter Ask;
- kein Analyseversand-/Booking-/Opt-out-Erfolg ohne positiven Readback;
- Lead-Quelle und kommerzieller Kontext werden wahrheitsgemaess behandelt; keine erfundene Einwilligung;
- keine menschliche Stuttgart-/Herkunftsbiografie;
- keine Mitarbeiter-/Owner-Leakage oder unsupported Claims.

## Diff-Regeln
Nicht lesbare Providerfelder = `SOURCE_NEEDED`, nicht automatisch Fehler. Unerwartete Werte = `unexpected_diffs`. Contract-Feldverlust/Umbenennung = `BLOCKED_CONTRACT_DRIFT`.

## Test-Readiness
`CONFIGURED_VERIFIED` bedeutet nur: Sollkonfiguration ist providerseitig gebunden/readback-geprueft. Es bedeutet NICHT automatisch `BEHAVIOR_TESTED`, Tool-E2E, Telephony-E2E oder Live-Outbound-Freigabe.

Interner Conversation-Test ist erst `READY_FOR_INTERNAL_CONVERSATION_TEST`, wenn:
- Config Readback ohne Blocker;
- Pre-Test Policy Assertions vorhanden;
- der 64-Test-Katalog vollständig angelegt/reused oder jede nicht provisionierbare ID explizit als Capability Gap dokumentiert ist;
- keine Live-Call-Autorisierung daraus abgeleitet wird.

## Ausgabe
```json
{
  "status": "CONFIGURED_VERIFIED|CONFIGURED_PARTIAL|BLOCKED_CAPABILITY|BLOCKED_CONTRACT_DRIFT|BLOCKED_UNEXPECTED_DIFF|NOT_CONFIGURED",
  "agent_key": "julia",
  "agent_id": "...",
  "profile": "candidate-safe",
  "branch_id": "...|SOURCE_NEEDED",
  "version_id": "...|SOURCE_NEEDED",
  "verified_sections": [],
  "contract_readback": {},
  "pre_test_policy_assertions": {},
  "test_catalog_count": 64,
  "tests_created_or_reused": [],
  "missing_test_ids": [],
  "test_capability_gaps": [],
  "source_needed": [],
  "capability_missing": [],
  "unexpected_diffs": [],
  "tests_executed": false,
  "behavior_tested": false,
  "internal_conversation_test_readiness": "READY_FOR_INTERNAL_CONVERSATION_TEST|NOT_READY",
  "known_unwired_capabilities": ["crm_tools", "calendar_tools", "analysis_delivery_tool", "external_mcp", "live_calling"],
  "live_call_authorized": false,
  "receipt_ready": true,
  "warnings": []
}
```

Danach Receipt gemaess `receipts/RECEIPT_TEMPLATE.md` erzeugen.
