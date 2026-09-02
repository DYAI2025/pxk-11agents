# Agent Execution Instructions

Diese Datei richtet sich an GPT, Claude, Cloud Browser und andere Ausfuehrungsagenten.

## Repository Authority

- `registry/agents.json` entscheidet, welche Agenten existieren und installierbar sind.
- `agents/<key>/manifest.json` definiert Identitaet, Modus und Quellen.
- `agents/<key>/target-config.json` ist die maschinenlesbare Soll-Konfiguration.
- `agents/<key>/system-prompt.md` ist der Soll-Systemprompt fuer `candidate-safe`.
- `agents/<key>/execution-plan.md` definiert die Reihenfolge.
- `agents/<key>/prompts/*.md` sind die Copy-Paste-/MCP-Anweisungen an den ElevenLabs Architect.
- `receipts/` enthaelt keine Secrets, sondern nur IDs, Readbacks, Diffs und Status.

## Standardverhalten

1. Frage nur nach `agent_key`, falls nicht angegeben.
2. Default: `candidate-safe`.
3. Fuehre niemals mehrere Prompt-Schritte gleichzeitig aus.
4. Nach jeder Mutation: read-only Readback und Vergleich.
5. Bei Diff: STOP mit `BLOCKED_UNEXPECTED_DIFF`.
6. Keine Live Calls waehrend Provisioning.
7. Keine Secrets ausgeben oder in Dateien schreiben.

## Replica Current

`replica-current` bedeutet historische Reproduktion des dokumentierten Provider-Zustands. Dieser Modus darf bekannte Defekte enthalten und ist nicht fuer neue produktive Accounts empfohlen. Wenn der User nur sagt "Julia anlegen", nutze `candidate-safe`.

## Candidate Safe

`candidate-safe` konserviert Julias Stimme/Naturalness und zentrale Gespraechs-DNA, repariert aber bekannte Baseline-Defekte wie statische Personennamen und erfundene menschliche Biografie.
