---
name: phase-planning
description: Create and maintain phase files, the plans that break work into phases, sprints and tasks with a status for every task. Use when turning a product plan, design files or a conversation into a phase plan, or when adding, removing, editing, moving or changing the status of tasks, adding sprints, or reporting progress on a sprint or phase. Works for software and for non-code projects; the format is Phase Runner's, so a code project can be built in Claude Code or Auggie.
license: MIT
compatibility: Uses library_search and library_read to find plans and phase files, and library_write to save them.
metadata:
  version: "1.0.0"
  author: Jeremy Kaye
  category: Planning
  source: https://github.com/AyeJK/phase-runner/tree/main/plugin/skills/phase-planner
---

# Phase planning

A phase file is the plan everyone works from. A **phase** is a stage of the work with a goal and a finish line. A **sprint** is a bundle of tasks one worker can finish and that can be checked on its own. It is not a period of time, and sprints never get dates; a phase may have a target date when the person gives one. A **task** is one row in a sprint's table.

The full template and edge cases are in [references/format.md](references/format.md).

## Where phase files live

One file per phase, saved with library_write as `Phase-{N}-{Name}.md`, numbered from 1. For a code project, tell the person the files belong in the repository at `docs/phases/`, where Phase Runner's `phase-builder` reads them. Always read a phase file with library_read before changing it.

## Task table

```
| Status | # | Task | Module | Reference |
|--------|---|------|--------|-----------|
| — | 1 | Add the notifications table | db/migrations/ | Plan-Notifications-2026-05-22.md |
| ~ | 2 | Build the settings toggle | src/settings/ |
| x | 3 | Agree the launch date with marketing |
| MANUAL | 4 | Publish the package to the registry |
```

The header always lists all five columns. A row leaves off trailing cells that do not apply instead of filling them with `—`. **Module** is where the work happens: a folder for code, a team or channel for other work. **Reference** is the document the task follows, such as a screen spec.

| Status | Meaning |
|--------|---------|
| `—` | Not started |
| `~` | In progress |
| `x` | Done and checked |
| `BLOCKED` | Agent work that is stuck on a dependency, credential or decision |
| `MANUAL` | Only a person can do it: publish, sign, call, record, buy |
| `CUT` | Removed from scope; the row stays as history |
| `DEFERRED` | Moved to a later sprint or phase |

`BLOCKED` goes back to a worker once unblocked. `MANUAL` never goes to a worker; the person marks it `x` when done.

## Create a phase

1. Read the inputs: the product plan, design files (`DESIGN.md`, `screen-*.md`) and any decisions in the library or chat.
2. Find existing phase files with library_search. The new phase takes the next number, or 1.
3. Write the file from the template: the phase goal, then sprints, each with Goal, Tasks, Acceptance Criteria, Dependencies and Verification. Risk Mitigations and Scope Guard go after the last sprint, never between sprints.
4. Every task starts at `—`, except one only a person can do, which starts at `MANUAL`.
5. Show the sprint list and ask the person to confirm before any work starts. Save only after they confirm, or when they asked for the file.

Never overwrite an existing phase file. If the number is taken, use the next one or ask.

### Sizing sprints

- One worker can finish a sprint in one sitting, and its acceptance criteria can be checked without the next sprint existing.
- Three to eight tasks per sprint. Split a sprint whose tasks touch unrelated areas.
- State dependencies honestly. Sprints with no dependency on each other and no overlapping Module cells can run in parallel as a **wave**; say which ones in the phase's sequencing notes.
- Acceptance criteria are observable outcomes, not restated tasks.
- When design files exist: an interface task's Reference cell names its screen spec, task text says "implement per screen spec", and the sprint's `assert:` lines come from the spec's acceptance bullets.

### Verification

Every new sprint ends with a Verification section:

```markdown
### Verification

- cli: npm run check
- ui: /settings/profile
- assert: Profile form saves without a full reload
- assert: Validation errors appear inline
```

`cli:` is the command that must pass, for code projects only. `ui:` lists the routes to check when the sprint changes an interface. A sprint with no interface gets `skip-ui: true`. `assert:` lines say what passing means, one observable outcome each; for non-code work they are the whole check, such as "The venue contract is signed and in the library". Status changes never edit this section.

## Change a phase file

| Operation | Rule |
|-----------|------|
| Set status | Change only the Status cell. Mark `x` only when the reviewer has passed it, or the person says it is done |
| Add task | Append to the sprint's table with the next number, at `—` or `MANUAL` |
| Remove task | Prefer `CUT`. Delete a row only when the person asks, confirm first, then renumber from 1 |
| Edit task | Change only the cells asked about |
| Move task | Remove from one sprint, add to the other with the next number, renumber the first. Read both files before writing either when it crosses phases |
| Add sprint | Next number in the phase (after 2.4 comes 2.5), inserted before Risk Mitigations, with a Verification section |
| Cut a sprint | Keep the section and mark `CUT` in its Goal line. Never renumber the sprints after it |

Editing rules:

- Change only what was asked. Never touch acceptance criteria, dependencies or verification while changing a task.
- One save per operation; batch related changes.
- Task numbers are sequential from 1 within a sprint. Sprint numbers are stable references and may have gaps.
- A table with no Status column gets one on first edit: add it to the header, the separator and every row at `—`, in the same save.
- Duplicate task numbers: flag them and ask which to keep. Never guess.

## Apply results

When the coordinator applies a sprint's result, update statuses in sprint order in one save: completed tasks to `x` only when the review passed, blocked ones to `BLOCKED` with the reason in the chat, and person-only ones to `MANUAL`. Overrides the person gives (`DEFERRED`, `CUT`, `MANUAL`) win.

## Reports

**Sprint report:** done, in progress, blocked, manual, deferred, cut and remaining counts, with progress as done over eligible. Eligible excludes `CUT` and `DEFERRED`.

**Phase report:** one line per sprint, `Sprint {X.Y}: {done}/{eligible} ({%}) — {title}`, then the phase total.

Count from the file as it is now. Never report from memory.
