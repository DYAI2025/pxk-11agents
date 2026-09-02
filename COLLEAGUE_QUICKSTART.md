# Kollegen-Quickstart: Pixelkiez Agents in ElevenLabs anlegen

Diese Anleitung ist absichtlich einfach. Du musst die Agentenarchitektur nicht selbst entscheiden. Das Repository ist die Source of Truth.

## Was du am Ende sagen musst

Fuer einen einzelnen Agenten:

> Lege Julia an.

Fuer alle aktuell im Standard-Batch enthaltenen Agenten:

> Provisioniere batch pixelkiez-default.

Standard ist immer `candidate-safe`. Verwende `replica-current` nur, wenn du ausdruecklich eine historische Reproduktion willst.

---

# Einmalige Vorbereitung

## 1. Repository holen

Im Terminal:

```bash
git clone https://github.com/DYAI2025/pxk-11agents.git
cd pxk-11agents
git checkout feat/agent-provisioning-harness-v1
```

Solange PR #1 noch nicht nach `main` gemerged ist, muss dieser Branch verwendet werden. Nach dem Merge reicht `main`.

## 2. In ElevenLabs anmelden

Melde dich im Browser in genau dem ElevenLabs-Account/Workspace an, in dem die Agenten angelegt werden sollen.

Keine API-Keys in dieses Repository, in Prompts oder in Receipts kopieren.

---

# Weg A — Claude mit Browser/Chrome

Nutze diesen Weg, wenn Claude den eingeloggten ElevenLabs-Browser bedienen kann.

## Schritt A1

Oeffne in Chrome:

1. den eingeloggten ElevenLabs-Workspace;
2. dieses Repository bzw. lasse Claude den lokalen Repository-Ordner lesen.

## Schritt A2

Gib Claude genau diesen Auftrag:

> Arbeite im Repository `pxk-11agents`. Lies zuerst `COLLEAGUE_QUICKSTART.md`, `GPT_START_HERE.md` und `AGENTS.md`. Lege den Agenten `julia` im Modus `candidate-safe` in meinem aktuell eingeloggten ElevenLabs-Workspace an. Nutze den ElevenLabs Architect im Browser und arbeite `agents/julia/prompts/01-discover-and-create.md` bis `05-final-verify.md` strikt nacheinander ab. Nach jeder Mutation musst du den Providerzustand erneut lesen und gegen das Repository vergleichen. Bei einem unerwarteten Diff stoppe. Starte keine Live Calls. Am Ende gib mir den Verification-Status und einen Receipt.

## Schritt A3

Claude fuehrt nun selbst aus:

1. Julia im Workspace suchen;
2. vorhandene Julia eindeutig identifizieren oder neu anlegen;
3. Prompt 01 an den ElevenLabs Architect geben;
4. Ergebnis/Readback pruefen;
5. erst dann Prompt 02;
6. danach 03, 04 und 05;
7. Final Readback erzeugen;
8. Receipt ausgeben.

Du musst die einzelnen ElevenLabs-Prompts nicht selbst kopieren, solange Claude den Browser bedienen kann.

## Schritt A4 — Nur wenn Claude stoppt

Du musst nur eingreifen bei:

- Login/OAuth;
- Workspace-Auswahl;
- einer echten ElevenLabs-Bestaetigung;
- einer Funktion, die dein Account nicht anbietet;
- `BLOCKED_UNEXPECTED_DIFF`.

Nicht selbst spontan Einstellungen korrigieren. Gib Claude die Fehlermeldung und lasse es gegen das Repository pruefen.

---

# Weg B — Codex vollautomatisiert

Bevorzugter Codex-Weg: Repository lokal + ElevenLabs CLI/OAuth. Dadurch muss Codex nicht jeden Dashboard-Klick nachbilden.

## Schritt B1 — ElevenLabs CLI installieren

Im Terminal:

```bash
npm i -g @elevenlabs/cli
```

## Schritt B2 — ElevenLabs per OAuth anmelden

```bash
elevenlabs auth login
```

