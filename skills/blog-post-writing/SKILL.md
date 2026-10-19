---
name: blog-post-writing
description: Write a blog post that reads like a person wrote it and earns search traffic. Use when someone wants to draft, edit or plan a blog post, write about their product or project for search and traction, or make an existing draft sound less like AI. Picks an angle that no published post already owns, builds a lead and section spine, drafts in a plain house voice, runs a humanizer pass, and adds on-page SEO and a distribution plan.
license: MIT
compatibility: Uses library_search and library_read for published posts, brand guidelines and product facts, and library_write to save drafts. Web search, when the model has it, helps check what already ranks.
metadata:
  version: "1.0.0"
  author: Tam Nguyen
  category: Writing
  source: https://github.com/tamdogood/builder-essential-skills/tree/main/skills/write-blog
---

# Blog post writing

The bar: the post reads like a person wrote it, it targets a search cluster no other post of theirs already owns, and every claim in it is true.

Read the references with skill_read as each step calls for them: `references/angles.md`, `references/craft.md`, `references/voice.md` and `references/seo.md`. `voice.md` is the default house voice. When the organisation has a style guide in the library, it wins wherever the two disagree.

## 1. Read the ground truth first

Before writing, look in the library with library_search and library_read for:

- **Published posts:** every title, description and tag set, so the new post does not compete with one. If the library does not hold them, ask for the blog's URL or a list.
- **One or two full posts**, to absorb the voice.
- **Product facts, docs and brand guidelines**, so claims and examples are accurate.

Ask only for what is missing.

## 2. Pick and pitch the angle

Each post must own a distinct search cluster; two posts chasing the same keywords split their own ranking. Using `angles.md`, pick an angle no published post owns, then pitch it in one message before drafting: the working title, the one-sentence thesis and the three to five keyword phrases it targets. Wait for a yes. If the topic collides with an existing post, say so and propose an adjacent, distinct angle.

## 3. Outline

A good post has a spine, not a listicle. Read `craft.md` before outlining; the lead and the heading spine decide most of whether the post is finished and found.

- **A lead** (description and opening) that names a concrete, specific problem the reader has.
- **Four to seven sections**, each making a claim backed by a real example, command, number or quote from the person's material. Made-up product details are worse than none.
- **An honest-limitations beat**: what this is not, or what is deferred. Candour keeps it from reading like marketing.
- **A close** that lands the thesis and ends on one concrete thing the reader can do or check, never a generic wrap-up.

Read only the headings in order: they must show the argument.

## 4. Draft

Write plain markdown. Follow `voice.md` and `craft.md`. Keep one clear opinion and support it with evidence. For technical or instructional passages, apply the Simplified Technical English baseline in `voice.md`: short sentences, one term per concept, direct actions, exact code and names. Apply the direct-response pass from `craft.md` to the title, description and closing call to action only.

## 5. Humanize (mandatory)

Run the humanizer checklist in `voice.md` over the whole draft. Strip significance inflation, promotional adjectives, the rule of three, trailing "-ing" analyses, negative parallelisms ("it's not X, it's Y"), synonym cycling, hedging and chat artefacts. Check the hard rules last, including the search for dashes and curly quotes, then read it as if aloud and fix anything hard to follow.

## 6. Add the SEO and hand over

Follow `seo.md`:

- Put the primary phrase in the title, the description, the first heading and the tags.
- Suggest two or three internal links to related published posts with descriptive anchor text, one reciprocal link from the most related existing post, and one outbound link to an authority.
- Give the post's metadata in one block: title, slug, description, tags and a cover image idea.

You cannot publish the post or open the site. Give the person the post-publish checklist from `seo.md` (sitemap, feed, meta tags, structured data, cover image) to run themselves.

## 7. Distribution plan

A correct post with no inbound links does not rank. After the draft, offer:

- a short social thread that teaches the core insight and links the post's production URL;
- where the question the post answers is already being asked, so the person can answer it there and link the post;
- which docs or pages should link to it.

Offer to write the thread, or hand it to the matching skill, such as linkedin-post-writing for LinkedIn.

## Deliver

Return the pitch first and wait for agreement. After that, return the metadata block, the post in markdown, the SEO suggestions, the checklist and the distribution plan, in that order. Mark placeholders for details only the author knows. Save the draft with library_write only when someone asks, and say the file name.

## Guardrails

- Never invent product features, figures, quotes, customers or results. Quote the person's material.
- Never weaken the voice to sound "professional". Concrete and a little contrarian beats polished and generic.
- Do not write a post whose angle overlaps a published one; adjust the angle.
- Do not claim strict Simplified Technical English conformance.
