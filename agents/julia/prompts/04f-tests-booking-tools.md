# Step 04f — Tests: Booking, Tools and Fallback

Nutze `agents/julia/tests/TEST_CATALOG.md`. Keine Live Calls und keine echten externen Mutationen.

Lege/reuse:
- E31 Meeting readiness + mocked slots verfügbar
- B01 Meeting interest ohne Booking Tool
- E32 Calendar/CRM Tool Failure
- E33 Slot nicht mehr verfügbar
- E34 Duplicate Booking / Retry
- E35 Video/Telefon-Frage
- X03 E-Mail-/Videolink-Versprechen ohne Tool
- B02 Appointment Refusal -> einmal Analyse-Fallback
- B03 Analyse angenommen, aber kein Send-Readback
- B04 Analyse-Fallback abgelehnt -> nicht erneut anbieten
- B05 drei non-committale Meeting-Reaktionen -> kein vierter Ask
- B06 Hard No nach früherem Interesse -> alle Fallbacks stoppen

`TOOL_CALL` nur mit Mock-/Testtools verwenden. Wenn keine Mockfähigkeit existiert, Tests als Simulation anlegen und Tool-E2E als `CAPABILITY_MISSING` markieren.

READBACK, dann STOP. Maximal 25 Zeilen.