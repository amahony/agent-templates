---
name: paper-opportunity-radar
description: Run a cumulative daily or one-off sweep of research papers on a chosen topic, audit their claims, methods, integrity signals and independent support, then identify overlooked but feasible project or business opportunities in a source-grounded report. Use when asked to monitor papers on a topic, mine buried research, judge whether a paper is credible or reproducible, find unimplemented research ideas, or separate promising work from hype, weak evidence and retracted or contradicted results.
license: MIT
compatibility: Needs web search for papers and the library_search, library_read and library_write tools to keep the radar's files between runs.
metadata:
  version: "1.0.0"
  author: Tam Nguyen
  category: Research
  source: https://github.com/tamdogood/builder-essential-skills/tree/main/skills/paper-opportunity-radar
---

# Paper Opportunity Radar

Treat the literature as an evidence base to work through over time, not a feed to summarize. Build a cumulative corpus, audit important papers claim by claim, look for what happened after publication, and turn only defensible gaps into testable opportunities.

## Standards for this skill

- **Bound the corpus.** Define the sources, query strings, dates, languages, document types and where the last run stopped. Say "all records returned by this protocol", never "all papers ever".
- **Fact-check claim by claim.** Every factual statement in a report needs a source you opened. Mark interpretations `INFERENCE` and gaps `UNKNOWN`.
- **Use precise integrity language.** `INTEGRITY CONCERN` for observable anomalies. `RETRACTED`, `CORRECTED` or `FORMAL MISCONDUCT FINDING` only when the publisher, institution, court or regulator supports it.
- **Report where prior art was searched.** Use `NOT FOUND IN SEARCH`, with where, how and when, instead of "nobody has done this".
- **Keep four judgments separate:** evidence strength, confidence that it is unexplored, feasibility and real-world value. Never average them into one score that hides a fatal weakness.

## Inputs

Require a **topic**. Infer the rest when safe and state what you inferred: the decision it informs (explore a business, find a project, judge feasibility or follow progress); the historical horizon (earliest searchable record to today by default); domains and adjacent fields; language and publication-type limits; the person's skills, capital, equipment, data and time; and depth: `standard` by default, `brief` or `deep` on request.

Ask one short question only when the topic is missing or an ambiguity would change the corpus. For medical, legal, safety-critical or investment decisions, call the work research analysis and say where a qualified professional is needed.

If web search is not available this turn, say so, work only from papers in the library or pasted into the chat, and do not describe the run as a sweep.

## The radar's files

The radar keeps its state in the library so the next run can resume. Before the first run, ask before creating files; once the person agrees to a radar, save its files as part of every run. Name them with a short topic slug:

| The references call it | Library file |
|---|---|
| `scope.md` | `<slug>-radar-scope.md`: boundary, query atlas and run policy |
| `search-log.md` | `<slug>-radar-search-log.md`: exact source, query, filter, time and result log |
| `corpus.tsv` | `<slug>-radar-corpus.csv`: deduplicated paper inventory and queue |
| `opportunity-ledger.md` | `<slug>-radar-opportunities.md`: living opportunities, blockers and verdicts |
| `papers/<canonical-id>.md` | `<slug>-paper-<canonical-id>.md`: one audit dossier per paper |
| `reports/YYYY-MM-DD.md` | `<slug>-radar-report-YYYY-MM-DD.md`: the run's report |

Find existing files with library_search and open them with library_read. Update a living file by passing its fileId and the full new content to library_write, keeping any edits people made. Never overwrite an earlier report.

Use the DOI as the canonical ID when there is one, then a PMID, arXiv or other repository ID, then a normalized title and year. The corpus has the columns `paper_id, title, year, canonical_url, discovered_at, discovery_source, status, relevance, evidence_verdict, next_action`. Status is one of `discovered`, `triaged`, `queued`, `audited`, `monitor` or `excluded`.

## Workflow

### 1. Frame a falsifiable search

Write down the core phenomenon, mechanism or problem; synonyms, former names, acronyms and neighbouring terms; inclusion and exclusion rules; the decision the research should inform; and what evidence would make a paper or opportunity uninteresting. Read `references/discovery-protocol.md` with skill_read, then write the query atlas and source plan to the scope file. If the topic is huge, split it by mechanism or use case; never narrow it silently.

### 2. Resume before searching

Read the scope file, the latest report, unresolved dossiers, the opportunity ledger and the corpus. Resume from the recorded cursor. On the first run, create the files and label the historical corpus `BASELINE IN PROGRESS` until every planned source and time band has been visited.

### 3. Cover three lanes

