# Adding a New ElevenLabs Agent

Neue Agenten duerfen den Provisioning-Orchestrator nicht veraendern. Sie werden als Daten-/Prompt-Paket hinzugefuegt.

## Pflichtstruktur

```text
agents/<agent_key>/
  manifest.json
  target-config.json
  system-prompt.md
  execution-plan.md
  prompts/
    01-discover-and-create.md
    02-core-config.md
    03-knowledge-and-variables.md
    04-evals-and-guardrails.md
    05-final-verify.md
```

## Pflichtschritte

1. `agent_key` eindeutig waehlen: lowercase, stabil, keine Leerzeichen.
2. Agent in `registry/agents.json` registrieren.
3. `manifest.json` mit Zweck, Sprache, Modi, Quellen, geschuetzten Eigenschaften und bekannten Defekten erstellen.
4. `target-config.json` als maschinenlesbare Soll-Konfiguration erstellen.
5. Vollstaendigen Soll-Systemprompt als `system-prompt.md` ablegen.
6. Fuenf sequenzielle Architect-Prompts bereitstellen.
7. Jeder Mutationsprompt muss einen Readback verlangen.
8. Live Calls muessen fuer Provisioning standardmaessig deaktiviert bleiben.
9. Bei Nutzung in einem Batch den Agenten explizit in `batches/<batch>.json` aufnehmen.

## Designregel

Charakter/Persona, Voice, Branche, Prompt, Knowledge und Eval-Set koennen pro Agent variieren. Der Orchestrierungsvertrag bleibt gleich.

Damit koennen z. B. spaeter ein maennlicher Agent, eine andere Sprachpersona oder spezialisierte Inbound-Agenten hinzukommen, ohne den GPT-Startprompt umzubauen.

## Merge Gate

Vor Merge eines neuen Agenten pruefen:

- Registry referenziert existierenden Ordner;
- alle Pflichtdateien vorhanden;
- JSON parsebar;
- kein Secret enthalten;
- First Message nutzt keine fremden statischen Personendaten;
- Systemprompt legt KI-Identitaet und Tool-Truthfulness fest, sofern der Use Case dies verlangt;
- Tool-/MCP-Bindings sind explizit statt implizit;
- finaler Verify-Prompt deckt alle mutierten Bereiche ab.
