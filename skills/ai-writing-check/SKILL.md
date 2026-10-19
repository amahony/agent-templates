---
name: ai-writing-check
description: Audit a draft for the tells that make AI detectors and human readers flag it as machine-written, and report what to fix, before publishing or sending. Use when the user asks "does this sound AI", "will this get flagged", or wants to check a draft before it goes out. Reviews only; does not rewrite.
license: MIT
metadata:
  version: "1.0.0"
  author: rephrasyai
  category: Writing
  source: https://github.com/rephrasyai/rephrasy-skills/tree/main/skills/detect-ai-text-self-check
---

# AI writing check

A pre-flight audit that scores a draft for AI tells and tells the user exactly what to fix. No external tool is required: this is a structured read, not a detector.

## When to use

- The user asks whether a draft "sounds like AI" or "will get flagged".
- Before publishing or sending anything that was drafted with AI help.
- As the final check after the ai-pattern-editing skill, to confirm the fixes landed.

## What detectors key on

AI detectors mostly react to two statistical properties plus learned patterns:

- **Low perplexity.** The text is too predictable; every next word is the obvious one.
- **Low burstiness.** Sentence length and complexity barely vary; humans spike and dip.
- **Learned fingerprints.** Modern detectors are neural networks trained on large sets of AI documents, so they also catch structural habits, not just statistics.

You can't compute perplexity by hand, but the symptoms are readable.

## The checklist

Score each item 0 to 2 (0 = clean, 2 = strong tell):

1. **Sentence-length variance.** Do lengths vary, or march in even lines? (even = tell)
2. **Filler openers.** "In today's...", "It's important to note", "When it comes to". (present = tell)
3. **Triads and lists of three.** Overused parallel structures. (frequent = tell)
4. **Empty transitions.** "Moreover", "Furthermore", "Additionally", "In conclusion". (frequent = tell)
5. **Abstraction density.** Claims with no concrete number, name, or example. (high = tell)
6. **Vocabulary flags.** "delve", "leverage", "utilize", "tapestry", "myriad", "realm", "testament". (present = tell)
7. **Paragraph symmetry.** Every paragraph the same length and shape. (uniform = tell)
8. **Over-explanation.** Restating the premise before making the point. (present = tell)

## Report format

Return:

- **Risk read:** Low, Medium, or High (sum the scores: 0 to 4 low, 5 to 9 medium, 10 or more high).
- **Top three tells**, each with a quoted example line from the draft.
- **A concrete fix** for each: the specific edit, not "make it more human". Where a fix needs a detail the draft lacks, such as a number, name, or example, ask the user for it. Never invent one.
- An offer to apply the fixes with the ai-pattern-editing skill.

## Honest limits

- This is a heuristic read, not a detector score. A clean check reduces risk; it can't guarantee any specific tool passes.
- Detectors produce false positives, especially on non-native English and terse technical writing. A High read doesn't prove AI wrote the text, only that it reads that way.
- Very short text (under about 100 words) is unreliable for both detectors and this check.
