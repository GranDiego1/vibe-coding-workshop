---
description: Step 3 of the workshop flow. Runs three reviewers in parallel (skeptical engineer, director of product, senior PM) on the latest PRD, then synthesizes their findings.
---

You are running step 3 of the Vibe Coding Workshop flow: the PRD review.

## Step A: Find the latest PRD

Use Glob with the pattern `prd/prd-v*.md` (NOT `prd/**/*.md`, which would pick up review files). Pick the file with the highest version number. Extract the version number as `[N]`.

If Glob returns zero matches, tell the user to run `/draft-prd` first and stop.

## Step B: Fire three reviewers in parallel

**Critical: all three Task tool calls MUST be in a single assistant message. Do not call one, wait, and then call the next. Parallelism is the whole point. Serializing triples the wall-clock time.**

Invoke:

1. `engineer-reviewer` (skeptical senior engineer). Tell it: "Review the PRD at `prd/prd-v[N].md`. Save your review to `prd/reviews/engineer-v[N].md`. Use the output format in your system prompt."
2. `director-reviewer` (Director of Product). Tell it: "Review the PRD at `prd/prd-v[N].md`. Save your review to `prd/reviews/director-v[N].md`. Use the output format in your system prompt."
3. `senior-pm-reviewer` (senior PM peer). Tell it: "Review the PRD at `prd/prd-v[N].md`. Save your review to `prd/reviews/senior-pm-v[N].md`. Use the output format in your system prompt."

Each agent has Write access and will save its own review.

## Step C: Synthesize

After all three return, read the three saved review files. Write a synthesis to `prd/reviews/synthesis-v[N].md` using this structure:

```
# Review Synthesis

**Document reviewed:** prd/prd-v[N].md
**PRD version:** v[N]
**Date:** [today's date]

## Where all three agree
The findings that showed up in more than one review. Most critical first. These are the things the PM cannot ignore.

## Where they disagree
When two reviewers pull in opposite directions, the PM has a real decision to make. Surface those tensions plainly.

## Each reviewer's top callout
- **Engineer:** [one line, the single thing that would most change how this gets built]
- **Director:** [one line, the single thing that would most change whether this ships]
- **Senior PM:** [one line, the single thing that would most strengthen the doc]

## Three questions the PM should answer before the next version
[Pick the three most important unanswered questions across all reviews.]
```

## Step D: Report to the user

1. Where the individual reviews and the synthesis were saved.
2. The top three "where all three agree" findings, one line each.
3. The three questions to answer next.

Do not soften the findings. If the reviews are harsh, the report is harsh. The PM asked for a review, not reassurance.

## Suggest the next step

End with: "Next step: `/improve-prd`. This applies the review feedback and produces the next PRD version."
