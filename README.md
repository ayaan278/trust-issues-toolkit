# Trust Issues Toolkit

Rules files, loop templates and a review skill for working with AI coding agents.

Copy them. Fill in the brackets. Delete what doesn't apply.

**The idea:** don't trust the generated code. Trust the verification.

## Who it's for

Anyone shipping code with an AI agent — and opening files in their own repo they didn't write.

If you can read a diff, you're qualified. No tool lock-in: plain markdown, meant to be adapted to whatever your agent reads.

## Quick start

1. **Rules first.** Copy [`rules/`](rules/) to wherever your agent loads always-on rules. Replace every `[bracket]` — anything still in brackets is a lie your agent will confidently act on. Delete every line that doesn't apply. Keep each file under ~40 lines.
2. **Run one bounded loop.** Pick a small, annoying, real bug. Fill in [`prompts/loop-template.md`](prompts/loop-template.md): exit condition, feedback, boundaries, budget. Then walk away.
3. **Turn repeat corrections into skills.** Corrected the agent the same way three times? That's a skill. Start from [`skills/skill-template/`](skills/skill-template/SKILL.md).
4. **Add the reviewer.** [`skills/branch-review/`](skills/branch-review/SKILL.md) reads every diff before you do. Cap it at three fix cycles.
5. **Pipeline last.** Only when 1–4 work: [`prompts/pipeline-template.md`](prompts/pipeline-template.md).

## What's inside

| # | File | What it is |
|---|---|---|
| A.1 | [`rules/project-rules.md`](rules/project-rules.md) | What this codebase is: stack, layout, where things live, what not to touch. |
| A.2 | [`rules/code-rules.md`](rules/code-rules.md) | How you write here. Where "tutorial code" goes to die. |
| A.3 | [`rules/test-rules.md`](rules/test-rules.md) | What "verified" means. If you copy one file, make it this one. |
| A.4 | [`prompts/loop-template.md`](prompts/loop-template.md) | Hand the agent an outcome, not a task — plus two filled examples and attempt budgets. |
| A.5 | [`skills/skill-template/SKILL.md`](skills/skill-template/SKILL.md) | Blank skill: goal, scope, playbook, output format, anti-patterns. |
| A.6 | [`skills/branch-review/SKILL.md`](skills/branch-review/SKILL.md) | Reviews your branch's diff against `main` before you do. Catches the cheap mistakes. |
| A.7 | [`prompts/pipeline-template.md`](prompts/pipeline-template.md) | Ticket → tests → review → draft PR → CI watch, with checkpoints. Build it last. |

More notes on using each folder: [`rules/README.md`](rules/README.md) · [`skills/README.md`](skills/README.md)

## One warning

These files shape *behaviour*. They do not *bound* it. Permissions do that — read-only access, branch protection, a human running migrations, deploy staying a human verb. If a rules file and a permission ever disagree, only one of them holds.

## Make them yours

Nothing here is clever — that's the point. Six months from now yours should look nothing like these. Every time you correct the agent twice, that correction belongs in a file.

Got a better rule, or a template that misfired? See [CONTRIBUTING.md](CONTRIBUTING.md).

---

These templates are the appendix of the book ***Trust Issues: Working With Code You Didn't Write*** by Ayaan Ahmad. The stories behind each file are in there. Free sample: [Chapter 2 — The 67/68 Problem](https://ayaan278.github.io/trust-issues-toolkit/chapter-2.html) · Book: [Kindle](https://www.amazon.com/dp/B0HD7D3DQ9) · [Paperback](https://www.amazon.com/dp/B0HL5DK2K6)

## Licence

Templates and site code: [MIT](LICENSE). Use them anywhere, including at work. Change whatever you like.

Exception: the Chapter 2 excerpt (`docs/chapter-2.*`) and the images in `docs/img/` are © 2026 Ayaan Ahmad, all rights reserved, and are **not** covered by the MIT licence.
