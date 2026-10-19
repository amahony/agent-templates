# Design-system planning: templates

## DESIGN.md

Follows the Google design.md format (https://github.com/google-labs-code/design.md).

```markdown
---
name: {Product Name}
version: alpha
colors:
  background: "#..."
  surface: "#..."
  text-primary: "#..."
  text-secondary: "#..."
  accent: "#..."
  on-accent: "#..."
  border: "#..."
typography:
  display:
    fontFamily: "{display font stack}"
    fontSize: 40px
    fontWeight: 600
    lineHeight: 1.2
  base:
    fontFamily: "{body font stack}"
    fontSize: 16px
    fontWeight: 400
    lineHeight: 1.5
  sm:
    fontFamily: "{body font stack}"
    fontSize: 14px
    fontWeight: 400
    lineHeight: 1.5
spacing:
  "1": 4px
  "2": 8px
  "3": 12px
  "4": 16px
  "5": 24px
  "6": 32px
rounded:
  sm: 4px
  md: 8px
  full: 9999px
components:
  button-primary:
    backgroundColor: "{colors.accent}"
    textColor: "{colors.on-accent}"
    typography: "{typography.base}"
    rounded: "{rounded.md}"
  input:
    backgroundColor: "{colors.surface}"
    textColor: "{colors.text-primary}"
    typography: "{typography.base}"
    rounded: "{rounded.sm}"
---

# {Product Name} — Design System

## Overview
{What the product is, who it is for, and the one-line design thesis, such as "warm and editorial" or "dense and utilitarian".}

## Colors
{When to use the accent and when neutrals; light and dark mode notes.}

## Typography
{The type scale and why these fonts.}

## Layout
{Grid and spacing approach, page structure, breakpoints.}

## Elevation & Depth
{Shadow and border conventions for cards, dialogs and menus.}

## Shapes
{Corner radius use: when sharp, when rounded, and why.}

## Components
{Notes beyond the tokens: states, variants, sizes, borders and shadows.}

## Do's and Don'ts
**Do:**
- {A rule translated from the plan's experience requirements}

**Don't:**
- {An anti-pattern, often the inverse of a hard rule}

## Surfaces
| Surface | Route or shell | Phase | Priority | Spec |
|---------|----------------|-------|----------|------|
| {name} | {route} | {N} | {P0/P1/P2} | screen-{name}.md |
```

### Token shapes

- `colors`, `spacing` and `rounded` are flat maps of name to value, with no nested groups or lists.
- `typography` has one token per text style, each with `fontFamily` and `fontSize`, plus `fontWeight`, `lineHeight` and `letterSpacing` when set.
- `components` is a flat map with one key per component or variant (`button-primary`, not `button` → `primary`). Sub-tokens: `backgroundColor`, `textColor`, `typography`, `rounded`, `padding`, `size`, `height`, `width`. Anything else, such as a border colour or shadow, goes in the Components prose.
- References name the group: `{colors.accent}`, `{typography.base}`. A bare `{accent}` is an error.

## Screen spec

```markdown
# {Screen Name}

**Route or shell:** {route, or modal, full screen, side panel}
**Phase:** {N}
**Purpose:** {one sentence}

## Layout
{Structured text wireframe: regions top to bottom, what each holds}

## Components
- {Component name as in DESIGN.md}: {note}

## States
| State | Behavior |
|-------|----------|
| Empty | {what shows with no data} |
| Loading | {skeleton, spinner or other} |
| Error | {inline, toast or blocking, per Do's and Don'ts} |
| Success | {confirmation pattern} |
| {Edge case from the plan} | {behavior} |

## Copy rules
- {Labels, empty-state wording, forbidden phrases, tone}

## Acceptance bullets
- {One observable outcome someone can confirm on the built screen}
```

## Checklist for DESIGN.md

- The front matter parses as YAML and has `name` and `version`.
- `colors`, `typography`, `spacing`, `rounded` and `components` are present; `components` has a primary button and an input.
- The body has all sections in order.
- Every colour in prose exists in the YAML, and no value appears only in prose.
- Text contrast is at least 4.5:1 in every mode.
