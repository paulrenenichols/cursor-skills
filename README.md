# Cursor skills

A collection of personal Cursor skills—one folder per skill. Each folder can be copied into `~/.cursor/skills/<skill-name>/` to use the skill in Cursor.

## How to install

1. Clone this repo:
   ```bash
   git clone https://github.com/paulrenenichols/cursor-skills.git
   cd cursor-skills
   ```
2. Copy the skill folder(s) you want into your Cursor skills directory:
   ```bash
   cp -r update-skill ~/.cursor/skills/
   ```
   Or install all active skills:
   ```bash
   for dir in */; do [ "$dir" != "deprecated/" ] && cp -r "$dir" ~/.cursor/skills/"${dir%/}"; done
   ```
   (Skips the `deprecated/` folder. Avoid copying the repo root into `~/.cursor/skills/`; copy only the skill subfolders.)

## Skills in this repo

| Skill | Description |
|-------|-------------|
| [update-skill](./update-skill) | Guides through updating any Cursor skill: gathers change details, determines semver bump, updates the version in SKILL.md, manages CHANGELOG.md, and offers installation after push. |

## Deprecated

The following skills have been moved to [`deprecated/`](./deprecated) and are no longer maintained. They have been superseded by [docs-driven-dev](https://github.com/paulrenenichols/docs-driven-dev).

| Skill | Last version | Successor |
|-------|-------------|-----------|
| scaffold-docs | 1.1.0 | [docs-driven-dev](https://github.com/paulrenenichols/docs-driven-dev) |
| scaffold-exploration | 1.1.2 | [docs-driven-dev](https://github.com/paulrenenichols/docs-driven-dev) |
