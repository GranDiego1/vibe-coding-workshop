# Runbook: The Claude Code Section

This is the step-by-step for the Claude Code portion of the Vibe Coding Workshop. Run it live in front of students. Every step is a single slash command that chains work through subagents and writes results to files students can see.

> **Reading solo?** If you are reading this to try the flow yourself (not teaching), skip the blocks marked **[Say to students]**. Everything else applies.

## Glossary

- **CUJ:** Critical User Journey. A single user's goal written as "as a [user], I want to [action]." Prioritized P0 (must have), P1 (next release), P2 (someday).
- **Subagent:** A specialized Claude with its own system prompt and tool access. Defined in `.claude/agents/*.md`. Invoked by a slash command or by the parent Claude.
- **Frontmatter:** The YAML block at the top of a markdown file (between `---` lines). Controls how Claude Code reads the file.

## Pre-flight checklist

Run through this 15 minutes before the demo starts.

- [ ] **Claude Code is installed and up to date.** Run `claude --version` in a terminal. If it prompts you to update, update.
- [ ] **You're signed in.** Run `claude` in any folder. If it asks you to log in, log in.
- [ ] **WebSearch and WebFetch are enabled.** These are on by default for Claude Pro. If `/find-evidence` returns "no web access," check your settings.
- [ ] **You cloned the repo fresh.** A clean repo is the safest demo state. Old `research/`, `prd/`, `prototype/` folders from prior runs should be empty (except `.gitkeep` files).
- [ ] **You ran `/find-evidence` once beforehand** with your demo problem statement to confirm it works and to prime any caches. Delete the output file before going live so students see it appear in real time.
- [ ] **Model selection:** Use the most capable model available (Claude Opus). The reviewer agents especially benefit from it.
- [ ] **Internet is solid.** The subagents hit the web. A flaky connection is the #1 demo killer.
- [ ] **Back pocket:** you know where `research/evidence-parents-food-waste-FALLBACK.md` lives in case `/find-evidence` comes back thin during the live demo.

## Before you start the flow

1. Open this folder in Claude Code:
   ```
   cd path/to/vibe-coding-workshop
   claude
   ```
2. Confirm Claude Code sees the commands and agents: type `/` in the Claude Code prompt. You should see `/find-evidence`, `/draft-prd`, `/review-prd`, `/improve-prd`, `/vibe-code` in the menu.
3. Have a problem statement ready. In the workshop, this is the problem the students picked earlier in the day. If you are running this solo, start with "Parents of kids 4-10 throw out too much food each week" so everything in this runbook lines up.

## The five steps

Each step writes artifacts to a folder so students can watch files appear in real time.

### Step 1: Find evidence (~3-5 min)

**What it does:** Searches Reddit, forums, product reviews, news articles, and social media for real posts from real people who have this problem. Writes findings to `research/evidence-[slug].md`.

**Prompt to run:**
```
/find-evidence "Parents of kids 4-10 throw out too much food each week"
```
(Substitute your problem statement.)

**What you should see:** Claude Code tells you it is invoking the `evidence-finder` subagent. The subagent runs WebSearch several times, uses WebFetch on the strongest hits, and writes a structured file to `research/`. When it finishes, the parent Claude reports the three strongest quotes and a strong/moderate/weak rating.

**Expected output file:** `research/evidence-parents-kids-food-waste.md` (or similar, based on slug). The file should have: a summary, direct quotes with sources, patterns, workarounds, counter-evidence, and an evidence-strength rating.

**Talking points while it runs (3-5 minutes):**
- "I didn't tell it which subreddits to search. The subagent's system prompt handles that. Let me show you."
- Open `.claude/agents/evidence-finder.md` in a separate window. Walk through the "Where to look" and "What to collect" sections.
- "This is what a specialist subagent looks like. One job, strong instructions, scoped tools."

**[Say to students]:** "Notice what just happened. I did not tell it where to look. I did not pre-select subreddits. The subagent has a system prompt that tells it how to research a problem, and it chose the sources itself. This is what a specialist subagent looks like."

**If the evidence is thin (fewer than 4 quotes, or the subagent says "weak"):** stop the demo. Either re-run with a sharper problem statement, or use the pre-baked fallback at `research/evidence-parents-food-waste-FALLBACK.md` to keep the flow moving. Tell students you're using the fallback for time reasons and why real evidence matters.

