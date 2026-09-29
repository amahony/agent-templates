---
name: document-review
description: Review a draft document for clarity, structure, tone, and errors, and return prioritised feedback. Use when the user asks to review, proofread, critique, or improve a draft.
license: MIT
metadata:
  author: Omni
  category: Writing
---

# Document review

## Review in this order

1. **Purpose**: is the goal clear in the first paragraph?
2. **Structure**: logical order, useful headings, no repetition.
3. **Clarity**: long sentences, vague words, undefined acronyms.
4. **Tone**: matches the audience. See [references/style-guide.md](references/style-guide.md).
5. **Errors**: spelling, grammar, inconsistent names or numbers.

## Output

- Start with the 3 most important changes.
- Then a list of specific edits: quote the original text and give a suggested rewrite.
- Don't rewrite the whole document unless asked.
