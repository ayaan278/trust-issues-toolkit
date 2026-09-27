# Rules

Always-on instructions your agent reads before doing anything. Three small files, not one big one.

| File | What it is |
|---|---|
| [`project-rules.md`](project-rules.md) | What this codebase IS. The agent reads this before doing anything. |
| [`code-rules.md`](code-rules.md) | How we write here. This is where "tutorial code" goes to die. |
| [`test-rules.md`](test-rules.md) | What "verified" means here. If you copy one file from this repo, make it this one. |

**How to use them.** Start with the three rules files and delete every line that doesn't apply; a short honest file beats a long aspirational one. Replace every `[bracket]` — anything still in brackets is a lie your agent will confidently act on. Keep each rules file under about forty lines, because they rot when they become dumps. Then grow them from your own scar tissue: every time you correct the agent twice, that correction belongs in here.

**One warning before you start.** These files shape *behaviour*. They do not *bound* it. Permissions do that — read-only access, branch protection, a human running migrations, deploy staying a human verb. If a rules file and a permission ever disagree, only one of them holds.

**Where they go.** Wherever your tool loads always-on rules from. If it wants frontmatter, add it — for example:

```yaml
---
alwaysApply: true
---
```

**Filling in `code-rules.md`.** The fastest way to fill this in: open your last five code reviews and copy out every comment you left. That was your style guide the whole time.
