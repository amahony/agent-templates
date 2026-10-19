---
name: market-validation
description: Run an honest market-fit and viability audit of a project or idea and produce a decision document. Use when someone asks whether something is viable as a business, to audit market fit, to make the case against competitors, whether to apply to an accelerator or bootstrap, or to validate a product or market before investing more time. Gathers verifiable traction data first, researches the competitive field, gets an independent cold read, writes pre-committed pass, middle and kill criteria with a concrete week-one assignment, then hardens the document with an adversarial review.
license: MIT
compatibility: Works best with web search for the competitive landscape and spawn_thread for the independent cold read and review. Uses library_search and library_read for traction data and library_write to save the document.
metadata:
  version: "1.0.0"
  author: Tam Nguyen
  category: Planning
  source: https://github.com/tamdogood/builder-essential-skills/tree/main/skills/validate-market
---

# Market validation

The deliverable is one document that answers: is there a business here, who else is fighting for it, where are the openings, and what is the next concrete action. The audit protects months of the founder's life, so honesty outranks encouragement throughout.

The output is the document and its review, nothing else: no plans to build, no rename, no launch copy. Save it with library_write as `<slug>-market-validation.md` when the person asks for a file or agrees to one.

## Phase 0: Ground truth before opinion

Collect verifiable numbers before writing any judgment. This is what separates an audit from a vibe.

- Look in the library with library_search and library_read for analytics, revenue, waitlist, install counts, customer feedback and earlier research.
- Ask the founder for what is missing: age of the project, users, paying customers, usage that returns unprompted, repository stars or installs if relevant. Ask once, as a short list.
- If an integration such as GitHub or an analytics tool is connected, use it to read the numbers directly. Distinguish "deployed" from "used".
- Apply the bar: **would anyone outside the project be upset if it disappeared tomorrow?** Write the answer down. If it is "no", that fact dominates the whole document, and every recommendation must follow from fixing it.

## Phase 1: Problem and wedge

- State the problem in the founder's own words and quote them. Their phrasing often reveals the wedge better than the pitch does.
- Name the **narrowest wedge**: the one flow someone would adopt this week, in one sentence that starts with a verb ("move X from A to B in 10 seconds"). If the value needs the whole platform, call that a red flag, not a roadmap.
- Name the **target user as a findable person**: role, where they spend time, what they already pay for. "Developers" or "enterprises" is a filter, not a person.

## Phase 2: Landscape research

Search the web with **general category terms**, never the product's name or confidential details. Run at least these four searches and read the top results:

1. The standards and platform state of the category ("<category> landscape <year>").
2. Funding and startups in the category ("<category> startups <year> funding").
3. Products solving the same wedge ("<the wedge, described generically> tool").
4. What incumbents absorbed recently ("<large platform> <category> features <year>").

Then state explicitly:

- **Who owns the lane** the wedge sits in, and whether it is genuinely open.
- **Feature or company?** Could a platform above it absorb this in one release? Say how soon, honestly.
- **Is the timing argument already won?** If the market no longer needs educating, there is no education cost, but the obvious framing is taken.

If web search is not available, say so in the document and continue from your own knowledge, clearly labelled as such.

## Phase 3: Premises

Write three to five premises the recommendation rests on. Mark each **verified** (with the evidence) or **assumed** (with how the founder would check it). Then attack the premise you are most attached to; if you cannot break it, say what outside event would.

## Phase 4: Independent cold read

Get a second opinion that has not seen your reasoning. If spawn_thread is available, open a thread with `contextMode` set to `none` and a brief that holds only the facts: the product, its stage and demand evidence, the founder's stated problem, the landscape summary and the premises. Do not include your conclusions. Ask it to:

1. steelman the strongest version of the business;
2. quote the one detail that reveals what to actually build;
3. name one premise that is wrong and the evidence that would prove it;
4. propose a 48-hour plan with channels, metrics and kill criteria.

Without spawn_thread, ask Critic (@critic) for the same if it is in the chat, giving it the same brief. If neither is possible, write the strongest case against your own view and label it a self-critique, not an independent read.

