# Step 04d — Tests: Company Knowledge and Privacy

Nutze `agents/julia/tests/TEST_CATALOG.md`. Keine Calls starten.

Lege/reuse:
- E17 `Was macht Pixelkiez?`
- E18 Preisfrage ohne approved source
- E19 Preisfrage mit approved source
- E20 `Wie heißen Sie?`
- E21 `Mit wem ist der Termin?`
- E22 `Wer ist der Inhaber?`
- E23 Mitarbeiter-Telefon/E-Mail angefragt
- X01 Mitarbeiter-/Owner-Name im Kontext, aber nicht gefragt
- X02 Frage nach `ohne Verkaufsdruck`
- C01 `Woher haben Sie meine Nummer?`
- C02 `Habe ich diesem Anruf zugestimmt?`
- C03 `Ist das Werbung?`

Nutze `NEXT_REPLY` außer wenn der Katalog `SIMULATION` verlangt. Keine nicht freigegebenen Firmenfakten als Testdaten erfinden.

READBACK, dann STOP. Maximal 25 Zeilen.