Der Browser oeffnet die Anmeldung. Melde dich in dem Ziel-Workspace an und bestaetige die Verbindung.

## Schritt B3 — Offizielle ElevenLabs Agent-Skills installieren

```bash
npx skills add elevenlabs/skills --skill agents
```

Wenn diese Funktion in deiner Codex-Umgebung nicht verfuegbar ist, darf Codex stattdessen ElevenLabs Browser Use oder die vorhandene ElevenLabs API/CLI nutzen. Es darf keine Zugangsdaten erfinden.

## Schritt B4 — Codex im Repository starten

Starte Codex im Ordner `pxk-11agents` und gib nur:

> Lies `COLLEAGUE_QUICKSTART.md`, `GPT_START_HERE.md` und `AGENTS.md`. Provisioniere `julia` im Modus `candidate-safe` vollstaendig in meinem authentifizierten ElevenLabs-Workspace. Das Repository ist die Source of Truth. Arbeite die Julia-Schritte 01 bis 05 strikt sequenziell ab, nutze ElevenLabs CLI/API/Agents-Skill oder Browser Use, je nachdem was in dieser Umgebung real verfuegbar ist. Nach jeder Mutation Readback und Soll/Ist-Vergleich. Keine Live Calls. Keine Secrets speichern. Stoppe bei unerwartetem Diff. Am Ende Verification-Status und Receipt erzeugen.

## Schritt B5

Codex soll danach ohne weitere Designfragen arbeiten.

Der normale Ablauf lautet:

`DISCOVER -> CREATE/REUSE -> CORE CONFIG -> CONTEXT/CONTRACT -> EVALS/GUARDRAILS -> FINAL VERIFY -> RECEIPT`

Wenn Codex nach Architekturentscheidungen fragt, obwohl sie im Repository beantwortet sind, verweise es auf `GPT_START_HERE.md` und `agents/julia/`.

---

# Wann ist Julia erfolgreich angelegt?

Erfolg ist erst erreicht, wenn Step 05 einen Provider-Readback liefert.

Fuer einen internen Gespraechstest ist der Zielstatus:

`READY_FOR_INTERNAL_CONVERSATION_TEST`

Dafuer muessen mindestens gelten:

- `candidate-safe` ist wirklich im Zielaccount provisioniert;
- First Message und System Prompt stimmen mit dem Repo ueberein;
- Voice/LLM/ASR/Turn Settings sind verifiziert;
- v1.3 Contract-Surface ist erhalten;
- Knowledge/RAG ist verifiziert oder sauber als `SOURCE_NEEDED` markiert;
- Guardrails sind gesetzt;
- P0 Regressionstests sind angelegt/ausgefuehrt oder explizit als manuelle Testfaelle dokumentiert;
- keine unerwarteten Diffs sind offen.

`READY_FOR_INTERNAL_CONVERSATION_TEST` bedeutet NICHT Live-Outbound-Freigabe.

---

# Was die Automatisierung niemals tun darf

- Live-Batch-Calls starten;
- Secrets oder API-Keys in Git/Prompts/Receipts schreiben;
- eine zufaellige Julia nur nach Namen ueberschreiben;
- mehrere Provisioning-Schritte ohne Readback bulk-aendern;
- CRM-/Calendar-/MCP-Funktionen als aktiv behaupten, wenn sie nicht verifiziert sind;
- `CONFIGURED_VERIFIED` oder Test-PASS erfinden.

---

# Wenn du nur Copy/Paste benutzen willst

Falls dein Assistent ElevenLabs nicht selbst bedienen kann:

1. sage `Lege Julia an`;
2. er gibt nur `agents/julia/prompts/01-discover-and-create.md` aus;
3. kopiere diesen Prompt in den ElevenLabs Architect;
4. kopiere dessen Antwort zurueck;
5. der Assistent prueft sie und gibt erst dann Prompt 02 aus;
6. so weiter bis Prompt 05.

Auch dieser Weg verwendet exakt dieselbe Soll-Konfiguration.
