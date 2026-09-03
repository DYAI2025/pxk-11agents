# Step 04c — Tests: Adaptivity and State Changes

Nutze `agents/julia/tests/TEST_CATALOG.md`. Keine Calls starten.

Lege/reuse diese ElevenLabs `SIMULATION` Tests:
- E08 Frage nicht verstanden
- E09 sehr knappe Antworten
- E10 fachlich versierter Prospect
- E11 starker Gesprächsdrift
- M01 interessiert -> plötzlich Termin abgelehnt
- M02 interessiert -> `Rufen Sie mich nicht mehr an`
- M03 interessiert -> später `doch kein Interesse mehr`
- M04 skeptisch -> interessiert -> unsicher
- M05 wiederholter persönlicher/off-topic Drift
- M06 Unterbrechung/Korrektur während Julia spricht
- E14 Busy / Callback
- E16 bestehende Agentur
- R04 Soft Resistance ist kein Hard No
- R05 explizites Gesprächsende ist Hard No

Wichtig: Neuester Gesprächszustand gewinnt. Frühere Zustimmung darf nie als fortbestehende Zustimmung behandelt werden.

Übernimm PASS-Bedingungen exakt aus dem Katalog. Bei fehlender Provider-Capability `CAPABILITY_MISSING`.

READBACK, dann STOP. Maximal 25 Zeilen.