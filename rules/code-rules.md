# Code Rules

## The overriding rule
Match the code that's already there. Naming, structure, patterns, file layout — follow the nearest existing example, not the framework's tutorial and not general best practice. If the repo does something unusual consistently, that's a decision, not an accident.

## Style
- [Formatter and linter]
- [Type hints required on new functions]
- Naming: [convention]. No abbreviations — `user_count`, not `usr_cnt`.
- Imports go at the top of the file. If one must be moved lower to break a circular import, leave a one-line comment saying why.

## Patterns
- All external calls (APIs, cloud services, third parties) go through a service layer. Views and components never call external systems directly.
- Errors: raise domain exceptions, handle them at the boundary. No silent `try/except: pass`. Ever.
- Prefer explicit over magic. [Put deletion behaviour in an explicit method override rather than an event hook nobody can find.]
- [Your one pattern nobody ever guesses right.]

## DRY, with actual thresholds
- Extract shared logic only when the same semantic operation appears twice or more with the same pre- and post-conditions, or when one helper removes real bug risk.
- Do not create a helper because two lines look similar. If the behaviours diverge on edge cases, they are not the same operation.
- Do not create a "utils" file without a second real consumer.
- Prefer clarity over cleverness. Collapsing branches is good only while it stays obvious — don't hurt grepability to save a line.

## Libraries
- Use: [list yours]
- Banned: [library] — use [alternative], because [reason]. Give the reason. It lets the agent generalise instead of memorising.

## Quality checks
- Run [lint command] before finishing.
- Fix warnings; never disable the rule. Silencing a linter, adding an ignore comment, or loosening config to make output green is not a fix.

## Naming and structure preferences
[Write yours here. If it isn't in this file, your edits are just noise.]
