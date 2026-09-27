# Test Rules

## Commands
- Tests: [your exact command]
- Run the full suite before opening a PR. Never push without running tests.

## What needs tests
- Every new entry point: happy path + auth failure + bad input
- Every bug fix: a regression test that FAILS without the fix. Reproduce first, then fix — never the other way around.
- [Anything touching money, permissions, or user data: no exceptions]

## Hard lines

When a test fails, first decide whether the test or the code is wrong — then say which, and why, before changing either. The default assumption is that the code is wrong. This one sentence is the difference between a fix and a cover-up.

NEVER modify an existing test to make it pass. Weakening an assertion, loosening a matcher, deleting a case, or marking it skipped requires explicit human approval. Say what you want to change and stop.

Tests must assert real behaviour. A test that runs without asserting anything meaningful is worse than no test, because it buys false confidence.

No sleep() as a fix for race conditions. A timing bug that a sleep hides is a timing bug that comes back under load. Fix the ordering, not the clock.

## Data
- Use [factories / fixtures]
- Never hit real external services — mock at the service boundary
- Never use production data in tests

## Verification I expect to see
When you finish, don't tell me it works — show me. Run it against the real cases (happy path, empty input, garbage input, [your weird edge case]) and paste the actual output. Descriptions can hallucinate. Logs can't.
