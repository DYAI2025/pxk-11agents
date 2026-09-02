# ElevenLabs Architect Contract

Diese Regeln gelten fuer jeden Prompt an den ElevenLabs Architect / Hosted MCP.

## Truth Rules

- Lies vor jeder Mutation den aktuellen Workspace-/Agentzustand.
- Erfinde keine IDs, Defaults, Settings oder Providererfolge.
- Unlesbare Felder werden als `SOURCE_NEEDED` oder `CAPABILITY_MISSING` gemeldet.
- Fehlende Felder bedeuten nicht automatisch `false` oder deaktiviert.
- Nach jeder Mutation ist ein Readback Pflicht.

## Mutation Rules

- Mutationen nur am explizit gewaehlten Agenten.
- Keine produktiven Calls, Batch-Starts, Retries oder Deletes.
- Keine anderen Agenten veraendern.
- Keine Secrets ausgeben.
- Bestehende Agenten nicht blind ueberschreiben: zuerst identifizieren, dann vergleichen.
- Bei Neuanlage zuerst Agent erzeugen, ID lesen, anschliessend schrittweise konfigurieren.
- Bei bestehendem Agenten nur die im aktuellen Schritt autorisierten Felder veraendern.

## Tool Model

- Neue Client-/Webhook-/Code-Tools werden als Workspace-Tools angelegt und ueber `prompt.tool_ids` gebunden.
- System Tools werden ueber `prompt.built_in_tools` konfiguriert.
- Legacy `prompt.tools` darf nicht fuer neue Konfiguration verwendet werden.
- MCP-Bindings nur, wenn die Agent-Definition dies explizit verlangt.

## Verification

Jeder Schritt muss liefern:

```json
{
  "status": "PASS|PARTIAL|BLOCKED",
  "agent_id": "...",
  "agent_name": "...",
  "mutations_performed": [],
  "readback": {},
  "unexpected_diffs": [],
  "source_needed": [],
  "warnings": []
}
```

Wenn `unexpected_diffs` nicht leer ist: `BLOCKED_UNEXPECTED_DIFF` und keine weiteren Mutationen.
