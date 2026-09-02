# pxk-11agents

Reproduzierbares Provisioning-Harness fuer Pixelkiez ElevenLabs Agents.

## Ziel

Ein Mensch, GPT/ChatGPT Work Cloud Browser, Claude oder ein anderer Ausfuehrungsagent soll dieses Repository lesen und ohne Architektur-Rueckfragen einen definierten Pixelkiez-Agenten in einem ElevenLabs-Account anlegen oder aktualisieren koennen.

Der einzige normale User-Entscheidungspunkt ist:

> Welcher Agent soll angelegt werden?

Danach wird die im Repository versionierte Prompt-Sequenz Schritt fuer Schritt an den ElevenLabs Architect / ElevenLabs Hosted MCP uebergeben. Jeder Schritt verlangt Readback und erzeugt Evidenz fuer den naechsten Schritt.

## Start

1. Oeffne `GPT_START_HERE.md`.
2. Waehle einen Agenten aus `registry/agents.json`.
3. Standardmodus ist `candidate-safe`.
4. Fuehre die in `agents/<agent>/execution-plan.md` referenzierten Prompts in Reihenfolge aus.
5. Speichere den abschliessenden Readback nach `receipts/RECEIPT_TEMPLATE.md`.

## Sicherheitsmodell

- Keine API Keys, Tokens oder Credentials in Git.
- Keine produktiven Calls als Teil des Provisionings.
- Keine erfundenen Provider-Erfolge: jeder Mutationsschritt braucht Readback.
- `replica-current` ist nur fuer historische Reproduktion; bekannte Defekte werden nicht zum Default-Sollzustand.
- `candidate-safe` ist das Default-Profil fuer neue Accounts.
- Live-Outbound bleibt ein separates Compliance-/Release-Gate.

## Repository-Struktur

```text
GPT_START_HERE.md
AGENTS.md
registry/agents.json
shared/
  architect-contract.md
  execution-protocol.md
  verification-contract.md
agents/
  julia/
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
receipts/
  RECEIPT_TEMPLATE.md
```

## Agenten

Aktuell registriert:

- `julia` — Pixelkiez B2B Website-Audit / Appointment Voice Agent.

Neue Agenten werden ausschliesslich ueber einen eigenen Ordner unter `agents/` plus Eintrag in `registry/agents.json` hinzugefuegt.
