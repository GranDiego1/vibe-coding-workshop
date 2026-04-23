---
description: Step 1 of the workshop flow. Searches Reddit, forums, reviews, and news for evidence that a user problem is real. Pass the problem statement as the argument.
---

You are running step 1 of the Vibe Coding Workshop flow: evidence research.

## Input

The user will pass a problem statement as the argument. For example: "Parents of kids 4-10 throw out too much food each week" or "Remote designers struggle to get feedback on early-stage work."

If no argument was passed, ask the user to describe the problem in one sentence before continuing. Do not proceed until you have a problem statement.

## What to do

Invoke the `evidence-finder` subagent with the problem statement. The agent will search Reddit, forums, product reviews, news articles, and social media to find real evidence that this problem exists, then save its findings to `research/evidence-[slug].md`.

Do not do the research yourself. The subagent is scoped and tuned for this job.

## Fallback for the live workshop

If the subagent comes back with thin results (fewer than 4 quotes, or the strength-of-evidence rating is "weak"), tell the user and offer two paths:
1. Re-run `/find-evidence` with a sharper problem statement.
2. If time is short (e.g., live demo), suggest using the pre-baked fallback at `research/evidence-parents-food-waste-FALLBACK.md` for continuity. Note this is for continuity only, not a substitute for real evidence on the user's actual problem.

## When the subagent returns

Use Glob on `research/evidence-*.md` to confirm the file was written. Read it. Then tell the user, in plain language:

1. Where the evidence was saved (full path).
2. The three strongest findings (direct quotes or patterns, with sources).
3. How strong the evidence is overall. Use the subagent's own assessment. Strong / moderate / weak.
4. Whether this problem looks worth building for. Your honest read. If the evidence is thin, say so.

Do not copy the whole research file into chat. Point the user at the file and highlight what matters.

## Suggest the next step

End with: "Next step: `/draft-prd`. This will turn the evidence into a PRD draft using the workshop template."