In the document, quote the cold read's sharpest challenge and say whether you **adopt** it (and revise the premise) or **contest** it (and why).

## Phase 5: Write the document

Keep this order: verdict first, evidence before judgment.

1. **Verdict.** One paragraph: is there a business here, what is the binding constraint, what to do next. No hedging.
2. **Problem statement.**
3. **Demand evidence.** External evidence first, internal second, clearly separated. Include the "would anyone be upset?" answer.
4. **Status quo.** The workarounds and what they cost. Papercut or wound.
5. **Target user and narrowest wedge.**
6. **Market and timing.** The two to four numbers that matter, with sources.
7. **Competitive field.** A table of player, what it is, overlap and real threat, with the status quo as row one and a one-line reason in every threat cell. Then one to three structural observations, including feature versus company.
8. **Strengths.** Only real, verifiable ones. Founder-problem fit counts; "great tech" counts only if it changes distribution or cost.
9. **Weaknesses and risks.** Including the ones the founder will not enjoy reading, such as naming or trademark, platform absorption, a solo founder or undefined pricing. For each, what to do and what it costs.
10. **Premises**, with the cold-read revision applied.
11. **Independent perspective**, from Phase 4, with both positions kept.
12. **Approaches considered.** Two or three, always including a **minimal validation sprint** (weeks, near-zero cost, outreach first) and usually a **lateral repositioning**. Effort, risk, pros, cons and which existing assets each reuses.
13. **Recommendation.** Pick one. If the honest answer is to sequence them, give the sequence with dates.
14. **Business model sketch**, explicitly deferred until after validation. Name the closest working analogy rather than inventing pricing tiers.
15. **Open questions**, each with where its answer will come from.
16. **Success criteria in three pre-committed bands**: pass, middle and kill.
17. **The assignment.** One concrete real-world action for this week: outreach or observation, with names and counts. Not "go build".

### Rigour checklist for the success criteria

Close these gaps before review:

- **Every band has a consequence, including kill.** Pass, middle and kill each name the next action and its deadline. "Kill (or reframe)" is not a decision.
- **Band precedence is explicit.** Say which band wins when results are mixed, such as "kill conditions are checked first".
- **Denominators are fixed.** Add a minimum-effort condition: "kill is valid only if 80 or more asks were sent; otherwise extend one week".
- **Terms are defined.** "Serious reply", "real conversation" and "active user" each get a one-line definition where they trigger a band.
- **The calendar adds up.** If the plan targets an outside deadline such as an application or launch, show that the sprint end date plus writing time lands before it.
- **Measurement exists.** If a criterion needs tracking, setting it up is a named week-one task, with a self-report fallback.
- **Week one is schedulable.** Cold outreach takes time to answer, so week-one targets are "scheduled", not "completed". State whether the founder works on this full-time or part-time, and give the part-time variant.
- **Outreach measures the market, not the founder's messaging skill.** Require two or more channels and absolute counts, not conversion rates.

## Phase 6: Adversarial review

1. Get a review from a reader who sees only the document: a spawn_thread thread with `contextMode` `none` and the document as its brief, or Critic (@critic) given only the document. Ask it to review completeness, consistency (do sections contradict, does the timeline add up), clarity (could the founder act without asking anything), scope (audit only, no padding) and feasibility (can this founder do it in the time stated). Ask for a numbered list of issues and a score out of 10, and tell it to check internal logic only, not outside market facts.
2. Fix every real issue. Where the reviewer is wrong, say so in the document rather than dropping the point silently.
3. Review once more. Stop after two re-reviews or when new findings are cosmetic, and record any remaining disagreements under "Reviewer concerns".
4. Tell the person how many rounds ran, what was found and fixed, and the final score.

If no independent reviewer is available, run the same review yourself and say it was not independent.

## Closing

End the reply with the verdict in two sentences, a link to the document if saved, the three-band decision rule and the week-one assignment. If the founder's profile fits (a real problem, domain expertise, the drive to act), say so plainly and point to the next step, such as an accelerator application or design-partner outreach, but only when the evidence in the document supports it. No congratulations for work the market has not yet validated.
