# Vibe Coding Workshop

Claude Code scaffolding for the AI Product Management with Vibe Coding workshop, co-taught by [Diego Granados](https://www.linkedin.com/in/diegogranadosh) and [Marily Nika](https://www.linkedin.com/in/marilynika) on [Maven](https://maven.com/marily-nika/ai-product-management-vibe-coding-certification/).

## What this is

Five slash commands that take a product manager from a problem hunch to a working prototype, end to end, in a single Claude Code session.

```
/find-evidence "Parents of kids 4-10 throw out too much food each week"
/draft-prd
/review-prd
/improve-prd
/vibe-code
```

Each command invokes a specialized **subagent** (a Claude with its own system prompt and tool access, defined in `.claude/agents/*.md`). Each subagent writes its output to a folder in this repo so you can see the work product.

## What you get

1. **Evidence research** from Reddit, forums, product reviews, and news. No fake data. The subagent uses WebSearch and WebFetch to find real posts from real people.
2. **A PRD** written from that evidence using an 8-section template (Problem, Evidence, Goals, Solution, CUJs, MVP Scope, Requirements, Risks).
3. **Three parallel reviews** of the PRD by a skeptical senior engineer, a Director of Product, and a senior PM peer. Plus a synthesis of where they agree, where they disagree, and what to answer next.
4. **An improved PRD version** with a changelog explaining what was applied from the reviews and what was rejected.
5. **A working HTML/CSS/JS prototype** of the P0 CUJs (Critical User Journeys, the must-have flows). No build step. Double-click to open.

## Three ways to use this

The slash commands are the fastest path, but they are not the only way. Pick the level that matches how much you want to trust vs. steer the flow.

### Method 1: Slash commands (one-shot)

Just type the command. The prompt, the subagents, and the output path are all wired up. Fast, repeatable, best for demos and teams that want a consistent output.

```
/find-evidence "Parents of kids 4-10 throw out too much food each week"
/draft-prd
/review-prd
/improve-prd
/vibe-code
```

### Method 2: Load the skill, then direct it

Ask Claude Code to load the skill by name and follow it, instead of typing the slash command. Useful when you want to tweak something mid-flow, or when you want students to see that the skill is just a prompt Claude Code reads and runs.

```
Load the find-evidence skill and run it for "Parents of kids 4-10 throw out too much food each week."

Load the draft-prd skill.

Load the review-prd skill.

Load the improve-prd skill.

Load the vibe-code skill.
```

You can redirect mid-flow, e.g., "Load the draft-prd skill, but emphasize the weekend-scheduling CUJ." You get the structure of the skill without being locked into its defaults.

### Method 3: No skill at all, write the prompt yourself

Skip the skill file entirely. Describe what you want Claude Code to do in plain English for each step. This is the most flexible and the best way to internalize what the skills are doing under the hood.

**Step 1 (instead of /find-evidence):**
```
Search Reddit, forums, product reviews, and news for real posts from parents of kids 4-10 talking about food waste. Find 8-12 quotes from real people. Save the findings to research/ in a structured markdown file with direct quotes, sources, patterns, workarounds, and counter-evidence. Tell me how strong the evidence is.
```

**Step 2 (instead of /draft-prd):**
```
Read the evidence file in research/. Write a PRD with these sections: Problem & User, Evidence, Goals & Success Metrics, Solution Overview, Key CUJs (as a user I want to...), MVP Scope, Trade-offs, Risks & Open Questions. Save it to prd/prd-v1.md. Every claim must cite a quote from the evidence.
```

**Step 3 (instead of /review-prd):**
```
Use three subagents in parallel to review the PRD at prd/prd-v1.md: a skeptical senior engineer (buildability), a Director of Product (scope and strategy), and a senior PM peer (clarity and sharpness). Save each review to prd/reviews/, then write a synthesis of where they agree and disagree.
```

**Step 4 (instead of /improve-prd):**
```
Read the three reviews and the synthesis. Apply the findings that are valid. Push back on the ones that contradict the evidence. Write prd/prd-v2.md with a changelog at the top explaining what changed and what was rejected.
```

**Step 5 (instead of /vibe-code):**
```
Read prd/prd-v2.md. Build a working HTML/CSS/JS prototype in prototype/ that demonstrates every P0 CUJ. One file preferred. No build step. Runs by double-clicking index.html.
```

The output quality depends on how well you write the prompt. The skill is just this prompt, pre-written and reusable.

**Workshop recommendation:** start with Method 1 to see the flow end to end. Once you understand what each step does, drop into Method 2 or 3 when you want to adapt the flow to a different problem, a different PRD format, or a different team's voice.

## How to run

1. **Clone this repo:**
   ```
   git clone https://github.com/GranDiego1/vibe-coding-workshop.git
   cd vibe-coding-workshop
   ```

2. **Install Claude Code.** On macOS and Linux:
   ```
   curl -fsSL https://claude.ai/install.sh | bash
   ```
   On Windows: see the install page at claude.ai/install. If curl doesn't work on a locked-down machine, the Homebrew cask (`brew install --cask claude-code`) is the fallback.

3. **Sign in.** First time you run `claude`, it will open a browser to log you into your Anthropic account. You need Claude Pro ($20/month, or $17/month billed annually) or higher.

4. **Open this folder in Claude Code:**
   ```
   claude
   ```
   (Run it from inside the `vibe-coding-workshop` folder.)

5. **Confirm the commands are loaded.** Type `/` at the Claude Code prompt. You should see `/find-evidence`, `/draft-prd`, `/review-prd`, `/improve-prd`, `/vibe-code` in the list.

6. **Run the five commands in order.** See `docs/PROMPTS.md` for the exact inputs, or `docs/RUNBOOK.md` for the full live-demo walkthrough with timing and troubleshooting.

## Glossary

- **CUJ:** Critical User Journey. A single user's goal written as "as a [user], I want to [action]." Prioritized P0 (must have), P1 (next release), P2 (someday).
- **Subagent:** A specialized Claude with its own system prompt and tools. Defined in `.claude/agents/*.md`. Invoked by a slash command or by the parent Claude.
- **Slash command:** A reusable prompt kicked off by typing `/command-name`. Defined in `.claude/commands/*.md`.
- **Frontmatter:** The YAML block at the top of a markdown file (between `---` lines). Controls how Claude Code reads the file.

## Folder structure

```
.claude/
  agents/              Six specialized subagents
  commands/            Five slash commands
  settings.json        Permission allowlist (prevents demo prompts)
templates/
  prd-template.md      The 8-section PRD template (empty)
  prd-example-filled.md  A fully filled-in example PRD for reference
docs/
  RUNBOOK.md           Live demo walkthrough with timing + troubleshooting
  PROMPTS.md           Copy-paste prompts
research/              Evidence output (plus a fallback file for live demos)
prd/                   PRD drafts
prd/reviews/           Reviewer output + synthesis
prototype/             HTML/CSS/JS prototype
CLAUDE.md              What Claude Code reads when it opens this repo
```

## Adapting it for your own team

The flow is not specific to the workshop. It works for any PM workflow where the shape is: find evidence → draft → review → iterate → prototype. To adapt:

1. Copy the `.claude/` folder into your own repo.
2. Edit `templates/prd-template.md` to match your team's PRD format.
3. Edit the reviewer agents in `.claude/agents/` to match the voices and biases of your actual reviewers.
4. Edit `.claude/agents/evidence-finder.md` if your evidence sources are different (e.g., Jira, Zendesk, interview transcripts instead of Reddit).

## License

MIT. Use it, change it, teach with it, ship with it.
