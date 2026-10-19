# Phase planning: format

## Full phase file template

```markdown
# Phase {N} — {Phase Title}

{One paragraph: what this phase delivers and why it is scoped this way. Add a target date only when the person gives one.}

**Sequencing:** {Which sprints depend on which, and which can run in parallel as a wave, e.g. "1.2 and 1.3 can run together after 1.1."}

---

# Sprint {N}.1 — {Sprint Title}

### Goal

{One sentence: what this sprint accomplishes.}

### Tasks

| Status | # | Task | Module | Reference |
|--------|---|------|--------|-----------|
| — | 1 | {task} | {module} | {document} |
| — | 2 | {task} | {module} |
| — | 3 | {task} |

### Acceptance Criteria

- {Observable outcome}
- {Observable outcome}

### Dependencies

- {Earlier sprint, outside party, or "None"}

### Verification

- cli: {check command, code projects only}
- ui: {route, when the sprint changes an interface}
- assert: {what passing means, one line per check}

---

# Sprint {N}.2 — {Sprint Title}

...

---

## Risk Mitigations

{Optional. Known risks for this phase and how they are handled.}

## Scope Guard

{Optional. What this phase explicitly does not include.}
```

Sprint headings must match `# Sprint {Phase}.{Sprint} — {Title}` exactly, with an em dash. Phase Runner's tools find sprints by this heading and skip any sprint whose heading differs.

## Edge cases

- **A whole sprint is cut:** keep its section, mark `CUT` in its Goal line, and do not renumber later sprints.
- **Inserting a sprint between two others:** append it at the end and note the dependency. Use a decimal number such as 1.2.5 only when the person wants the order kept without renumbering.
- **Moving a sprint to another phase:** it keeps its title, takes the next number in the target phase, and gets a one-line note under its Goal saying where it came from.
- **Checkbox-style tables** (`[ ]`, `[x]`): convert to the status values above on first edit and say so in the reply.
- **A task with no sensible Module** (research, decisions, approvals): use the three-cell row. If only a person can do it, its status is `MANUAL`.
- **Old sprints without Verification:** do not add one while changing something else. Add it only when the person asks, or on a new sprint.
- **Two files in one operation:** read both before writing either. If one has an unexpected shape, stop before any write.
