---
name: seo-keyword-rewrite
description: Rewrite existing copy while keeping target SEO keywords, entities, and rough keyword density intact. Use when improving copy that must still rank, such as blog posts, landing pages, or product descriptions, and the user cares about specific keywords, search intent, or on-page SEO.
license: MIT
metadata:
  version: "1.0.0"
  author: rephrasyai
  category: Writing
  source: https://github.com/rephrasyai/rephrasy-skills/tree/main/skills/seo-keyword-preserving-rewrite
---

# SEO keyword rewrite

Improve readability and voice without dropping the keywords a page needs to rank.

## When to use

- The user is rewriting content that must keep ranking for specific terms.
- You're editing a blog post, landing page, or product copy and SEO matters.
- The user mentions "keywords", "search intent", "don't lose the SEO", or gives a target term.

## Before you rewrite

1. **Identify the targets.** Ask for, or infer, the primary keyword, any secondary keywords, and named entities (brands, products, people). If they are not given, take the terms that repeat and clearly carry the page's intent, and tell the user which ones you chose.
2. **Note their placements.** Record which appear in the title, the first 100 words, subheadings, and image alt text. These positions carry the most weight, so protect them.
3. **Count roughly.** Get an approximate count for the primary keyword so you can match it after rewriting. Don't chase exact percentages.

## Rewrite rules

- **Keep the primary keyword** in the title, the first paragraph, and at least one subheading, word for word, not as a synonym.
- **Preserve exact entity names.** Brands, products, and proper nouns stay exact; never vary them.
- **Vary the surrounding language freely.** Outside those anchor spots, rewrite naturally. Related terms help search engines understand the topic.
- **Match intent, not just the string.** If the term is "best running shoes", the rewrite must still deliver a comparison or recommendation, not drift into a history of running.
- **Hold density steady.** Don't strip so many mentions that the page thins out, and don't stuff. If you added keywords to hit a number, you overdid it.
- **Protect links and their anchor text** unless asked to change them.
- **Add no facts.** Keep every claim the copy makes and add none of your own.

## Then edit for AI patterns

Apply the ai-pattern-editing skill to everything except the protected anchors. The result should read like a person wrote it and still hit every keyword a search engine checks.

## Output

Return the rewritten copy, then a short checklist:

- Primary keyword kept in the title, first paragraph, and a subheading (yes or no for each)
- Secondary keywords retained: list
- Entities preserved exactly: list
- Approximate density compared with the original: similar, lower, or higher
