---
name: scaffold-exploration
version: "1.1.0"
description: Prompts a discussion to create or update an exploration folder under _docs/planning/explorations/. Use when creating a new exploration or when updating an existing one (add feature sets, align README to standards, add supporting docs). Drafts READMEs with feature-set sections and skill version; after approval creates or updates per-feature markdown files, feature-sets/ and supporting-docs/ structure, and README links.
---

# Create or update an exploration

Use this skill when the user wants to **create** a new exploration folder or **update** an existing one under `_docs/planning/explorations/` in a project that has _docs. The project must have (or will get) `_docs/planning/explorations/` and ideally `_docs/planning/setup/explorations-evaluation.md` (from scaffold-docs or added separately).

## When to use

- User wants to add a new exploration to a _docs project.
- User wants to update an existing exploration (add feature sets, bring README up to standard, add screenshots or other supporting docs).
- User says "create an exploration", "add an exploration folder", "scaffold an exploration in _docs", "update an exploration", "add feature sets to exploration", "bring exploration README up to standard", "add screenshots/docs to exploration", or references this skill by name; or user points at an existing exploration folder to update.
- Do **not** use for evaluating an existing exploration or turning it into a milestone (use the project's `explorations-evaluation.md` instead).

---

## Create vs update

**First step:** Determine intent from the user's request or context.

- **Create** — User wants a new exploration (new folder). Run the **Create flow** (Phases 1–3 below), using the **new exploration folder structure** (top-level README, `feature-sets/` with README and per-feature-set `.md` files, `supporting-docs/` with README).
- **Update** — User points at or names an existing exploration folder to update. Run the **Update flow** (Steps 1–4 under "Update an exploration" below): review contents, discuss (unmentioned files and how supporting docs relate to feature sets), apply chosen updates, set "Updated with" skill version, commit.

Existing flat explorations (README + feature `.md` files at exploration root, no `feature-sets/` or `supporting-docs/`) remain valid; the update flow can suggest migrating them to the new structure.

---

## Branch and commit

**Before creating or changing any files**, ask the user:

> Should this work be done on the **current branch**, or on a **new branch from main**?

- **If new branch from main:** In the **current project** (the _docs project where the exploration lives), run `git fetch origin` (or `git fetch origin main`), then create and checkout a new branch from `origin/main`. Use a branch name like `explore/<exploration-name>` once the exploration name is known, or `explore/new-exploration` if you create the branch before the name is decided.
- **If current branch is main:** Treat like "new branch"—fetch latest main, then create and checkout a new branch from `origin/main` so the exploration is not committed directly to main.
- **If current branch and not main:** Proceed on the current branch; no fetch or new branch.

**When scaffolding or updates are complete** (after Phase 3 for create, or after Step 4 for update): In the project repo, run `git add` for the exploration folder and any new or changed files, then `git commit` with a clear message (e.g. `Add exploration: <name>`, `Update exploration: <name>`, or `Scaffold exploration <name> with scaffold-exploration skill`). Do not push unless the user asks.

---

## Exploration folder structure (target layout)

New explorations use this layout. Updates can migrate existing flat layouts to it.

```
_docs/planning/explorations/<name>/
  README.md                    # Top-level: summary, structure blurb, skill version
  feature-sets/
    README.md                  # Feature-set index (sections + links, no global summary)
    overview.md
    api-docs.md
    ...
  supporting-docs/
    README.md                  # One summary section per doc/folder; links to feature sets when relevant
    screenshots/
    ...
```

**Top-level README.md**

- H1, skill version line ("Created with…" or "Updated with…"), global summary, link to explorations-evaluation.
- **Structure** section: "Feature sets are in `feature-sets/` (see [feature-sets/README.md](feature-sets/README.md)). Supporting materials (screenshots, extra docs) are in [supporting-docs/](supporting-docs/) with a short index in [supporting-docs/README.md](supporting-docs/README.md)."
- One `## <Feature set name>` per feature set with a short summary and link to `feature-sets/<slug>.md`.

**feature-sets/README.md**

- No skill version line (only at exploration root). No global summary (lives in parent README).
- One `## <Feature set name>` per feature set with short summary + "See [filename.md](filename.md)." Optional: "For overview and structure, see [../README.md](../README.md)."

**supporting-docs/README.md**

- One section per file or subfolder (e.g. `## screenshots`). Each section: 1–2 sentence summary of what the asset is and how it relates to the exploration. When a supporting doc relates to one or more feature sets, include links (e.g. "Relates to [sql-query-interface.md](../feature-sets/sql-query-interface.md)."). No skill version line.

---

## Phase 1 – Discussion (create flow)

1. **Confirm** the project has `_docs/planning/explorations/` (create it if missing).

2. **Exploration name:** Ask for a name used as the folder name (e.g. `developer-experience`). You may **suggest** a kebab-case name based on the features or theme discussed. If the user hasn't given a name by the time you draft the README, suggest one before creating the folder.

3. **Ask for:**
   - **What this exploration is about** — One short paragraph (global summary).
   - **Feature sets to explore** — For each, a short name and a summary (what we're exploring and why). Group fine-grained ideas into logical feature sets (e.g. "API docs", "DB UI", "Docker dev"); do not create a separate file for every small idea.

4. Optionally ask if they want to add supporting materials later (screenshots, extra docs); if yes, `supporting-docs/` is created up front with a placeholder README.

5. Do not create exploration files yet; only capture intent. (Branch setup may already be done if the user chose a new branch.)

---

## Phase 2 – Draft top-level README and pause (create flow)

1. Create `_docs/planning/explorations/<exploration-name>/README.md` with **this order**:

   - **Top-line header** — Single H1 (e.g. `# Developer experience`).
   - **Skill version** — One line: `Created with the **scaffold-exploration** skill (vX.Y.Z).`  
     Read the **current** version from this skill's SKILL.md frontmatter (`version` field). If the skill is loaded from `~/.cursor/skills/scaffold-exploration/`, open that path; otherwise use the skill file in context.
   - **Global summary** — One short paragraph describing the work being done in this exploration (from the discussion).
   - **Link to explorations-evaluation:**  
     `Use [explorations-evaluation.md](../../setup/explorations-evaluation.md) to evaluate this exploration or turn it into a milestone.`
   - **Structure** — Short blurb: "Feature sets are in `feature-sets/` (see [feature-sets/README.md](feature-sets/README.md)). Supporting materials (screenshots, extra docs) are in [supporting-docs/](supporting-docs/) with a short index in [supporting-docs/README.md](supporting-docs/README.md)."
   - **Sections for each feature set** — One `## <Feature set name>` per feature set, each with a short **summary paragraph**. Do not add links yet (the per-feature files do not exist yet); you will link to `feature-sets/<slug>.md` in Phase 3.

2. **Pause for explicit user approval** before Phase 3. Say something like: "Review the README. When you're happy, say you approve and I'll create the feature-sets and supporting-docs folders and add the links."

---

## Phase 3 – Create feature-sets, supporting-docs, and commit (create flow)

1. **Create `feature-sets/`** and **`feature-sets/README.md`**:
   - In the README, one `## <Feature set name>` per feature set with short summary + "See [slug.md](slug.md)." (Use kebab-case slugs as below.)

2. **For each feature set** from the discussion:
   - **Filename:** Kebab-case slug from the feature set name (e.g. "Live API documentation" → `api-docs.md`). If the first feature set is "Overview" or similar, use `overview.md`.
   - **Content:** Create `_docs/planning/explorations/<name>/feature-sets/<slug>.md` with:
     - Title (H1) matching the feature set.
     - **Summary** — Short paragraph.
     - **Scope** — Bullets or short sections.
     - Optional: **Implementation options**, **Out of scope**, **Dependencies** (as in existing exploration docs).

3. **Create `supporting-docs/`** and **`supporting-docs/README.md`** with a single placeholder section, e.g. "_No supporting documents yet._"

4. **Update top-level README.md:**
   - Keep the header, skill version line, global summary, explorations-evaluation link, and structure blurb.
   - In each feature-set section, **add a link** to the corresponding file (e.g. `See [api-docs.md](feature-sets/api-docs.md) for details.`).

5. Then run **add and commit** per "Branch and commit" above.

---

## Update an exploration

When the user wants to **update** an existing exploration:

**Before Step 1:** Ask the user about branch per **Branch and commit** above (current branch vs new branch from main). Then proceed with the steps below.

### Step 1 – Review contents

- List all files and folders under the exploration (recursively).
- Read top-level README (and if present, `feature-sets/README.md`, `supporting-docs/README.md`).
- Identify:
  - Feature-set docs (in flat layout: any `.md` except README at exploration root; in new structure: under `feature-sets/`).
  - Supporting assets (images, PDFs, subfolders like `sample-xlsx-exports/`, etc.).
  - Anything not referenced in the top-level README or in feature-sets/README or supporting-docs/README.

### Step 2 – Discuss and decide

- **Unmentioned files:** For each file (or folder) not referenced in any README, trigger a short discussion: "X is not mentioned in the README(s). Should we: (a) add a feature set / section and link it, (b) move it into supporting-docs and add a summary in supporting-docs/README.md, (c) leave as-is but add a mention, or (d) remove/relocate?" Do not change files until the user chooses.
- **Supporting docs and feature sets:** For each supporting doc or folder (existing or newly added), ask the user how it relates to the feature sets. Document that relationship in supporting-docs/README.md by adding links to the related feature-set files (e.g. "Relates to [overview.md](../feature-sets/overview.md) and [api-docs.md](../feature-sets/api-docs.md).") in that doc's section. If the user says a supporting doc has no specific feature-set link, the section can omit the links and just give the summary.
- **Optional:** Suggest bringing README up to "skill standard" (see README standards below) and, if the layout is flat, suggest migrating to the new structure (feature-sets/, supporting-docs/).

### Step 3 – Apply updates

- **Adding feature sets:** Same as create: new section in top-level README and in feature-sets/README, new file under feature-sets/, link from both READMEs. Create feature-sets/ and supporting-docs/ first if the exploration is still flat.
- **README standards check:** Ensure top-level README has: H1, skill version line, global summary, explorations-evaluation link; if using new structure, add structure blurb and feature-set sections with links to `feature-sets/*.md`. Ensure feature-sets/README and supporting-docs/README exist and are consistent with contents.
- **Adding supporting files:** When the user adds files under `supporting-docs/` (or a subfolder), update `supporting-docs/README.md` with a section per new file/folder: a one-sentence summary plus, when the user has indicated a relationship, links to related feature-set files (e.g. "Relates to [feature-name.md](../feature-sets/feature-name.md).").
- **Version line:** When making any edits, set the exploration's top-level README line to "Updated with the **scaffold-exploration** skill (vX.Y.Z)." where X.Y.Z is the **current** skill version (read from this skill's SKILL.md frontmatter). Replace any existing "Created with…" with this line (optionally append "(Created with …)" in parentheses for traceability). The version must always be the current skill version at the time of the run.

### Step 4 – Commit

- Run `git add` for the exploration folder and any new or changed files, then `git commit` with a message like "Update exploration: <name>" or "Add feature sets / supporting-docs to <name>".

---

## README standards (for create and update)

Use this checklist when checking or bringing an exploration README up to standard:

**Top-level exploration README**

- Single H1.
- One line: "Created with…" or "Updated with…" **scaffold-exploration** skill (vX.Y.Z) — version from current skill frontmatter.
- One short paragraph global summary.
- Link to explorations-evaluation.
- If using new structure: "Structure" blurb + one `## <Feature set name>` per feature set with summary + link to `feature-sets/<file>.md`.
- No broken links to feature-set or supporting-docs files.

**feature-sets/README.md**

- One `## <Feature set name>` per feature set with short summary + link to the corresponding `.md` in the same folder.

**supporting-docs/README.md**

- One section per file or subfolder under supporting-docs, each with a brief summary. When a supporting doc relates to feature sets (from the update discussion), the section includes links to the related feature-set files.

---

## Skill version (Created with / Updated with)

Both "Created with" and "Updated with" must use the **current** skill version — the `version` field from this skill's SKILL.md frontmatter at the time of the run (read from `~/.cursor/skills/scaffold-exploration/SKILL.md` or the skill file in context). That way the exploration README always reflects which version of the skill last created or updated it.

- **Create:** Write "Created with the **scaffold-exploration** skill (vX.Y.Z)." with X.Y.Z = current skill version.
- **Update:** Write "Updated with the **scaffold-exploration** skill (vX.Y.Z)." with X.Y.Z = current skill version; replace any existing "Created with…" line (optionally keep "(Created with …)" in parentheses for history).
