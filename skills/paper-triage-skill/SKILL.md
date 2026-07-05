---
name: paper-triage-skill
description: Use when a user provides paper PDFs, paper text, titles, abstracts, DOI lists, candidate reading lists, or a research direction and needs a first-pass literature triage workflow. This skill turns a pile of candidate papers into an actionable reading queue, classifies papers as Deep read, Skim, Park, or Skip, recommends where to start reading, and lists source-verification items. Use for graduate reading, group meeting preparation, thesis opening, literature review scouting, method search, Obsidian note preparation, and handoff to deeper paper reading. Do not use it to fabricate literature reviews, replace full-text verification, or make unsupported academic claims.
---

# Paper Triage Skill

Turn a paper pile into a reading queue before deep reading.

Default to Chinese unless the user asks for another language.

## Core promise

Help the user make the first reading decision:

- which papers deserve deep reading now;
- which papers only need a quick skim;
- which papers should be saved for later;
- which papers can be skipped for the current task.

The output is a reading queue, not a final literature review.

## Public metaphor

Use this metaphor when it helps the user understand the workflow:

> AI Watson organizes the case file before the real investigation begins.

In Chinese:

> AI华生先整理案卷，把论文堆变成阅读队列；真正值得深挖的论文，再交给后续精读流程。

Do not overuse the metaphor if the user asks for a direct academic output.

## Input handling

Proceed when the user provides enough information to make a useful first pass. Ask only for missing information that materially affects triage.

Useful inputs:

- paper PDF, pasted paper text, title, abstract, DOI, PMID, or citation;
- the user's research direction or current question;
- the current task: group meeting, thesis opening, literature review, method search, course project, or topic scouting;
- available reading time;
- expected downstream output: reading notes, group meeting, PPT, Obsidian cards, or deep-reading report.

If the user provides a folder or many PDFs, first ask whether titles and abstracts are available. If PDFs are already available and metadata extraction is easy in the environment, extract lightweight metadata first. Do not deep-read every PDF by default.

## Workflow

Use the lightest workflow that fits the request.

1. Clarify the user's current task and research direction.
2. Build a quick paper inventory from titles, abstracts, keywords, citations, or PDF metadata.
3. Classify each paper as `Deep read`, `Skim`, `Park`, or `Skip`.
4. Recommend reading effort: `Full paper`, `Key sections`, `Abstract first`, or `Save for later`.
5. Explain the reason in one concrete sentence.
6. Tell the user where to start: abstract, introduction, methods, results, figures, tables, limitations, or discussion.
7. List what must be checked in the original paper.
8. Summarize the final reading queue.
9. If useful, hand off selected papers to group meeting preparation, Obsidian cards, or deep reading.

## Output: batch triage table

For multiple papers, output this table:

| # | Paper | Topic fit | Recommended action | Reading effort | Why | Start with | Must verify |
|---|---|---|---|---|---|---|---|
| 1 | title | High / Medium / Low / Unclear | Deep read / Skim / Park / Skip | Full paper / Key sections / Abstract first / Save for later | concrete reason | section / figure / table | source-check item |

Use short reasons. The table should help the user act, not bury them in a review article.

After the table, include a short reading queue:

```markdown
## Reading queue

1. Deep read:
2. Skim:
3. Park:
4. Skip:
```

## Action labels

Use these labels consistently:

- `Deep read`: directly relevant to the current task and likely worth full-text reading.
- `Skim`: useful background, method context, or adjacent reference, but not the first priority.
- `Park`: potentially useful later; save it but do not spend serious attention now.
- `Skip`: currently low relevance, duplicate, inaccessible, or too weak for the task.

Use these reading effort labels:

- `Full paper`: worth full-text reading.
- `Key sections`: read selected sections, figures, or tables first.
- `Abstract first`: do not go beyond metadata/abstract unless the user's task changes.
- `Save for later`: keep the citation but do not read it now.

## Paper card

For papers worth keeping, create a short card:

```markdown
# Paper Card

- title:
- source:
- user_task:
- recommended_action: Deep read / Skim / Park / Skip
- reading_effort: Full paper / Key sections / Abstract first / Save for later
- first_pass_confidence: high / medium / low

## One-sentence topic
-

## Why it matters for this task
-

## What to read first
- abstract:
- introduction:
- methods:
- results:
- figures/tables:

## Useful for
- group meeting:
- thesis opening:
- method borrowing:
- background:

## Must verify in the original paper
1.
2.
3.
```

## Group meeting handoff

If the user is preparing a group meeting, add:

- top papers to deep read;
- 3-5 sections or figures to inspect first;
- possible advisor questions;
- what is safe to put on slides only after original-paper verification;
- what should not be claimed yet.

## High-level triage heuristics

Prioritize a paper when:

- it directly matches the user's research question;
- it can help with a near-term deliverable;
- its method, dataset, evaluation, or figure design may be borrowed or adapted;
- it clarifies a mainstream route, key debate, or important limitation;
- it gives the user a better starting point for group meeting or thesis planning.

Lower priority when:

- it is only loosely related;
- it is general background and not urgent;
- it duplicates stronger papers in the list;
- extraction quality is poor and the current task does not justify recovery effort;
- claims cannot be checked from the provided material.

Do not expose or invent numeric scoring weights unless the user explicitly asks for a custom scoring sheet.

## Verification reminders

Always separate:

- what the paper appears to claim;
- what evidence has actually been provided;
- what still needs original-paper verification;
- what is first-pass inference.

Common verification items:

- exact sample size;
- experimental conditions;
- dataset source;
- key numerical results;
- figure and table captions;
- whether the paper is review, method, dataset, or original experimental study;
- limitations and failure cases;
- whether a conclusion is author-stated or evidence-supported.

## Style

Be direct, practical, and calm.

Prefer:

> 这篇可以先略读。它和你的方向有关，但目前更像背景材料，不是最该进入精读队列的核心文献。

Prefer:

> 这篇值得进入精读队列，但关键结果和图表解释必须回原文核对。

Avoid:

> 本文具有重大创新意义，并对领域发展产生深远影响。

Do not use grand academic praise unless the provided evidence supports it and the user asks for formal writing.

## Safety boundary

This skill helps with reading priority. It does not:

- replace full-text reading;
- replace citation checking;
- write fabricated literature reviews;
- support academic dishonesty;
- claim a paper has evidence that was not provided;
- guarantee that the triage decision is correct.

When evidence is incomplete, say so plainly.
