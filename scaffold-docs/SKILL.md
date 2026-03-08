---
name: scaffold-docs
version: "1.0.0"
description: Creates a fresh _docs structure in a new project (planning, milestones, progress, setup), helps plan and write the 00-initial-milestones README, then runs an adapted new-project-setup workflow to generate definition files and initial milestones. Use when starting a new project and the user wants _docs-based planning and milestone/phase workflow.
---

# Scaffold _docs in new projects

Use this skill when the user wants to create a fresh `_docs/` folder structure in a **new project**, with planning, milestones, setup guides, and the initial milestone README + definition docs + generated milestones.

## When to use

- User is starting a new project and wants _docs-based planning.
- User asks to scaffold _docs, set up planning docs, or create the milestone/phase workflow from scratch.
- Do **not** use for adding a new milestone to an existing project (that project already has setup docs; use `new-milestone-setup.md` there).

---

## Phase 1 – Scaffold

1. **Confirm target project** – Ensure you are in the project where _docs should be created (current workspace or user-confirmed path).

2. **Create the _docs folder structure:**

   ```
   _docs/
   ├── README.md
   ├── planning/
   │   ├── setup/
   │   ├── milestones/
   │   │   └── 00-initial-milestones/
   │   └── explorations/
   ├── milestones/
   └── progress/
   ```

3. **Write _docs/README.md** – Include:
   - A brief index: milestones, progress, planning, setup (links or short descriptions).
   - **Attribution:** Read the skill version from this skill's frontmatter: open `~/.cursor/skills/scaffold-docs/SKILL.md` and read the `version` field. Add this line at the top (after the `# _docs` title) or in a short footer at the bottom:
     - `This _docs/ folder was scaffolded by the **scaffold-docs** skill (v{version}).`
     - Example: if version is `1.0.0`, write `(v1.0.0)`.

4. **Copy setup files from the skill into the project** – Copy these files **as-is** from `~/.cursor/skills/scaffold-docs/setup/` to the project's `_docs/planning/setup/`:
   - `new-project-setup.md`
   - `new-milestone-setup.md`
   - `explorations-evaluation.md`
   Do not adapt from any other repo; use the skill's canonical versions so paths and workflow stay consistent.

5. Leave `_docs/planning/milestones/00-initial-milestones/` empty for now (README will be created in Phase 2). Leave `_docs/planning/explorations/`, `_docs/milestones/`, and `_docs/progress/` empty.

---

## Phase 2 – Plan and write 00-initial-milestones README

1. **Prompt the user for a discussion** about what they want to build. Ask about:
   - Project purpose and who it's for (users, stakeholders).
   - Core features and scope (what's in for the initial plan, what's out).
   - Goals and success criteria.
   - Architecture or technical direction (if they have preferences).
   - Risks, constraints, or open questions.
   Ask clarifying questions as needed; do not assume or embellish. The aim is to capture their intent before writing the README.
2. **Draft** `_docs/planning/milestones/00-initial-milestones/README.md` from that discussion: project summary, scope, goals, architecture, risks. Include **links to the definition files that will be created** (user-flow.md, auth.md, tech-stack.md, ui-rules.md, theme-rules.md, project-rules.md). The README is the single entry point for the initial plan; the definition files live in the **same folder** (flat structure).
3. Pause for review before proceeding to Phase 3.

---

## Phase 3 – Run new-project-setup

1. The project now has `_docs/planning/setup/new-project-setup.md` (copied from the skill). Its paths already use the **flat** layout: all definition files in `_docs/planning/milestones/00-initial-milestones/`; the overview is README.md in that folder.
2. Follow the **sequence** in that file: overview (README) → user-flow → auth → tech-stack → ui-rules/theme-rules → project-rules → milestones/phases/phase-plans. Use the prompts and steps in the project's `new-project-setup.md`; do not rewrite paths.
3. **Milestone generation (step 9):** Create `_docs/milestones/01-setup`, `02-mvp`, etc., each with `phases/` and `phase-plans/` and number-prefixed files. Phase-plan conventions: branch first, commit/push at logical points, README step, progress doc at `_docs/progress/<milestone>/<phase>.md`, final commit on user approval.
4. The skill does **not** implement steps 10–13 (Agent Rules, root README update, verification checklist, "Let's get started"). Optionally point the user to those steps in the copied `new-project-setup.md` as "Optional next steps."

---

## Optional: explorations and new milestones

- **Explorations:** The project has `_docs/planning/setup/explorations-evaluation.md`. Use it in planning mode to evaluate an exploration folder and optionally turn it into a milestone.
- **New milestones:** Use `_docs/planning/setup/new-milestone-setup.md` in the project to add milestones (phases, phase-plans, progress) after the initial setup.

---

## Path convention (flat 00-initial-milestones)

All definition docs live in `_docs/planning/milestones/00-initial-milestones/`: README.md (overview), user-flow.md, auth.md, tech-stack.md, ui-rules.md, theme-rules.md, project-rules.md. There are no `project-overview/` or `definition/` subfolders.
