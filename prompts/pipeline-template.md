# Pipeline Template

*Only build this after the rest exist and work. A pipeline built on a vague rules file is just chaos with scheduling.*

Copy the block, fill every `[bracket]`, hand it to your agent.

```text
Implement [TICKET-ID] on a new branch.

1. Fetch the ticket description and acceptance criteria from [tracker]. Treat the acceptance criteria as the definition of done.

2. Implement the changes following the project, code, and test rules. Write tests as specified in test-rules.

3. Run the full test suite. Fix and re-run as needed — but never modify an existing test to pass.

4. Run [review skill] over the diff. Max [3] fix cycles, then report what's left.

5. Push the branch and open a DRAFT PR referencing the ticket.

6. Then watch until it merges. Every [10] minutes, check CI status and any new reviewer comments:
   - CI still running: do nothing, wait for the next tick
   - CI failed: fix, push, re-arm on the new run, max [3] attempts then stop and report
   - New review comments: address the must-fix ones, push, re-arm CI
   - Merged: stop the loop, move the ticket, message me
   - Outside working hours: stop and pick up in the morning

Message me at every checkpoint: what you decided, what changed, anything you need clarified. Short lines, not walls of logs.
```

## Notes

**What to checkpoint on:** anything irreversible, anything touching tests, dependencies or configuration, any change of plan, and the end of each stage. Not every file edit or passing test.

The reason to separate "what I decided" from "here's the result" is that decisions are where the expensive mistakes live. A summary at the end gets skimmed. A decision on its own line gets read.

That last stop condition — clocking off — matters more than it looks. You are the escalation path for this pipeline. An agent grinding away at 2 a.m. with nobody to escalate to isn't autonomy; it's an unsupervised process with commit access.

**And where it stops:** deploy is a human verb. This pipeline ends at "PR ready for review." The last click is yours. Always.
