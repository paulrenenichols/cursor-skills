---
name: scaffold-exploration
version: "1.0.0"
description: Prompts a discussion to create a new exploration folder under _docs/planning/explorations/, drafts a README with feature-set sections and skill version, then after approval creates per-feature markdown files and updates the README with links. Use when adding a new exploration to a _docs project or when the user wants to explore a set of features in a structured way.
---

# Scaffold a new exploration

Use this skill when the user wants to create a **new exploration folder** under `_docs/planning/explorations/` in a project that already has _docs: discuss features, draft a README with sections and summaries, then after approval create per-feature markdown files and add links. The project must have (or will get) `_docs/planning/explorations/` and ideally `_docs/planning/setup/explorations-evaluation.md` (from scaffold-docs or added separately).

## When to use

- User wants to add a new exploration to a _docs project.
- User says "create an exploration", "add an exploration folder", "scaffold an exploration in _docs", or references this skill by name.
- Do **not** use for evaluating an existing exploration or turning it into a milestone (use the project's `explorations-evaluation.md` instead).

---

## Branch and commit (before Phase 1 and after Phase 3)

**Before creating any files**, ask the user:

> Should this exploration be created on the **current branch**, or on a **new branch from main**?

- **If new branch from main:** In the **current project** (the _docs project where the exploration will live), run `git fetch origin` (or `git fetch origin main`), then create and checkout a new branch from `origin/main`. Use a branch name like `explore/<exploration-name>` once the exploration name is known, or `explore/new-exploration` if you create the branch before the name is decided.
- **If current branch is main:** Treat like "new branch"—fetch latest main, then create and checkout a new branch from `origin/main` so the exploration is not committed directly to main.
- **If current branch and not main:** Proceed on the current branch; no fetch or new branch.

**When scaffolding is complete** (after Phase 3): In the project repo, run `git add` for the new exploration folder and any new files, then `git commit` with a clear message (e.g. `Add exploration: <name>` or `Scaffold exploration <name> with scaffold-exploration skill`). Do not push unless the user asks.

---

## Phase 1 – Discussion

1. **Confirm** the project has `_docs/planning/explorations/` (create it if missing: `_docs/planning/explorations/`).

2. **Exploration name:** Ask for a name used as the folder name (e.g. `developer-experience`). You may **suggest** a kebab-case name based on the features or theme discussed (e.g. "developer-experience", "export-pdf") for the user to approve or change. If the user hasn't given a name by the time you draft the README, suggest one before creating the folder.

3. **Ask for:**
   - **What this exploration is about** — One short paragraph (global summary).
   - **Feature sets to explore** — For each, a short name and a summary (what we're exploring and why). Group fine-grained ideas into logical feature sets (e.g. "API docs", "DB UI", "Docker dev"); do not create a separate file for every small idea.

4. Do not create exploration files yet; only capture intent. (Branch setup may already be done if the user chose a new branch.)

---

## Phase 2 – Draft README and pause

1. Create `_docs/planning/explorations/<exploration-name>/README.md` with **this order**:

   - **Top-line header** — Single H1 (e.g. `# Developer experience`).
   - **Skill version** — One line: `Created with the **scaffold-exploration** skill (vX.Y.Z).`  
     Read the version from this skill's SKILL.md frontmatter (`version` field). If the skill is loaded from `~/.cursor/skills/scaffold-exploration/`, open that path; otherwise use the skill file in context.
   - **Global summary** — One short paragraph describing the work being done in this exploration (from the discussion).
   - **Optional:** Link to explorations-evaluation:  
     `Use [explorations-evaluation.md](../../setup/explorations-evaluation.md) to evaluate this exploration or turn it into a milestone.`
   - **Sections for each feature set** — One `## <Feature set name>` per feature set, each with a short **summary paragraph**. Do not add links yet (the per-feature files do not exist yet).

2. **Pause for explicit user approval** before Phase 3. Say something like: "Review the README. When you're happy, say you approve and I'll create the feature docs and add the links."

---

## Phase 3 – Create feature docs and update README (after approval)

1. **For each feature set** from the discussion:
   - **Filename:** Kebab-case slug from the feature set name (e.g. "Live API documentation" → `api-docs.md` or `live-api-documentation.md`). If the first feature set is "Overview" or similar, use `overview.md`.
   - **Content:** Create a markdown file in the same folder with:
     - Title (H1) matching the feature set.
     - **Summary** — Short paragraph.
     - **Scope** — Bullets or short sections.
     - Optional: **Implementation options**, **Out of scope**, **Dependencies** (as in existing exploration docs).

2. **Update README.md:**
   - Keep the top-line header, skill version line, global summary, and explorations-evaluation link.
   - Keep the **sectioned structure** (one `## <Feature set name>` per feature set with summary). In each section, **add a link** to the corresponding feature-set file (e.g. `See [api-docs.md](api-docs.md) for details.` or a consistent line at the end of each section). Do not replace sections with a table.

3. Then run **add and commit** per "Branch and commit" above.
