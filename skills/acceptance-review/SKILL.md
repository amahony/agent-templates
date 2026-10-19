---
name: acceptance-review
description: Check finished sprint work against the sprint's acceptance criteria and give every criterion a verdict backed by evidence, then an overall PASS, PARTIAL or FAIL with actionable failures. Use when a sprint or wave is reported done, before tasks are marked complete, or when someone asks "is this sprint actually done", "review this against the criteria" or "verify the sprint". Works for code and non-code work. A worker's own claim of completion never counts as evidence.
license: MIT
compatibility: Uses library_search and library_read to read the phase file, the deliverables and the worker's report. Uses connected integrations, such as a code host, when they hold the evidence.
metadata:
  version: "1.0.0"
  author: Jeremy Kaye
  category: Review
  source: https://github.com/AyeJK/phase-runner/tree/main/plugin/skills/phase-verify
---

# Acceptance review

Decides whether a sprint is done. A **sprint** is a bundle of tasks one worker can finish and that can be checked on its own; it is not a period of time. Its acceptance criteria and Verification section in the phase file are the only standard. The reviewer did not assign or do the work, which is what makes the check independent.

## Inputs

1. The sprint's section in the phase file (`Phase-{N}-{Name}.md`): Goal, Tasks with their Module and Reference cells, Acceptance Criteria and Verification. Read it with library_read; never work from memory.
2. The worker's result: what it says it completed, blocked or left as manual.
3. The deliverables: library files, documents, links, screenshots or commits the result points to, and the Reference documents the tasks follow, such as screen specs.

If a deliverable the result names cannot be found, that is a finding, not a reason to assume it exists.

## Step 1: A verdict for every criterion

For every acceptance criterion and every `assert:` line:

| Verdict | Requires |
|---------|----------|
| `MET` | Concrete evidence: the passage in the deliverable, the file and line in the code, the passing check, or the signed document. Cite it |
| `NOT_MET` | Concrete evidence that it is not met: the thing is missing, contradicts the criterion, or the check fails. Cite it |
| `UNVERIFIED` | Cannot be decided from what you can read, for example it needs a browser, a live service, real data or a person's confirmation. Say what would decide it |

- No evidence means `UNVERIFIED`, never `MET`. "Done" in the worker's result is a claim, not evidence.
- A suspicion without a citation means `UNVERIFIED`, never `NOT_MET`. A false failure costs a full redo.
- A criterion only a `MANUAL` task can meet is `UNVERIFIED (manual)`, never `NOT_MET`.
- Judge the criterion as written. Do not raise the bar, and do not lower it because the work looks good.

## Step 2: Integrity

Flag anything that makes a criterion look met without meeting it:

- **Code:** tests deleted, commented out or skipped; assertions loosened or expected values changed to match new output; coverage thresholds lowered. A change a task explicitly asked for is `EXPECTED`, with the task number.
- **Documents and other work:** placeholder text left in, figures without a source, a criterion's wording copied into the deliverable instead of being satisfied, or a "final" file that is a draft.

## Step 3: Scope

A sprint's scope is the Module cells of its tasks. Note work done outside them, naming the nearest sprint. Scope findings are notes, except these, which block:

- The worker edited the phase file. Workers never change it; only the coordinator applies results.
- Deleted files, changed deployment or security configuration, or a secret written into a deliverable.

If the sprint has no Module cells, report scope as not declared and treat every scope finding as a note.

## Step 4: Overall result

- **FAIL** when any criterion is `NOT_MET`, any integrity flag is not `EXPECTED`, or a blocking scope finding exists.
- **PARTIAL** when nothing blocks but some criteria are `UNVERIFIED` or there are non-blocking notes.
- **PASS** when every criterion is `MET` and nothing is flagged.

Write each blocking finding as one actionable line starting with the sprint id, so it can go straight back to the worker:

```
2.3: criterion "Expired links show an error" NOT_MET — src/auth/link.ts:40 returns before checking expiry
2.4: criterion "Venue contract signed" NOT_MET — venue-contract.md is the unsigned draft from 12 May
```

## Result block

End the review with this block, exactly:

```
REVIEW RESULT:
STATUS: PASS | PARTIAL | FAIL
CRITERIA:
- {sprint id} | "{criterion}" | MET | NOT_MET | UNVERIFIED | {evidence, or what would decide it}
INTEGRITY: CLEAN | FLAGGED
- {flags and EXPECTED changes; omit lines when CLEAN}
SCOPE: CLEAN | FLAGGED | NOT_DECLARED
- {item → nearest sprint, blocking or note; omit lines when CLEAN}
FAILURES:
- {actionable lines, or NONE}
NEEDS A PERSON:
- {UNVERIFIED criteria and what would decide each, or NONE}
```

## What not to do

- Do not fix the work. Report it; the worker fixes it.
- Do not change the phase file or mark tasks done.
- Do not review against anything except the written criteria and the Reference documents.
- Do not give a verdict on a criterion you did not check. Say it was not checked.
