# Skills

*A rule says "always do X." A skill says "when asked to do job Y, here's the whole playbook."* Skills load on demand, so they can be far deeper than a rule without drowning the agent in context it doesn't need yet.

How to know you need one: you've corrected the agent the same way three times. Your frustration is the curriculum.

| Skill | What it is |
|---|---|
| [`skill-template/`](skill-template/SKILL.md) | A blank skill with the sections that matter: goal, scope, playbook, output format, anti-patterns. |
| [`branch-review/`](branch-review/SKILL.md) | Reviews your branch's diff against `main` before you do. Catches the cheap mistakes so your attention is spent only on the expensive ones. |

Each skill is a folder with a `SKILL.md`. Name the folder after its `name:` line, then drop it wherever your tool loads skills from.

**Three notes on writing good skills.** The `description` line is the whole game — it's what the tool matches against to decide whether to load this skill, so a vague one means the skill either never fires or fires constantly. Anti-patterns sections punch above their weight, because the failure mode isn't ignorance, it's confident over-reach. And give it permission to find nothing: any skill that asks the agent to evaluate something needs an explicit "if it's fine, say it's fine," or an agent asked to find problems will find problems.

**Cap the fix cycles.** However you wire this in, bound it — mine gets three passes, then it reports what's left. An uncapped reviewer-fixer pair will happily refactor each other's work until you run out of patience or tokens.
