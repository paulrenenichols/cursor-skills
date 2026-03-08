# Cursor skills

A collection of personal Cursor skills—one folder per skill. Each folder can be copied into `~/.cursor/skills/<skill-name>/` to use the skill in Cursor.

## How to install

1. Clone this repo:
   ```bash
   git clone https://github.com/<your-username>/cursor-skills.git
   cd cursor-skills
   ```
2. Copy the skill folder(s) you want into your Cursor skills directory:
   ```bash
   cp -r scaffold-docs ~/.cursor/skills/
   ```
   Or install everything:
   ```bash
   for dir in */; do cp -r "$dir" ~/.cursor/skills/"${dir%/}"; done
   ```
   (Avoid copying the repo root into `~/.cursor/skills/`; copy only the skill subfolders.)

To install a single skill without cloning the whole repo, clone then copy just that folder (e.g. `scaffold-docs`).

## Skills in this repo

| Skill | Description |
|-------|-------------|
| [scaffold-docs](./scaffold-docs) | Scaffolds a `_docs/` structure and planning workflow in new projects (00-initial-milestones README, definition docs, milestones/phases). |
