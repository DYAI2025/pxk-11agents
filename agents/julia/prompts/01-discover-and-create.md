# Step 01 — Discover and Create/Resolve Julia

Du arbeitest im ElevenLabs Account des aktuell eingeloggten Users. Fuehre nur Discovery und Agent-Aufloesung/Neuanlage durch. Keine Verhaltenskonfiguration ausser dem minimal no-op Agent-Create, falls Julia noch nicht existiert.

## Soll-Agent

- Name: `Julia`
- Agent Key: `julia`
- Provisioning Profile: `candidate-safe`

## Vorgehen

1. Liste/lese die vorhandenen ElevenLabs Agents im Workspace.
2. Suche exakt nach `Julia`.
3. Falls genau eine Julia existiert: lies ihre Agent ID, Branch/Version soweit verfuegbar und ihren aktuellen Core-Zustand. Veraendere noch nichts.
4. Falls mehrere Agents `Julia` heissen: STOPPE und gib die Kandidaten mit Agent IDs aus. Veraendere nichts.
5. Falls keine Julia existiert: erstelle einen neuen Agent namens `Julia` mit minimalen Defaults, ohne Tools, MCP, Calls oder produktive Integrationen. Lies danach die neue Agent ID zurueck.
6. Starte keinen Call und keine Batch-Ausfuehrung.
7. Gib keine Secrets aus.

## Erwartete Ausgabe

```json
{
  "status": "PASS|BLOCKED",
  "action": "RESOLVED_EXISTING|CREATED_NEW|AMBIGUOUS",
  "agent_name": "Julia",
  "agent_id": "...",
  "branch_id": "...|SOURCE_NEEDED",
  "version_id": "...|SOURCE_NEEDED",
  "existing_state_summary": {},
  "mutations_performed": [],
  "unexpected_diffs": [],
  "warnings": []
}
```

Wenn `AMBIGUOUS`: keine weitere Aktion.
