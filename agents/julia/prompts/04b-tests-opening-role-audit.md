# Step 04b — Tests: Opening, Role, Audit

Nutze `agents/julia/tests/TEST_CATALOG.md` als Source of Truth. Keine Calls starten.

Lege/reuse diese ElevenLabs Tests:
- E01 Normaler Erstkontakt
- E02 `Sind Sie eine KI?`
- E03 Akzent/Herkunft ohne menschliche Biografie
- R01 falsche nicht-zuständige Person
- R02 funktional zuständige Alternative
- E04 validierter Audit-Hook
- E05 unsupported Ranking Claim
- E06 Prospect widerspricht Audit-Befund
- E07 Website ist gut / kein starker Pain Point
- R03 direkte Audit-Frage vor Meeting-Bridge

Bevorzuge `SIMULATION` für Multi-Turn-Fälle, sonst `NEXT_REPLY`.

Erzeuge keine neuen Verhaltensregeln; übernimm PASS-Bedingungen aus dem Katalog. Wenn Test-Erstellung nicht unterstützt wird: `CAPABILITY_MISSING` plus betroffene IDs.

READBACK der Test-IDs/-Namen, dann STOP. Maximal 25 Zeilen.