### Step 2: Draft the PRD (~3-5 min)

**What it does:** Reads the PRD template and every evidence file in `research/`, produces a first PRD at `prd/prd-v1.md`.

**Prompt to run:**
```
/draft-prd
```

**What you should see:** The `prd-writer` subagent reads the template, reads all evidence files, and writes `prd/prd-v1.md`. The PRD follows the 8-section structure and every claim ties to a quote or pattern from the research.

**Expected output file:** `prd/prd-v1.md`. Skim it while students watch. Point at sections that echo specific research quotes.

**Talking points while it runs:**
- Open `templates/prd-template.md`. Walk through the 8 sections.
- Open `templates/prd-example-filled.md` for a "good looks like this" view.
- "The template is the structure. The research is the fact base. The PRD is the synthesis."

**[Say to students]:** "Every claim in this PRD cites something from the evidence. That is how you keep a PRD honest. If a PRD makes a claim and there's no evidence for it, either it moves to open questions or it gets cut."

### Step 3: Review the PRD with three personas (~3-8 min)

**What it does:** Runs three reviewer agents in parallel on the PRD: a skeptical senior engineer, a Director of Product, and a senior PM peer. Writes each review to `prd/reviews/engineer-v[N].md`, `director-v[N].md`, `senior-pm-v[N].md`, plus a synthesis.

**Prompt to run:**
```
/review-prd
```

**What you should see:** The parent Claude announces it is calling three Tasks in parallel. It should not call them one-at-a-time. Three separate review files appear in `prd/reviews/` within a few minutes, then a `synthesis-v[N].md` file appears last. If they appear one by one over 15+ minutes, the parent serialized them; stop, and ask it to retry in parallel.

**Expected output files:**
- `prd/reviews/engineer-v1.md`: buildability verdict, top 3 things that break
- `prd/reviews/director-v1.md`: scope verdict, strategic story, what gets cut
- `prd/reviews/senior-pm-v1.md`: overall read, CUJs that could be sharper
- `prd/reviews/synthesis-v1.md`: where they agree, where they disagree, what to answer

**Talking points while it runs (the longest step, 5-8 min):**
- "Parallel is the magic here. Three reviewers, one wait. Same work serially would take three times as long."
- Open `.claude/agents/engineer-reviewer.md`, `.claude/agents/director-reviewer.md`, `.claude/agents/senior-pm-reviewer.md`. Walk through how each one has a different voice, different tool access, different lens.
- "In real life, you wait a week for three reviewers. You get them on a calendar. One of them doesn't read the doc. This takes three minutes and they all actually read."

**[Say to students]:** "This is the move. Instead of sending your PRD to three people and waiting a week, you get three skeptical reads in minutes. The engineer will catch what will break. The director will catch scope creep. The senior PM will tell you how to sharpen it."

### Step 4: Improve the PRD (~2-4 min)

**What it does:** Reads the synthesis and the three reviews, produces `prd/prd-v2.md` with a changelog at the top explaining what changed, what was rejected, and why.

**Prompt to run:**
```
/improve-prd
```

**What you should see:** A new file `prd/prd-v2.md` appears. The top of it has a "Changelog from v1" block. The body has sharper CUJs, tighter scope, or clearer trade-offs. Not every reviewer suggestion should be applied; watch for rejections in the changelog.

**Expected output file:** `prd/prd-v2.md`.

**Talking points while it runs:**
- "Watch for the changelog. A good v2 says 'I accepted this, I rejected that, and here's why.' If it applied every suggestion, something's wrong. The PM is still the owner."
- "The reviews are input, not instructions."

**[Say to students]:** "The PM is still the owner. Notice Claude Code pushes back on the things a good PM would push back on. If a reviewer says 'add this feature' and it contradicts the evidence, the PM rejects it, even if three agents agreed."

Optional: run `/review-prd` again on v2 to show the reviews got shorter and friendlier. This demonstrates the loop working.

### Step 5: Vibe code the prototype (~3-8 min)

**What it does:** Reads the latest PRD, calls the `vibe-coder` subagent, writes a working prototype to `prototype/`. Double-click to open.

