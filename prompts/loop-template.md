# Loop Template

*A prompt asks for code. A loop asks for an outcome.*

Every working loop has four parts: an exit condition the machine can check, feedback it can actually read, boundaries on what it may touch, and a budget so a stuck loop escalates to you instead of grinding forever.

Copy the block, fill every `[bracket]`, hand it to your agent.

## Template

```text
GOAL: [one sentence, stated as an outcome — not a task]

VERIFY WITH: [exact command that proves it]
  (must print something unambiguous — a status code, a pass/fail, an exit code)

RULES:
- After every change, run the verify command and read the FULL output
- Change ONE thing per attempt
- Keep a running log in attempts.md: what changed, what came back
- Commit after every attempt with a one-line message
- Do NOT touch anything outside [module/directory]

STOP WHEN: [verify command succeeds], or after [N] attempts — then summarise the log and hand back to me.
```

## Filled example — a stubborn integration

```text
GOAL: POST /v1/transactions on [provider] must return 200.

VERIFY WITH: ./scripts/test_api_call.sh
  (sends one request, prints status code + full response body)

RULES:
- After every change, run the verify script and read the FULL response
- Change ONE thing per attempt (auth header, payload field, encoding, endpoint version)
- Keep a running log in attempts.md: what changed, what came back
- Commit after every attempt with a one-line message
- Do NOT touch anything outside the api_client module

STOP WHEN: script prints 200, or after 25 attempts — then summarise the log and hand back to me.
```

## Filled example — a bug with an unknown cause

```text
GOAL: the [X] reported in [ticket] can no longer happen.

STEP 1 — REPRODUCE FIRST. Before changing any code, write a test or script that fails the same way users are failing. Do not propose a fix until the bug happens on demand. If you can't reproduce it, tell me what evidence you're missing.

STEP 2 — VERIFY WITH: [the reproduction you just wrote]

STEP 3 — Make the SMALLEST change that turns the reproduction green. Not a redesign. If you think a redesign is needed, stop and say so.

STEP 4 — Promote the reproduction into the permanent test suite, plus any sibling cases where the same kind of failure could hide.

RULES:
- Evidence over theory: work from [logs/traces/payloads], not my guess
- One change per attempt, logged
- No sleep() or timing hacks as a fix for ordering problems

STOP WHEN: reproduction passes and is committed as a permanent test, or after 15 attempts — then summarise what you learned.
```

## Budgets — rough starting points

| Kind of loop | Attempt budget |
|---|---|
| Known bug, clear exit condition | 10–15 |
| Unknown cause, needs reproduction | 15–20 |
| Integration nobody has ever made work | 25 |
| Anything touching money or auth | Don't loop it. See Chapter 4. |

## What `attempts.md` ends up looking like

From Chapter 2 — the log from the stubborn-integration loop above:

```text
#11  auth header: Bearer -> Token          -> 401
#12  payload: amount as string             -> 422
#13  endpoint: /v2/ -> /v1/                -> 404
#14  content-type: added charset=utf-8     -> 200 OK
```

Four lines, zero mystery. The answer to “which one worked?” is right there — permanently, boringly, in writing.
