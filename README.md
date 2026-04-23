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
