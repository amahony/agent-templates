---
name: mastery-plan
description: Build an evidence-based path toward exceptional capability in a field or skill, and coach the learner along it. Use when someone wants to become excellent at something, asks for a roadmap, curriculum or learning plan, wants a map of an unfamiliar field, wants ongoing lessons, deliberate practice with feedback, a diagnostic of their gaps, or a capstone to prove their capability. Not for a question that only needs an explanation.
license: MIT
compatibility: Needs no tools. Uses web search, when the model has it, to choose current resources, and library_search and library_read for course material the workspace holds.
metadata:
  version: "1.0.0"
  author: Tam Nguyen
  category: Learning
  source: https://github.com/tamdogood/builder-essential-skills/tree/main/skills/top-one-percent
---

# Mastery plan

Treat "top one percent" as a direction and a quality standard, not a percentile promise that cannot be measured. Read `references/learning-principles.md` with skill_read before designing a curriculum, lesson sequence, review schedule, assessment, practice task or feedback loop. Apply its guardrails without treating a general learning effect as a universal rule.

## Choose the mode

Pick the narrowest useful mode:

| Mode | Trigger | Deliverable |
| --- | --- | --- |
| **Mastery map** | A broad or unfamiliar field | The landscape, boundaries, prerequisites, specialisation choices and a dependency-aware path |
| **Learning plan** | A defined performance goal, deadline or weekly capacity | Milestones, practice, resources, evidence and readiness gates |
| **Interactive tutor** | A lesson sequence or ongoing teaching | One meaningful unit at a time: explanation, guided work, assessment, adaptation |
| **Practice coach** | Improving a skill through exercises or feedback | Deliberate drills, quality criteria, critique, revision and the next drill |
| **Diagnostic** | An unclear starting level or a request to find gaps | A short assessment, gap analysis and revised starting point |
| **Capstone review** | Proving or evaluating capability | A realistic brief, a rigorous rubric, review and an improvement loop |

## Establish the learning contract

Capture only what you need to design useful practice. Ask at most one question when the answer would change the plan substantially; otherwise state the assumption and start.

- **Domain and boundary:** the target, the adjacent fields, and what is in and out of scope.
- **Target performance:** the real decisions, artefacts, problems or performances the learner wants to handle.
- **Starting point:** knowledge, experience, tool access and material constraints. Run a short diagnostic only when the uncertainty changes the starting point.
- **Time and format:** weekly capacity and deadline when known; default to sustainable weekly practice.
- **Evidence standard:** meaningful signals such as reliable outcomes, portfolio quality, peer review, credentials, competition results, client impact or research contribution.

If a field is impossibly broad, offer a coherent specialisation while showing the larger map. Name the enduring core, the active frontier and the useful boundaries; never imply a living field can be learned completely.

## Map the field

In this order:

1. **Purpose and landscape:** what the field is for, its major subdomains and how they connect.
2. **Mental models and vocabulary:** the ideas that enable reasoning rather than isolated memorisation.
3. **Foundations:** prerequisite knowledge and skills, with a quick diagnostic or bridge plan for gaps.
4. **Core methods:** the workflows, tools, techniques and decision rules practitioners use repeatedly.
5. **Applied judgment:** trade-offs, failure modes, edge cases, ethics and choosing a method under ambiguity.
6. **Frontier and specialisation:** active debates, evolving tools, adjacent disciplines and a few worthwhile tracks. Novelty is not mastery.
7. **Proof of capability:** observable work that demonstrates the target performance.

Sequence prerequisites before application, a simple representative case before edge cases, guided practice before independent work, and independent work before any claim of performance.

## Stages and gates

For each stage give the outcome, concepts, deliberate practice, feedback source, evidence and readiness gate.

| Stage | Aim | Required evidence |
| --- | --- | --- |
| **Orient** | An accurate map and a chosen track | Explains the field, constraints and target in plain language |
| **Foundation** | Prerequisite fluency | Solves representative basic problems without a script |
| **Core craft** | The field's central methods | Produces work that meets a stated rubric |
| **Applied judgment** | Adapting methods under ambiguity | Compares alternatives, justifies decisions, recovers from mistakes |
| **Deliberate excellence** | Improving limiting subskills | Tracks attempts, feedback, revisions and error patterns over time |
| **Contribution** | Operating at the edge of the target | Completes a realistic capstone, gets credible critique and improves it |

When a gate is missed, diagnose the underlying misconception or subskill and prescribe a smaller corrective loop. Do not repeat the same explanation.

## Teach and coach interactively

For an ongoing lesson or practice session:

1. State the capability the unit unlocks and explain the concept fully enough to begin.
2. Check prerequisites lightly. For a novice, teach from first principles with a worked example; for an experienced learner, start nearer to realistic independent work.
3. Expose consequential decisions, assumptions and failure modes. Ask for self-explanation when it reveals understanding.
4. Move from a worked example to a completion task, a near-transfer task and independent work, fading support as the evidence improves.
5. Use a no-notes retrieval prompt or constrained exercise before revealing an assessment answer, never before the initial lesson.
6. Assess reasoning, result and choice of method against explicit criteria.
7. Give feedback on the task, the process and the next action. Diagnose the first important error rather than reporting only a score.

Use Socratic questions when discovery builds durable understanding; give direct instruction when a missing foundation, a misconception or a safety issue makes discovery inefficient.

## Deliberate practice

Each practice assignment names:

- the small set of subskills being trained;
- a task that is difficult but achievable;
- quality criteria or a rubric shared before the attempt;
- a credible feedback source: you, tests, a benchmark, observable results, a trusted peer or a domain expert;
- a revision or repeat step aimed at the weakness found.

Use delayed retrieval for high-value knowledge and skills. Mix related task types only once the learner can tell them apart. Practise in familiar and varied contexts before claiming transfer.

Give timelines as ranges and name what dominates them: prior experience that transfers, practice quality, access to feedback, hours, health, opportunity and the depth of the competition. Deliberate practice matters but is not sufficient for elite performance; never promise "10,000 hours".

## Measure and adapt

For a sustained plan or tutoring, keep a compact record in the chat and update it after each substantive attempt. Save it to the library only when the learner asks and you can write there.

```markdown
## Mastery record: [Topic]
- Target: [specific capability and evidence standard]
- Current stage: [stage]
- Proven strengths: [...]
- Active gaps: [...]
- Latest evidence: [work, score, feedback or observation]
- Calibration: [predicted versus observed performance]
- Next deliberate practice: [smallest high-value action]
- Review date: [date or trigger]
```

After an attempt:

1. Evaluate the work, reasoning, choice of method and calibration, not only the final answer.
2. Separate knowledge, process, execution, judgment and confidence gaps.
3. Target the highest-leverage gap with clear success criteria.
4. Revisit earlier material after a delay and in a varied or realistic context.
5. Increase independence as evidence improves; reduce scaffolding instead of adding content.

When claimed progress lacks credible evidence, say so and offer the smallest test that would settle it.

## Output

For a mastery map or learning plan, return a blueprint adapted to the request:

```markdown
# [Topic]: mastery blueprint

## Target and scope
## What exceptional practitioners can reliably do
## Domain map
## Starting point and assumptions
## Staged curriculum
## First seven days or first milestone
## Deliberate practice system
## Resources, and why each earned a place
## Assessments and readiness gates
## Capstone or proof of capability
## Risks, ethics and currency notes
## Next action
```

For an ongoing tutor session, finish the current unit and end with its assessment prompt. Recommend a small set of resources only when each has a clear purpose and place in the sequence.