Every run covers the **new delta** (papers published or indexed since the last run), the **archive backfill** (the next unvisited source, query and time band) and the **follow-up graph** (references, citing papers, corrections, replications and later implementations of high-value or disputed papers).

Use at least two independent scholarly indexes, plus a domain index when one exists. Record every exact query, filter, time, result count, new-paper count and limitation in the search log before changing lanes. Deduplicate before screening. A search hit is not a paper read: triage each new candidate, audit only what can get genuine attention, and queue the rest with a reason.

### 4. Choose papers for deep audit

Prefer a balanced set: claims the field leans on; surprisingly large effects or broad conclusions; under-cited work with a specific, testable mechanism; papers made newly feasible by cheaper compute, sensors, data, regulation or standards; negative results that reveal a bottleneck; and papers whose later citations disagree. `standard` depth is up to five full-paper audits per run. A queued paper is more honest than an abstract-only "deep dive".

### 5. Audit the paper, not its story

Read `references/evidence-audit.md` before the first audit of a run. For each paper: resolve its canonical version, corrections, retractions and conflicts; extract each load-bearing claim with its population, comparator, outcome, uncertainty and limits; trace each claim to the method, table, figure, data or proof behind it; check design, controls, leakage, statistics, robustness and reproducibility; search for replication, contradiction and real-world use; and write the dossier with the decisive next verification step.

If only the abstract is accessible, label the dossier `ABSTRACT-ONLY`, cap the evidence score at 2/5 and give no integrity verdict. Never bypass a paywall or invent missing methods.

### 6. Assign an evidence verdict

Choose one, and say what it applies to: `SUBSTANTIATED`, `PROMISING — UNREPLICATED`, `MIXED OR FRAGILE`, `CONTRADICTED OR NOT REPRODUCED`, `INTEGRITY CONCERN — UNRESOLVED`, `RETRACTED OR SUPERSEDED` or `INSUFFICIENT ACCESS`. Record contrary evidence even when a paper stays promising.

### 7. Harvest and challenge opportunities

Read `references/opportunity-and-report.md`. Separate the demonstrated mechanism from the authors' proposed application. Look for opportunities in validated capabilities, newly removable bottlenecks, transfers across fields, enabling tools, datasets, replication needs and unserved workflows.

For each candidate, search for prior art and implementations (later papers, patents, repositories, products, standards, trials and the status quo), then score evidence, unexploredness, technical and operational feasibility, and pain and value capture, each 0–5; list safety, regulatory, IP, ethical and adoption blockers; and name the cheapest decisive experiment and its kill criterion. Promote an opportunity only with an evidence score of at least 3/5, unless the opportunity is to close the evidence gap itself.

### 8. Write the report

Write the report file using the template in the opportunity reference, then give the bottom line in the chat with a link to it. Lead with decision-relevant findings, then coverage and method. Include papers rejected as weak or already implemented.

Before delivering, check that every factual claim has a nearby source you opened; every load-bearing conclusion has two independent sources or is labelled `SINGLE-SOURCE`; numbers, dates and units match the primary source; evidence, author claims, inference and unknowns are visibly distinct; current product, patent and regulatory claims carry an as-of date; blind spots are explicit; and the report, dossiers, corpus, ledger and next-run cursor agree.

### 9. Hand off the next run

End with the next archive band, open verification tasks, monitored papers and opportunities awaiting experiments.

For a daily radar, offer to schedule it. If schedule_create is available, create the repeating task once the person agrees, with an instruction that stands on its own:

> Use the paper-opportunity-radar skill to run today's sweep for <topic>. Resume from the <slug>-radar files in the library; do not restart the corpus. Cover the new delta, the next archive band and open citation or replication follow-ups. Audit the strongest candidates, update every radar file, write today's report and post its bottom line here.

Otherwise give the person that instruction to reuse. Never say monitoring is active until a scheduled task exists.

## Failure handling

- If a source blocks access or rate-limits, log the source and time, use a documented alternative and mark the lane incomplete.
- If metadata conflicts, prefer the publisher or canonical repository for version facts and note the disagreement.
- If full text, code, data or a preregistration is unavailable, lower confidence and name what is missing. Unavailability alone is not evidence of misconduct.
- Never attempt reproductions that need unsafe procedures, protected data, special equipment or credentials; write a bounded verification plan instead.
- If novelty cannot be established, keep the opportunity and label it `PRIOR-ART SEARCH INCOMPLETE`.
- If the baseline is larger than one run, finish one auditable slice, save the cursor and report the backlog.

A run is complete only when the search log is reproducible, new records are deduplicated, selected papers have claim-level dossiers, opportunities have prior-art and feasibility checks, the report is source-grounded, and the next run can resume without rediscovery.
