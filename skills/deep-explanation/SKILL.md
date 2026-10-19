---
name: deep-explanation
description: Explain any topic from first principles as a layered, causal explanation that fully answers the question. Use when someone asks what something is, why or how it works, what is special about it, how alternatives compare, what different perspectives reveal, or asks for a deep dive or to really understand a topic. Answers the question itself; it does not replace the answer with a roadmap, diagnostic or quiz.
license: MIT
compatibility: Needs no tools. Uses web search, when the model has it, for current, niche or contested claims, and library_search and library_read for material the workspace holds.
metadata:
  version: "1.0.0"
  author: Tam Nguyen
  category: Learning
  source: https://github.com/tamdogood/builder-essential-skills/tree/main/skills/top-one-percent
---

# Deep explanation

Produce unusually clear understanding. The explanation itself must create it: no shallow resource list, no generic invitation, no study plan in place of the answer.

## Research before synthesis

Research when claims may have changed, the topic is niche or contested, or the question is about a current ecosystem, frontier, product, company, standard, law or recommendation. Check the library first when the workspace may hold relevant material. Prefer official documentation, primary research, standards bodies, direct data and credible first-party statements; use strong secondary sources for interpretation, not in place of an available primary source. If web search is not available, say which claims could be out of date.

Keep these apart in the text:

- stable principles and current implementation details;
- documented facts and your own synthesis or inference;
- marketing claims and mechanisms or observed trade-offs;
- broad consensus and active debate.

Cite sources near the claims they support. Do not cite common knowledge, and never let a list of links stand in for explanation.

## Build the causal model

Before drafting, identify the central thesis and the few causal relationships that make the rest of the topic make sense. Explain mechanisms with explicit links such as "because", "which means" and "therefore". A feature inventory leaves the learner to work out why the features matter.

Use this sequence when it fits; leave out sections that do not apply rather than filling a template:

1. **Simplest accurate model.** Give the direct answer or a compact analogy first. If you use an analogy, say where it stops being accurate.
2. **Layers people conflate.** Define the important actors, abstractions or terms and what each is responsible for. Use a compact table when an exact mapping is clearer than prose.
3. **Mechanism.** Trace how it works from cause to effect. Make hidden constraints and design decisions visible.
4. **Concrete example.** Walk through one representative end-to-end case, worked example or before-and-after comparison. Anchor every major abstraction in something observable.
5. **Why it matters.** Connect the mechanism to its consequences for users, engineering, business, science or society, as relevant.
6. **Perspectives.** When the topic benefits, analyse at least two genuinely different lenses, such as technical architecture, economics, competitive strategy, operations, history, ethics or user behaviour. Do not relabel the same point as two perspectives.
7. **Alternatives and the strongest counterargument.** Say when the celebrated approach is not the best, what complexity it moves rather than removes, and what a thoughtful critic would say.
8. **Implications for the learner.** Translate the analysis into what it means for their projects, decisions or next conceptual step, when you know enough about them.
9. **Synthesis.** End with the deepest reusable idea in one or two sentences. For a learning-oriented request, optionally add two to four non-trivial questions worth exploring next; never make answering them a condition of getting the explanation.

## Calibrate depth and form

- A simple factual question gets a concise answer.
- A normal conceptual question gets enough sections and examples to make the causal model clear.
- "Deep dive", "teach me everything" or "really understand" favours comprehensive synthesis over brevity. "Everything" means the complete conceptual map, the important mechanisms, trade-offs and frontier, not every fact ever published.
- For a broad topic, give the big picture first, then zoom into the parts that answer the question. Say what you left out.
- Use prose for reasoning, bullets for sets, tables for exact comparisons, and diagrams only when relationships or order are materially easier to see.
- Define jargon on first use without losing precision. For an experienced learner, move quickly through the basics and spend the time on mechanisms, edge cases, competing models and second-order effects.

Recommend resources only when each has a clear purpose and place in a sequence.

## Shape of the answer

Lead with the answer, then use the smallest useful subset of:

```markdown
# [Topic]

[Simplest accurate model and central thesis]

## The layers or terms people conflate
## How it actually works
## A concrete example
## Why it matters from different perspectives
## Alternatives, trade-offs and counterargument
## What this means for you
## The deeper takeaway
## Questions worth exploring next
```

This is a coverage guide, not a fixed set of headings. If the person then wants to build lasting capability in the topic, offer the mastery-plan skill's approach in one line; do not append a curriculum.

## Final check

Before responding, confirm that:

- the opening answers the real question directly;
- the response explains causal mechanisms, not only labels or features;
- each important abstraction is grounded in at least one concrete example;
- commonly confused layers or alternatives are distinguished;
- a real trade-off or the strongest counterargument appears when relevant;
- each perspective adds a genuinely different insight;
- current, niche or contested claims are researched, and uncertainty is labelled;
- personalisation changes the explanation, rather than merely mentioning the learner;
- the learner leaves with a reusable mental model and a clear next step.
