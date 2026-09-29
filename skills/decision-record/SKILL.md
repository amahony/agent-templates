---
name: decision-record
description: Write a decision record capturing context, options considered, and the chosen option. Use when the user wants to document a decision, write an ADR, or record why something was chosen.
license: MIT
metadata:
  author: Omni
  category: Planning
---

# Decision record

## Template

```markdown
# [Short decision title]

**Date:** [date] · **Status:** Proposed / Accepted / Superseded

## Context

What problem or constraint forced a decision.

## Options considered

For each option: a one-line description, its pros and its cons.

## Decision

The chosen option and the main reason for it.

## Consequences

What becomes easier, what becomes harder, and what to revisit later.
```

## Rules

- Ask for missing options or reasons rather than inventing them.
- Stay neutral about the options that were rejected.
