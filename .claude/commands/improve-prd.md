---
description: Step 4 of the workshop flow. Applies the review findings to the PRD and produces the next version. Does not blindly accept every reviewer comment.
---

You are running step 4 of the Vibe Coding Workshop flow: improving the PRD based on reviewer feedback.

## Step A: Find inputs

1. Use Glob with `prd/prd-v*.md` to find the latest PRD. Extract its version as `[N]`.
2. Use Glob with `prd/reviews/synthesis-v*.md` to find the latest synthesis. Its version should also be `[N]`.

If either glob returns zero, tell the user what to run first:
- No PRD: `/draft-prd`
- No synthesis: `/review-prd`

If versions do not match (e.g., PRD is v2 but synthesis is only v1), tell the user the reviews are stale and recommend rerunning `/review-prd` on the current PRD.

## Step B: Read all inputs

Read in order:
- `prd/prd-v[N].md`
- `prd/reviews/synthesis-v[N].md`
- `prd/reviews/engineer-v[N].md`
- `prd/reviews/director-v[N].md`
- `prd/reviews/senior-pm-v[N].md`

## Step C: Produce the improved PRD

Write the new PRD to `prd/prd-v[N+1].md`.

Do not blindly accept every finding. Judgment matters.

- **Where all three reviewers agree:** apply the fix.
- **Where reviewers disagree:** choose the side you believe, briefly explain why in the changelog, do not pretend the tension does not exist.
- **Where a reviewer's suggestion would weaken the PRD:** ignore it and note why in the changelog.
- **Where a reviewer asked a question you cannot answer from the evidence:** add it to section 8 (Risks & Open Questions) rather than inventing an answer.

## Step D: Add a changelog

At the top of the new PRD file (right under the H1 title but above section 1), add:

```
## Changelog (v[N+1])

**Applied from review synthesis:**
- [Change 1. Reference which reviewer flagged it.]
- [Change 2.]
- [Change 3.]

**Rejected:**
- [Suggestion we did not apply, and why.]

**Moved to open questions:**
- [Question we could not answer from evidence, added to section 8.]
```

## Step E: Report to the user

Tell the user:
1. Where the new PRD was saved.
2. The three biggest changes, one line each.
3. Anything you pushed back on, with a one-line reason.

## Suggest the next step

End with: "Next step: `/review-prd` again for another pass, OR `/vibe-code` to build a working prototype from this version of the PRD."
