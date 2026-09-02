# Agent Execution Instructions

Diese Datei richtet sich an GPT, Claude, Codex, Cloud Browser und andere Ausfuehrungsagenten.

## First-use rule

Wenn der Nutzer das Repository zum ersten Mal benutzt oder nach dem konkreten Vorgehen fragt, lies zuerst `COLLEAGUE_QUICKSTART.md` und erklaere exakt den dort definierten einfachen Einstieg. Stelle keine Architekturfragen, die im Repository bereits beantwortet sind.

## Repository Authority

- `COLLEAGUE_QUICKSTART.md` erklaert den menschlichen Start fuer Browser/Chrome, Codex und Copy/Paste.
- `registry/agents.json` entscheidet, welche Agenten existieren und installierbar sind.
- `agents/<key>/manifest.json` definiert Identitaet, Modus und Quellen.
- `agents/<key>/target-config.json` ist die maschinenlesbare Soll-Konfiguration.
- `agents/<key>/system-prompt.md` ist der Soll-Systemprompt fuer `candidate-safe`.
- `agents/<key>/execution-plan.md` definiert die Reihenfolge.
- `agents/<key>/prompts/*.md` sind die sequenziellen Anweisungen an den ElevenLabs Architect bzw. dieselben Sollschritte fuer CLI/API/Browser-Ausfuehrung.
- `receipts/` enthaelt keine Secrets, sondern nur IDs, Readbacks, Diffs und Status.

## Standardverhalten

1. Frage nur nach `agent_key`, falls nicht angegeben.
2. Default: `candidate-safe`.
3. Fuehre niemals mehrere Prompt-Schritte gleichzeitig aus.
4. Nach jeder Mutation: read-only Readback und Vergleich.
5. Bei Diff: STOP mit `BLOCKED_UNEXPECTED_DIFF`.
6. Keine Live Calls waehrend Provisioning.
7. Keine Secrets ausgeben oder in Dateien schreiben.
8. Wenn Browserzugriff existiert: Browser selbst bedienen.
9. Wenn authentifizierte ElevenLabs CLI/API/Agents-Skill vorhanden ist: diese darf fuer dieselben Repository-Schritte benutzt werden.
10. Wenn keine direkte Ausfuehrung moeglich ist: nur den naechsten Copy-Paste-Prompt ausgeben.

## Replica Current

`replica-current` bedeutet historische Reproduktion des dokumentierten Provider-Zustands. Dieser Modus darf bekannte Defekte enthalten und ist nicht fuer neue produktive Accounts empfohlen. Wenn der User nur sagt "Julia anlegen", nutze `candidate-safe`.

## Candidate Safe

`candidate-safe` konserviert Julias Stimme/Naturalness und zentrale Gespraechs-DNA, repariert aber bekannte Baseline-Defekte. Ein Repository-Target ist noch kein Provider-Beweis: erst Step 05 darf einen finalen Config-Status liefern.
