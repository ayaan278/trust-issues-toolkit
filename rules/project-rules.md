# Project Rules

## What this product does
[One or two sentences in plain language. Who uses it, what it does for them. Agents write better code when they know what the code is FOR — this line is not decoration.]

## Stack and layout
- Backend: [framework] in [/backend]
- Frontend: [framework] in [/frontend]
- Database: [engine]
- Shared logic lives in [core] — if something is useful in more than one place, it goes there. Do not re-implement the same helper twice.
- Match the structure already used in existing modules: same naming style, same organisation, same file layout.

## Designated homes
Every kind of thing has one place it belongs. Don't invent new locations.

| Kind of thing | Goes in |
|---|---|
| [Custom model managers] | [managers.py] |
| [Serializers / schemas] | [serializers.py] |
| [Test factories] | [factories.py] |
| [Cross-model orchestration, external I/O] | [services/] |
| [Anything reusable across apps] | [core/] |

Avoid creating new files unless justified by real reuse, size, or an existing convention.

## Do not touch
- [migrations/] — see the migration rules below
- [legacy_module/] — scheduled for rewrite, do not invest effort here
- [infra/] — ask before changing anything here
- Anything outside the module named in the current task

## Running things
- All commands run through [your toolchain], never directly on the host.
- Tests: [your exact command]
- Lint/format: [your exact command]
- Do it yourself, don't hand me instructions. If a change needs a worker reload, a container restart, or a rebuild to take effect, perform it and verify the service is healthy before you finish.

## Migrations / schema changes
- Once a migration is merged to [main], it is never edited or deleted. Changes go in a new migration.
- If your branch creates two or more migrations for one app, merge them into a single file manually. Do not use automated squashing.
- Never apply migrations to a live database yourself — write it, a human runs it.

## Scope discipline
- Implement only what the task asks. If something adjacent looks broken, say so and stop. Do not fix it uninvited.
- Do not create markdown files unless I ask for one. No SUMMARY.md, no NOTES.md littering the repo. Summaries go in the chat.