**Prompt to run (pick one):**
```
/vibe-code
```
Or with visual direction:
```
/vibe-code "mobile-first, clean like Duolingo, pastel palette, rounded cards"
```
Or with an image:
```
/vibe-code [paste screenshot here]
```
If you paste an image, the parent Claude converts it to a text description before passing to the subagent (subagents cannot see images).

**What you should see:** `prototype/index.html` appears (possibly with `style.css` and `script.js` next to it). Opening it in a browser shows a working UI for the P0 CUJs.

**Expected output file:** `prototype/index.html`.

**Open it in front of students:**
```
open prototype/index.html
```
(On Linux: `xdg-open prototype/index.html`. On Windows: `start prototype/index.html`.)

**Talking points while it runs:**
- "Every P0 CUJ should be clickable. Not beautiful. Clickable. That's the demo bar."
- "No build step. No npm. It's one HTML file you double-click."

**[Say to students]:** "Everything we did in the first four hours, with five different tools, just happened in one conversation. You learn the tools because the tools teach you the shape of the work. Once you know the shape, Claude Code can run the whole thing."

### Step 6: Iterate in the same session

Once the prototype is open, keep going. Claude Code already has the PRD and the prototype in context. Edits are fast.

**Good iteration prompts are specific:**
- "On the shopping list screen, group items by aisle. Keep the three-section split."
- "Add a welcome screen before the home screen. One sentence of copy, a big button."
- "The weekly summary is missing. Add it between the log and the shopping list."

**Bad iteration prompts are vague:**
- "Make it better." (Better how?)
- "Improve the design." (Which screen? What changes vs. what stays?)
- "Add more stuff." (No.)

**Rule of thumb:** name the screen, say what changes, say what stays. Claude Code will edit the files directly for small changes and re-invoke the vibe-coder subagent for large pivots.

## Timing

Rough target for the full demo: **25-40 minutes.** Longer if the Q&A in each step is rich. The commands themselves take 3-8 minutes each because the subagents do real work.

## Troubleshooting

**`claude: command not found`**
- Claude Code isn't installed or isn't on your PATH. Reinstall from the install guide (see README.md), then open a new terminal.

**Typing `/` shows no commands**
- You are not in the `vibe-coding-workshop` folder. Check with `pwd`. Exit Claude Code, `cd` to the repo root, relaunch `claude`.
- `.claude/commands/` is missing. Check that you cloned the full repo, not a shallow copy.

**A subagent errors out**
- Re-run the same command. Subagents are idempotent.
- If it errors again with a web error, check your internet. WebSearch and WebFetch fail silently on flaky connections.

**The PRD draft is thin or empty**
- Check that `research/` has content. If it does not, the PRD step got no input. Re-run `/find-evidence`.
- Check that evidence files are named `evidence-*.md`. The PRD writer globs that pattern; a file named something else will be ignored.

**The review step took a long time and reviews appeared one by one**
- The parent Claude serialized the Task calls instead of parallelizing. Not critical, just slower. If you want to re-run, delete the `prd/reviews/*-v1.md` files first.

**The prototype is a white screen**
- Open DevTools (Cmd-Option-I on macOS). Look for a red console error. Usually a typo in a selector or a missing file.
- Ask Claude Code: "The prototype shows a white screen. Here's the console error: [paste]. Fix it."

**The prototype looks nothing like what I asked for**
- Be more specific next time. Name the screen, name the visual reference, name what stays.
- If a full pivot is needed, say "scrap this and rebuild from the PRD with [new direction]." Claude Code will re-invoke the vibe-coder subagent.

**Context is filling up (Claude warns about context)**
- You're deep in iteration. Start a new Claude Code session in the same folder. It re-reads `CLAUDE.md`, the PRD, and the prototype from disk; you don't lose the work.

## What to emphasize across all steps

- **The subagents have system prompts.** Students can read them in `.claude/agents/`. Every behavior they are seeing is encoded in those files.
- **The commands are thin wrappers** around the subagents. Students can read them in `.claude/commands/`.
- **The entire folder is version-controlled and shareable.** A team can adopt this flow by copying `.claude/` into their own repo.
- **Nothing is magic.** Everything is a file, a prompt, and a well-chosen tool call.
