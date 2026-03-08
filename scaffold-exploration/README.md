# scaffold-exploration

A Cursor skill that **creates or updates** an exploration folder under `_docs/planning/explorations/`. It can guide a discussion and scaffold a new exploration (with a README, feature-set docs, and supporting-docs structure), or update an existing one (add feature sets, align READMEs to standards, add supporting docs and link them to feature sets). It can create a new branch from main and commit when done.

## What it does

**Create flow**

- **Branch (optional):** Asks whether to work on the current branch or a new branch from main. If new branch (or if you're on main), fetches latest main and creates a branch so the exploration isn't committed directly to main.
- **Discussion:** Asks for an exploration name (or suggests one), a global summary, and feature sets with summaries. Groups ideas into logical feature sets.
- **README draft:** Creates the exploration folder and a **top-level** README with: header, skill version, global summary, link to explorations-evaluation, a short "Structure" blurb (feature-sets/ and supporting-docs/), and one section per feature set (heading + summary). Pauses for your approval.
- **Feature docs and structure:** After approval, creates `feature-sets/` with a README and one `.md` file per feature set (Summary, Scope, optional Implementation options / Out of scope), and creates `supporting-docs/` with a README (placeholder until you add assets). Updates the top-level README so each section links to `feature-sets/<file>.md`.
- **Commit:** Adds and commits the new exploration folder (no push unless you ask).

**Update flow**

- **Review:** Lists all files and folders in the exploration and reads existing READMEs.
- **Discuss:** For any file not mentioned in a README, asks whether to add it as a feature set, move it to supporting-docs, or leave as-is. For each supporting doc or folder, asks how it relates to feature sets so the agent can document that (with links) in `supporting-docs/README.md`.
- **Apply:** Adds feature sets, brings READMEs up to standard, adds or updates supporting-docs sections (with links to related feature-set files when you've indicated a relationship), and sets the top-level README to "Updated with" the current skill version.
- **Commit:** Adds and commits the changes.

## Why use it

Use this when you want to start a new exploration in a _docs project or maintain an existing one without manually keeping the folder structure and READMEs consistent. The layout (top-level README, `feature-sets/` with its README and per-feature-set `.md` files, `supporting-docs/` with its README for screenshots and other assets) keeps each exploration traceable to the skill version and makes it clear how supporting docs relate to feature sets.

## How to install

Copy this folder to your Cursor skills directory:

```bash
cp -r scaffold-exploration ~/.cursor/skills/
```

Or, from the repo root: `cp -r cursor-skills/scaffold-exploration ~/.cursor/skills/`

## How to trigger

In Cursor, open the project that has _docs and say something like:

**Create**

- "Create a new exploration in _docs"
- "Add an exploration folder for [topic]"
- "Use scaffold-exploration to add an exploration"
- "Scaffold an exploration in _docs"

**Update**

- "Update an exploration"
- "Add feature sets to [exploration name]"
- "Bring exploration README up to standard"
- "Add screenshots/docs to exploration"

The agent will either run the create flow (branch, name, summary, feature sets, README draft, approval, feature-sets + supporting-docs + commit) or the update flow (review, discuss unmentioned files and supporting-docs ↔ feature sets, apply updates, "Updated with" version, commit).

## Example flow

**Create**

1. **Branch:** You choose current branch or new branch from main; if new (or on main), the agent fetches main and creates a branch.
2. **Phase 1 (Discussion):** Agent asks for exploration name (or suggests one), global summary, and feature sets with summaries.
3. **Phase 2 (README):** Agent creates the exploration folder and top-level README (header, version, global summary, structure blurb, feature-set sections). You review and approve.
4. **Phase 3 (Feature docs and structure):** Agent creates `feature-sets/` (README + one `.md` per feature set) and `supporting-docs/` (README with placeholder), updates the top-level README with links to `feature-sets/*.md`, then adds and commits.

**Update**

1. **Review:** Agent lists contents and reads READMEs.
2. **Discuss:** Agent asks what to do with unmentioned files and how each supporting doc relates to feature sets.
3. **Apply:** Agent adds feature sets, fixes READMEs, updates supporting-docs/README with summaries and links to feature-set files, sets "Updated with" skill version.
4. **Commit:** Agent adds and commits the exploration folder.

After that, you can evaluate the exploration with `_docs/planning/setup/explorations-evaluation.md` or turn it into a milestone.
