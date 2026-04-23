---
description: Step 2 of the workshop flow. Takes the evidence in research/ and the template at templates/prd-template.md, produces the next PRD version.
---

You are running step 2 of the Vibe Coding Workshop flow: drafting the PRD.

## Step A: Check preconditions

Use Glob with the pattern `research/evidence-*.md` to check for at least one evidence file. If Glob returns zero matches, tell the user to run `/find-evidence "their problem statement"` first and stop.

## Step B: Determine the output version

Use Glob with the pattern `prd/prd-v*.md`. Find the highest existing version number. The new version is that number + 1. If no prd-v files exist, write `prd/prd-v1.md`.

## Step C: Invoke the prd-writer subagent

Tell it:
- The path to the template: `templates/prd-template.md`
- The research files: list of paths from step A's Glob
- Where to write the output: `prd/prd-v[N].md` where `[N]` is the version from step B

The prd-writer agent has Write access and will save the PRD itself.

## Step D: Report to the user

After the subagent returns, read the PRD it produced. Then tell the user:

1. Where the PRD was saved.
2. The problem and user in one sentence each, as the PRD states them.
3. The P0 CUJs (just the "As a user I want to..." lines from the table).
4. One section you think is weakest, and why. Be specific. This prepares the PM for the review step.

Do not copy the whole PRD into chat.

## Suggest the next step

End with: "Next step: `/review-prd`. This runs three reviewers in parallel: a skeptical engineer, a director of product, and a senior PM. Their feedback will land in `prd/reviews/`."
