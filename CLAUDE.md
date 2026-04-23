# Vibe Coding Workshop: Claude Code Brain

## What this repo is

This is the Claude Code scaffolding for the AI Product Management with Vibe Coding workshop. It takes a product manager from "I have a hunch there is a problem here" to "I have a working prototype" in five slash commands.

## Glossary (for anyone new reading this repo)

- **CUJ:** Critical User Journey. "As a [user], I want to [action]." P0 = must have for MVP, P1 = next release, P2 = someday.
- **Subagent:** A specialized Claude with its own system prompt and tool access. Defined in `.claude/agents/*.md`. Six of them in this repo.
- **Slash command:** A reusable prompt invoked by typing `/command-name`. Defined in `.claude/commands/*.md`. Five of them.
- **Frontmatter:** The YAML block at the top of a markdown file (between `---` lines).

## How to use it

Five commands, in order. Each writes files to a dedicated folder so students can watch the work happen.

```
/find-evidence "<problem statement>"
/draft-prd
/review-prd
/improve-prd
/vibe-code
```

See `docs/RUNBOOK.md` for what each step does live in front of students. See `docs/PROMPTS.md` for copy-paste prompts.

## Folder layout

```
.claude/
  agents/       Six specialized subagents, one per job
  commands/     Five slash commands that invoke the subagents
templates/
  prd-template.md       The 8-section PRD structure used by all demos
  prd-example-filled.md  A fully filled-in reference PRD (food-waste example)
docs/
  RUNBOOK.md    Step-by-step for running the live demo
  PROMPTS.md    Copy-paste prompts
research/       Where /find-evidence writes (plus evidence-parents-food-waste-FALLBACK.md for demo safety)
prd/            Where /draft-prd and /improve-prd write
prd/reviews/    Where /review-prd writes (three reviews + synthesis per PRD version)
prototype/      Where /vibe-code writes
```

## Rules for anything Claude Code writes inside this repo

1. **Every PRD claim must trace to evidence.** If the research does not support it, either cut it or move it to section 8 (Open Questions). Do not invent data.
2. **Reviews are blunt.** No softening. The PM asked for a review, not reassurance.
3. **The prototype is runnable.** No build step, no npm install, no dependencies. Double-click `prototype/index.html` and it works.
4. **No em dashes in any written output.** Use commas, periods, or restructure.
5. **No filler words.** No "leverage," "seamless," "unlock," "dive into," "robust," "comprehensive," "here's the thing."
6. **Iterate, do not reset.** When the user asks for a change to the prototype, edit the files. Do not rebuild from scratch unless they say "start over."

## The subagents

- **evidence-finder**: searches Reddit, forums, reviews, articles for real evidence of a problem.
- **prd-writer**: writes the PRD using the template and the evidence.
- **engineer-reviewer**: skeptical senior engineer's read on the PRD.
- **director-reviewer**: Director of Product's read on the PRD.
- **senior-pm-reviewer**: peer senior PM's constructive suggestions on the PRD.
- **vibe-coder**: builds the HTML/CSS/JS prototype from the PRD.

Read each `.claude/agents/*.md` file to see the full prompt. Students should be encouraged to open them and read. They are not black boxes.

## What this repo is not

- Not a tutorial on Claude Code itself. Students should already be able to install it and get past the first prompt by the time they use this repo.
- Not a production PRD framework. It is workshop-sized. Real PRDs for real products will be bigger.
- Not an AI product template. The PRD template is deliberately general so it works whether or not the solution uses AI.
