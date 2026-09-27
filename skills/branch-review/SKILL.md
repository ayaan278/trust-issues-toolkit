---
name: [stack]-branch-review
description: Reviews git diffs against main for [stack] quality — dead code, sensible DRY, correct placement of logic, [performance risk], and small simplifications, while matching this repo's existing structure. Skips tests and translation files.
---

# [Stack] branch review (diff vs main)

## Goal
Improve quality and maintainability of the changes relative to `main`, without fighting the repo's existing patterns. Prefer small, high-signal edits over churn.

## Scope
1. Diff source: compare the current branch to `main`.
2. Paths: only under [project root].
3. Exclude unless I explicitly ask:
   - Test code: [patterns]
   - Translations / generated files: [patterns]
4. Include everything else in scope.

## What to look for, in order

### 1. Dead code and unnecessary surface
- Unused imports, unreachable branches, obsolete flags
- Functions referenced only by removed code paths
- Over-abstraction: thin wrappers that add no clarity

Do not flag "might be used later" unless it's clearly orphaned.

### 2. Right place for the logic

| Concern | Prefer |
|---|---|
| Persistence rules, invariants | Model or custom manager |
| Cross-model orchestration, external I/O | Service module |
| Request/response shape, contract validation | Serializer / schema |
| Small predicates used across apps | [core] helper, if real reuse |

### 3. DRY, with thresholds
- Extract only when the same semantic operation appears twice or more with the same pre- and post-conditions
- Do not create a helper because two lines look similar
- Do not create new files unless justified

### 4. Performance and data access
- [N+1 queries: loops touching related fields without prefetching]
- Heavy work in [serializers or views] that belongs in a single query
- Only flag with evidence in the diff

### 5. Readability without cleverness
- Collapse repetitive branches only while it stays obvious
- Prefer clarity over golf

## Output format
Return findings in the chat. Do not create files.

1. Summary — a few bullets: overall risk and themes
2. File-ordered notes — path → issue → suggested fix
3. Severity — Blocker / Should fix / Nice to have
4. If nothing material: say so explicitly.

## Workflow
1. List changed in-scope files vs `main`; apply exclusions
2. Read the hunk context plus callers and callees where needed — not the whole repo blindly
3. Cross-check proposed moves against [circular imports] and module boundaries
4. If proposing a behaviour change, state how to verify it

## Anti-patterns — do not suggest
- New files for one-off helpers
- "Utils" dumping grounds with no second consumer
- Broad refactors unrelated to this diff
- Moving domain rules into [serializers] just to shorten a [view]
