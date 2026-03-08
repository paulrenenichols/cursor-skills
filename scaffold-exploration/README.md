# scaffold-exploration

A Cursor skill that creates a **new exploration folder** under `_docs/planning/explorations/`: it guides a discussion, drafts a README with feature-set sections and summaries (plus skill version at the top), then after your approval creates per-feature markdown files and adds links in the README. It can also create a new branch from main and commit the scaffolded exploration when done.

## What it does

- **Branch (optional):** Asks whether to work on the current branch or a new branch from main. If new branch (or if you're on main), fetches latest main and creates a branch so the exploration isn't committed directly to main.
- **Discussion:** Asks for an exploration name (or suggests one from the discussion), a global summary, and feature sets with summaries. Groups ideas into logical feature sets.
- **README draft:** Creates `_docs/planning/explorations/<name>/README.md` with: top-line header, skill version, global summary, optional link to explorations-evaluation, and one section per feature set (heading + summary). Pauses for your approval.
- **Feature docs:** After approval, creates one `.md` file per feature set (Summary, Scope, optional Implementation options / Out of scope), then updates the README so each section links to its file.
- **Commit:** Adds and commits the new exploration folder to the current branch (no push unless you ask).

## Why use it

Use this when you want to start a new exploration in a _docs project without manually creating the folder structure and README. The sectioned README (header, version, global summary, then sections with summaries and links) keeps each exploration consistent and traceable to the skill version.

## How to install

Copy this folder to your Cursor skills directory:

```bash
cp -r scaffold-exploration ~/.cursor/skills/
```

Or, from the repo root: `cp -r cursor-skills/scaffold-exploration ~/.cursor/skills/`

## How to trigger

In Cursor, open the project that has _docs and say something like:

- "Create a new exploration in _docs"
- "Add an exploration folder for [topic]"
- "Use scaffold-exploration to add an exploration"
- "Scaffold an exploration in _docs"

The agent will ask about branch, name, summary, and feature sets, then draft the README and wait for your approval before creating the feature docs and committing.

## Example flow

1. **Branch:** You choose current branch or new branch from main; if new (or on main), the agent fetches main and creates a branch.
2. **Phase 1 (Discussion):** Agent asks for exploration name (or suggests one), global summary, and feature sets with summaries.
3. **Phase 2 (README):** Agent creates the exploration folder and README (header, version, global summary, sections). You review and approve.
4. **Phase 3 (Feature docs):** Agent creates one markdown file per feature set and adds links in the README, then adds and commits to the branch.

After that, you can evaluate the exploration with `_docs/planning/setup/explorations-evaluation.md` or turn it into a milestone.
