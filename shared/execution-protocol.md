# Execution Protocol

## Modes

### candidate-safe
Default fuer neue Accounts. Reproduziert Julias gewuenschte Conversation-DNA und Providerparameter, repariert aber bekannte Baseline-Defekte.

### replica-current
Nur fuer historische Vergleichstests. Ziel ist moeglichst genaue Reproduktion des dokumentierten Provider-Snapshots vom 01.09.2026. Bekannte Defekte bleiben als Reproduktionsmerkmal erhalten und duerfen nicht als Produktziel interpretiert werden.

## Sequence

1. Discover workspace + resolve/create agent.
2. Apply core model/voice/conversation configuration.
3. Apply system prompt, variables and knowledge configuration.
4. Configure guardrails/evals/tests that are supported in the account.
5. Final readback and receipt.

## State Machine

`NOT_STARTED -> DISCOVERED -> CORE_CONFIGURED -> CONTEXT_CONFIGURED -> EVAL_CONFIGURED -> VERIFIED`

Any unexpected diff or capability blocker transitions to `BLOCKED`.

## Browser Operation

If the executing AI controls a logged-in browser:

- prefer the ElevenLabs Architect/AI interface or official account UI;
- paste exactly one repository prompt at a time;
- wait for the Architect result;
- compare result with expected output;
- proceed only on PASS/PARTIAL-without-diff.

If no browser control is available, output only the next prompt in a copy-ready block and the expected evidence to paste back.

## Idempotency

All prompts must be safe to rerun:

- search/resolve before create;
- compare before patch;
- never duplicate KB bindings, tools or tests when equivalent resources already exist;
- report `NO_CHANGE_REQUIRED` when target state already matches.
