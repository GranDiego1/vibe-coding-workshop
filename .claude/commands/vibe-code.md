---
description: Step 5 of the workshop flow. Builds a working HTML/CSS/JS prototype from the final PRD. Optionally accepts a visual direction or a reference URL.
---

You are running step 5 of the Vibe Coding Workshop flow: building the prototype.

## Step A: Find the PRD

Use Glob with the pattern `prd/prd-v*.md` (NOT `prd/**/*.md`, which would pick up review files). Pick the file with the highest version number. If Glob returns zero matches, tell the user to run the previous steps first and stop.

## Step B: Parse the user's argument

The user may pass an argument:
- **Nothing:** build from scratch using only the PRD.
- **A description or URL:** use it as visual direction (e.g., "mobile-first, like Duolingo" or "match this style: [url]").
- **An image attached to the message:** You (the parent) can see the image. The subagent cannot. If an image is attached, describe its visual direction in 2-3 sentences (layout, color palette, typography, density) and pass that description as text to the subagent.

## Step C: Invoke the vibe-coder subagent

Tell it:
- The path to the latest PRD.
- Any visual direction (as text, never as a raw image reference).
- The output directory: `prototype/`.

The vibe-coder has Write, Edit, and Bash. It will produce a single `prototype/index.html` (or split into index.html, style.css, script.js if needed).

## Step D: Report to the user

1. The exact file path.
2. How to open it:
   ```
   open prototype/index.html
   ```
   (macOS. On Linux: `xdg-open prototype/index.html`. On Windows: `start prototype/index.html`.)
3. Which P0 CUJs the prototype implements and, if relevant, which it does not and why.
4. One suggested next iteration (a specific change the PM could ask for in the next prompt).

## Step E: Iterating after the prototype is built

If the user says "change X" or "make it do Y" after seeing the prototype, you do not need to invoke the subagent again for small iterations. Edit the files directly. Keep the prototype runnable by double-clicking at all times.

For larger pivots (new CUJ, new screen, reshape of the flow), re-invoke the vibe-coder subagent with the updated direction.

## What not to do

- Do not add a build step. No npm, no webpack, no package.json.
- Do not depend on external services the user has to sign up for.
- Do not break the "double-click to open" property. Keep everything self-contained in `prototype/`.
- Do not pass images to the subagent. The subagent cannot see them. Convert to a text description first.
