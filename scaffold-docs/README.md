# scaffold-docs

A Cursor skill that creates a fresh `_docs/` structure in a new project and runs a planning workflow: it helps you plan the initial README, then generates definition docs and milestones with phases and phase-plans.

## What it does

- **Scaffold:** Creates `_docs/` with `planning/setup/`, `planning/milestones/00-initial-milestones/`, `planning/explorations/`, `milestones/`, and `progress/`. Copies setup guides (new-project-setup, new-milestone-setup, explorations-evaluation) into the project.
- **Plan:** Prompts you for a discussion about what you want to build (purpose, scope, goals, architecture, risks), then drafts `00-initial-milestones/README.md`.
- **Run setup:** Follows the new-project-setup workflow to add definition files (user-flow, auth, tech-stack, ui-rules, theme-rules, project-rules) in `00-initial-milestones/` and generate initial milestones (e.g. 01-setup, 02-mvp) with `phases/` and `phase-plans/`.

## Why use it

Use this skill when you want a consistent planning workflow across projects: discuss what to build, capture it in a README, then generate user-flow, auth, tech stack, UI/theme/project rules, and initial milestones with phases and phase-plans. It’s useful for project kickoffs and keeping _docs in sync. The skill ships its own setup file versions (flat paths, no project-overview/definition subfolders) so every project gets the same workflow.

## How to install

Copy this folder to your Cursor skills directory:

```bash
cp -r scaffold-docs ~/.cursor/skills/
```

Or, from the repo root: `cp -r cursor-skills/scaffold-docs ~/.cursor/skills/`

## How to trigger

In Cursor, open the project where you want _docs and say something like:

- “Scaffold _docs in this project”
- “Set up the _docs planning structure for this new project”
- “Use the scaffold-docs skill to create _docs and plan the initial README”

The agent uses the skill when it detects you’re starting a new project and want _docs-based planning.

## Example flow

1. **Phase 1 (Scaffold):** The agent creates the `_docs/` tree, writes `_docs/README.md` (with an attribution line for the skill version), and copies the setup files into `_docs/planning/setup/`.
2. **Phase 2 (Plan README):** The agent asks what you want to build (purpose, scope, goals, etc.), then drafts `_docs/planning/milestones/00-initial-milestones/README.md` and pauses for review.
3. **Phase 3 (Run setup):** The agent follows the project’s `new-project-setup.md` to add user-flow, auth, tech-stack, ui-rules, theme-rules, project-rules, then generates milestones and phase/phase-plan files.

After that, you can run phases from `_docs/milestones/`, add milestones with `new-milestone-setup.md`, or evaluate explorations with `explorations-evaluation.md`.
