# Prompts: Copy-paste for the Claude Code Demo

Run these in order in the same Claude Code session. Each chains through subagents that write files to `research/`, `prd/`, `prd/reviews/`, and `prototype/`.

## Setup

```
cd path/to/vibe-coding-workshop
claude
```

## Step 1: Find evidence

Replace the problem statement with your workshop example.

```
/find-evidence "Parents of kids 4-10 throw out too much food each week"
```

## Step 2: Draft the PRD

```
/draft-prd
```

## Step 3: Three reviewers in parallel

```
/review-prd
```

## Step 4: Apply the review feedback

```
/improve-prd
```

## Step 5: Vibe code the prototype

Default:
```
/vibe-code
```

With visual direction:
```
/vibe-code "mobile-first, feel like Duolingo"
```

With a screenshot as reference (drop the image into the prompt after typing this):
```
/vibe-code "use the attached screenshot as visual direction"
```

## Opening the prototype

```
open prototype/index.html
```

On Linux: `xdg-open prototype/index.html`
On Windows: `start prototype/index.html`

## Iterating after the prototype is built

You do not need a slash command for small changes. Just describe what you want in plain English:

```
Make the home screen use a card layout instead of a list.
```

```
Add a welcome screen before the home screen.
```

```
The quiz feature from the PRD is missing. Add it.
```

```
I want to show a screenshot of the kid's meal history when you tap a name.
```

## If things go sideways

**Re-run any step.** Subagents are idempotent. Running `/find-evidence` twice is safe. It will either overwrite or produce a new version.

**Start over.** Delete the contents of `research/`, `prd/`, and `prototype/`, then re-run from step 1.

**Use a different problem statement.** Everything is parameterized on the problem you pass to `/find-evidence`. The rest of the flow adapts.
