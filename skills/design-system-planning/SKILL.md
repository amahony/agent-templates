---
name: design-system-planning
description: Set a product's visual design language and screen contracts after the product plan and before phase planning. Writes DESIGN.md (Google design.md format), design-system.md and one spec per screen with states and acceptance bullets. Use when someone wants to design the interface before building, lock a design system, choose a visual direction, write screen specs, or run "the design pass". Not for architecture, sprint breakdown or building production components.
license: MIT
compatibility: Uses library_search and library_read for the product plan and existing design files, and library_write to save them. Files follow Phase Runner's design-planner format, so a code project can be handed to Claude Code or Auggie.
metadata:
  version: "1.0.0"
  author: Jeremy Kaye
  category: Design
  source: https://github.com/AyeJK/phase-runner/tree/main/plugin/skills/design-planner
---

# Design-system planning

Sets the visual language and the screen contracts. The order is: product plan (what and why) → this skill (how it looks and behaves) → phase planning (sprints). Phase planning puts screen specs in the Reference column of interface tasks, and the acceptance bullets become the sprint's checks.

Terms used across this team: a **phase** is a stage of the work with a goal and a finish line. A **sprint** is a bundle of tasks one worker can finish and that can be checked on its own. It is not a period of time.

Templates for every file are in [references/templates.md](references/templates.md).

## Files

Saved to the library with library_write when the person asks for files or agrees to them:

| File | Purpose |
|------|---------|
| `DESIGN.md` | The contract: tokens in YAML front matter, rationale in prose. Tokens are normative |
| `design-system.md` | Expanded patterns for whoever builds: CSS custom properties, type scale, component patterns, copy rules, screen index |
| `screen-{kebab-name}.md` | One per screen: layout, components, states, copy, acceptance bullets |
| `screen-{kebab-name}.html` | Optional mockup, only when the person asks to see one |

For a code project, tell the person these files belong in the repository at `docs/design/` (screens in `docs/design/screens/` without the `screen-` prefix), where Phase Runner's tools read them.

If design files already exist, read all of them before changing anything, and keep locked decisions unless the person asks to revise them.

## Step 1: Read inputs

1. The product plan, from the chat or the library. Extract the product name, audience, every interface surface mentioned, hard rules about the experience and the stack.
2. The project's own vocabulary. Use the terms the plan already uses; never introduce new ones.
3. Existing design: earlier design files, brand guidelines, screenshots the person shares.

Do not re-ask what the plan answers. Ask only for gaps that block a design decision.

## Step 2: Surface inventory

Before any visual work, list the surfaces in a table:

| Surface | Route or shell | Phase | Priority | Notes |
|---------|----------------|-------|----------|-------|

Specify only near-term phases, usually 1 to 3. Defer later phases to a later design pass unless asked. Show the inventory and confirm missing surfaces and priorities before choosing a direction.

## Step 3: Choose a direction

Present two or three directions as short cards:

- **Name**: a short label
- **Mood**: one line
- **Type and colour**: fonts, light or dark, accent strategy
- **Fit**: why it suits this product and audience
- **Risk**: what it makes harder

Ask the person to pick one, blend two, or point to a reference. **Do not write tokens until they confirm.** Avoid generic defaults such as a plain sans-serif with a purple gradient unless the product calls for it.

When surfaces have different jobs, such as an admin console and a public site, choose either one system with two modes (shared tokens plus mode overrides) or a separate design pass per surface family. State the choice in DESIGN.md's Overview.

## Step 4: Write DESIGN.md

Follow the template. Requirements:

1. YAML front matter with `name`, `version: alpha`, and token groups `colors`, `typography`, `spacing`, `rounded` and `components` (at least a primary button and one input).
2. Body sections in this order: Overview, Colors, Typography, Layout, Elevation & Depth, Shapes, Components, Do's and Don'ts, then Surfaces.
3. Prose matches tokens: every colour named in prose exists in the YAML.
4. Do's and Don'ts translate the plan's experience rules into component behaviour, for example "never block with an error dialog" becomes "errors appear inline under the field".
5. Text contrast is at least 4.5:1 against its background, in every mode.

## Step 5: Write screen specs

For each P0 and P1 surface, write `screen-{kebab-name}.md` with: route or shell, purpose in one sentence, a layout wireframe as structured text, components named as in DESIGN.md, a states table (empty, loading, error, success and edge cases from the plan), copy rules, and **acceptance bullets**: observable checks someone can confirm by looking at the built screen. Reference DESIGN.md sections instead of repeating token values.

Write an HTML mockup only when the person asks for one: a single self-contained file with inline CSS that uses the real tokens and labels every interactive element.

## Step 6: Write design-system.md

Sections: last updated and a link to DESIGN.md, design intent as a short table of principles, a copy-paste `:root` block of CSS custom properties derived from the YAML, a typography table mapping elements to tokens, core component patterns (buttons, inputs, cards, dialogs used in the specs), voice rules for interface copy, and a screen index linking each surface to its spec.

When DESIGN.md and design-system.md disagree on a token value, **DESIGN.md wins**: update design-system.md to match.

## Step 7: Handoff

List the saved files and give the constraints phase planning must follow:

- An interface task's Reference cell names its screen spec file.
- A sprint's `assert:` lines come from the spec's acceptance bullets.
- Task text says "implement per screen spec" and invents no visual detail.
- A sprint with no interface gets `skip-ui: true` and no design reference.

## Iterating

| Request | Action |
|---------|--------|
| New direction | Redo Step 3, rewrite DESIGN.md tokens and design-system.md, and list the screen specs that need layout changes |
| Add a screen | New screen spec, and add it to the screen index and the Surfaces table |
| Change a token | Edit DESIGN.md's YAML and prose, then the CSS block in design-system.md |
| Design report | Surfaces specified and deferred, open contrast or consistency issues, files changed |

Read a file with library_read before changing it, and save over it by its fileId.

## Checks before finishing

- The person confirmed the direction before tokens were written.
- DESIGN.md has valid YAML and every required section, or says why one is omitted.
- Every P0 and P1 surface has a screen spec with acceptance bullets.
- design-system.md's CSS values match DESIGN.md exactly.
- The plan's experience rules appear in Do's and Don'ts.
- No sprint or task breakdown appears in any design file; that belongs to phase planning.
