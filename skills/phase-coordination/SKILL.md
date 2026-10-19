---
name: phase-coordination
description: Run a phase from its phase file, sprint by sprint, grouping independent sprints into parallel waves, giving each sprint to its own thread, sending finished work to an independent reviewer, applying the results and stopping at blockers and at the end of the phase. Use when someone says "run phase 2", "start the next sprint", "continue the phase", "what's the status" or "hand this to Claude Code". For code projects it hands the phase files to Phase Runner in Claude Code or Auggie instead of building in the chat.
license: MIT
compatibility: Uses library_search, library_read and library_write for phase files, and spawn_thread to give each sprint its own thread. Needs a reviewer in the chat, such as Phase Reviewer, for an independent check.
metadata:
  version: "1.0.0"
  author: Jeremy Kaye
  category: Planning
  source: https://github.com/AyeJK/phase-runner/tree/main/plugin/skills/phase-builder
---

# Phase coordination

The coordinator runs the phase; it does not do the sprints' work itself and does not judge it. A **phase** is a stage of the work with a goal and a finish line. A **sprint** is a bundle of tasks one worker can finish and that can be checked on its own. It is not a period of time. A **wave** is a set of sprints that run at the same time.

## Step 1: Read the phase file

Find `Phase-{N}-{Name}.md` with library_search and read it with library_read. Never run from memory. List the sprints that still have tasks at `—`, `~` or `BLOCKED`. A sprint whose remaining tasks are all `MANUAL` is not run; its tasks go on the checkpoint's manual list.

If no phase file exists, say so and offer to create one with the phase-planning skill.

## Step 2: Code or not

**Code projects are built outside the chat.** When the sprints change a codebase, tell the person to put the plan in the repository (phase files in `docs/phases/`, design files in `docs/design/`, the product plan in `docs/`) and run `run phase {N}` with Phase Runner's `phase-builder` in Claude Code or Auggie (https://github.com/AyeJK/phase-runner). Offer to keep the phase file here up to date from the results they paste back, and to have the reviewer check a sprint against its criteria. Do not try to build code in a thread.

**Other work runs here**: research, writing, planning, outreach drafts, event logistics, anything the threads can do with the library and the tools the chat has.

## Step 3: Group into waves

Build the order from each sprint's Dependencies section and the phase's Sequencing note.

- Sprints with no dependency on each other and no overlapping Module cells may share a wave.
- When in doubt, run them one after another. Sequential is the default.
- At most four sprints per wave.

Before starting, show the plan in one short block: the waves, the sprints in each, and what will be checked. Start only when the person confirms.

## Step 4: Run a wave

For each sprint in the wave, open one thread with spawn_thread, all in the same turn:

- **title:** `Sprint {X.Y} — {title}`, with `(retry {n})` on a retry.
- **contextMode:** `none`. The brief carries everything.
- **brief:** the phase's goal and decision notes, then this sprint's whole section copied from the phase file (Goal, Tasks, Acceptance Criteria, Dependencies, Verification), the names of the Reference documents to read, any failures from an earlier review to fix, and the worker rules below.

Worker rules, copied into every brief:

```
Do every task at —, ~ or BLOCKED. Never do a MANUAL task.
Save deliverables to the library and name each file in your report.
If a task needs something only a person can give (a credential, a decision, a payment), mark it BLOCKED and say why. Do not guess.
If a task is one only a person can do, list it under MANUAL and say exactly what they must do.
Do not edit the phase file.
When done, call report_to_parent once, ending with:
SPRINT RESULT:
COMPLETED: [task numbers, or NONE]
BLOCKED: [task numbers, or NONE]
BLOCKED_REASONS: [one line per blocked task: "Task N: reason"]
MANUAL: [task numbers, or NONE]
DELIVERABLES: [file names or links]
NOTES: [decisions made, warnings, what the next sprint should know]
```

Never start the next wave in the same turn as this wave's review.

## Step 5: Review

When every thread in the wave has reported, read each report. A report with no `SPRINT RESULT` block goes back to its thread's work as a retry before any review.

Then ask the reviewer in this chat, by its handle, to run an acceptance review of the wave's sprints, naming the phase file and each sprint's deliverables. Do not review the work yourself: the person who assigned the work cannot check it independently. If no reviewer is in the chat, say so, list the criteria for the person to check, and mark nothing done until they confirm.

- **PASS:** apply the results.
- **PARTIAL:** apply the results, and carry the criteria marked `NEEDS A PERSON` to the checkpoint.
- **FAIL:** send the `FAILURES` lines back as a retry of that sprint only. After two failed retries, stop and ask the person.

## Step 6: Apply results

Update the phase file with the phase-planning skill, in sprint order, in one save: completed tasks that passed review to `x`, blocked tasks to `BLOCKED`, person-only tasks to `MANUAL`. Then show the status board.

**Blockers stop the run.** If any task is `BLOCKED`, stop before the next wave and list each blocked task with its sprint and reason. Offer: resolve it and rerun the sprint; skip it as `DEFERRED`, `CUT` or `MANUAL`; or stop here. Wait for the answer. `MANUAL` tasks never stop the run.

## Status board

After every wave, and whenever someone asks for status, show:

- Phase {N} — {title}, and "Wave {n} of {total}".
- One row per sprint: id, title, done over eligible tasks, and its state (waiting, running, in review, done, blocked).
- Blocked tasks with their reasons, and manual tasks with who must do them.

Build it from the phase file as saved, never from memory. Eligible tasks exclude `CUT` and `DEFERRED`.

## Step 7: Phase checkpoint

When every sprint in the phase is done, or the person's request is met, always stop. Never start the next phase on your own.

Re-read the phase file, then report: sprints run with their exact titles and task counts; anything still blocked; the manual list (`☐ {sprint} #{n} — {task} — what the person must do`); criteria that need a person's check; and what comes next, with the next phase's first sprint goal. Ask whether to begin the next phase.
