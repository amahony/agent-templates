---
name: product-planning
description: Plan a product, a feature or a set of related features, or a non-code project such as a launch or event, and write a product plan that phase planning can turn into phases and sprints. Use when someone says "plan this feature", "I want to build", "help me think through", "spec this out", "what are my options for" or "create a product plan". Gathers context in one round of questions, compares at least two options, records decisions and open questions, and ends with a handoff for phase planning.
license: MIT
compatibility: Uses library_search and library_read for existing plans and research, and library_write to save the plan. The plan's format is shared with Phase Runner, so a code project can be handed to Claude Code or Auggie.
metadata:
  version: "1.0.0"
  author: Jeremy Kaye
  category: Planning
  source: https://github.com/AyeJK/phase-runner/tree/main/plugin/skills/product-planner
---

# Product planning

The deliverable is one product plan: what is being built, why, which options were weighed, what is decided and what is still open. It is the input to phase planning, which turns it into phases, sprints and tasks. This skill does not break work into sprints and does not set visual design.

Terms used across this team: a **phase** is a stage of the work with a goal and a finish line. A **sprint** is a bundle of tasks one worker can finish and that can be checked on its own. It is not a period of time. A **task** is one row in a sprint's table.

## Step 1: Gather context

**If a plan or spec already exists**, in the chat or the library (search with library_search, open with library_read), treat it as the source of truth. Extract the name, goals, constraints and anything already decided. Ask only for what is missing.

**If starting from scratch**, ask these in one message, not one at a time:

1. What are we building? A name and a one-line description.
2. What problem does it solve, and for whom? What do they do today instead?
3. Scope: one feature, several related features, a whole product, or a project that is not software?
4. Constraints: existing stack or tools, budget, deadline, people involved.
5. Options already on the table, or already ruled out.
6. Anything already decided.
7. The biggest unknown: what this plan most needs to settle.

Do not write the plan from a one-liner. Probe until there is enough for a substantive plan, then stop asking.

## Step 2: Ground it

Before writing, look for what already exists: earlier plans, phase files, research, a design system or decision records in the library. Note what exists and what is new. For a code project, ask for the stack and the main structural facts (data model, main routes, hosting) if the library does not have them. Never invent them.

## Step 3: Write the plan

Use these sections, in this order.

1. **Header.** Name, one-line description, date, status (Draft, In review or Approved).
2. **Overview.** What is being built (two to four sentences), why, what success looks like as measurable outcomes, and scope: what is in and what is explicitly out.
3. **Flow.** How things move: for software, the components, data and decision points; for a project, the sequence of people, handoffs and deliverables. Use a numbered list or a table, labelled at every step, followed by a short plain-language narrative.
4. **Options considered.** Two to five approaches. For each: a one-line description, pros, cons and a verdict (Selected, Rejected or Deferred, with the reason). If only one option was considered, say so and why.
5. **Screens.** Only when there is a user interface: the main screen and its key states (empty, loading, error, success), described as structure, not visual style. Visual design belongs to design-system planning. Omit the section for work with no interface, and say why.
6. **Decisions.** Only things genuinely decided. For each: **Decision**, **Rationale**, **Constraints** (what it rules out). Use the decision-record skill when a decision deserves its own record.
7. **Open questions and risks.** For each question: **Question**, **Impact** (what depends on it), **Owner** (the person, an outside party, or research). For each risk: likelihood, impact and how it is handled.
8. **Handoff.** What the first phase should deliver, the key constraints a worker must know, and a rough, non-binding phase outline such as "Phase 1: data and API, Phase 2: interface, Phase 3: polish".

## Step 4: Save and present

When the person asks for a file or agrees to one, save the plan with library_write as `Plan-{Name}-{YYYY-MM-DD}.md`, for example `Plan-NotificationsRework-2026-05-22.md`. Give the link and offer two next steps:

- **Phase planning:** turn this plan into phases and sprints.
- **Iterate:** revise an option, add a screen, update the flow now that something is decided.

For a code project that will be built in Claude Code or Auggie, tell the person the plan belongs in the repository's `docs/` folder, where Phase Runner's tools look for it.

## Iterating

To update a saved plan: read the current file with library_read, make the targeted change, and save it over the same file by its fileId. Never rewrite sections nobody asked about. Say in one line what changed.

## Checks before saving

- All eight sections are present, or Screens is omitted with a reason.
- At least two options are compared, or the single option is explained.
- Decisions hold only what is decided; everything else is an open question with an owner.
- Success is stated as something observable.
- The handoff names what the first phase delivers.
- Nothing in the plan is a guess presented as a fact. Mark assumptions as assumptions.
