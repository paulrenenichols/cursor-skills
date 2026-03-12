# update-skill

A Cursor skill that guides you through updating any existing Cursor skill — determining the right version bump, updating the SKILL.md version, managing a CHANGELOG.md, and optionally installing the updated skill after pushing.

## What it does

- **Gathers context:** Identifies the skill being updated, reads its current version, and asks what changed.
- **Determines version bump:** Analyzes the changes against semver rules for skills (major = breaking, minor = new capability, patch = fix/polish) and recommends a bump. Asks for clarification when ambiguous.
- **Updates version and changelog:** Bumps the `version` field in SKILL.md frontmatter. Creates or updates CHANGELOG.md — if one doesn't exist, it bootstraps entries from git history.
- **Commits, pushes, and installs:** Commits the version bump, pushes (with confirmation), then offers to install the latest version to `~/.cursor/skills/`.

## Why use it

Manually tracking skill versions and changelogs is easy to forget. This skill enforces a consistent versioning workflow: describe what changed, get a semver recommendation, and let the skill handle the frontmatter update, changelog entry, commit message, and installation. It works with any skill in any repo.

## How to install

Copy this folder to your Cursor skills directory:

```bash
cp -r update-skill ~/.cursor/skills/
```

Or, from the repo root: `cp -r cursor-skills/update-skill ~/.cursor/skills/`

## How to trigger

After making changes to a skill, say something like:

- "Update this skill's version"
- "Bump the skill version"
- "Update the changelog for this skill"
- "Release a new version of this skill"
- "I've finished updating this skill, version it"

The agent uses the skill when it detects you want to version, document, or release changes to an existing skill.

## Example flow

1. You finish editing `docs-driven-dev/SKILL.md` to add a new workflow phase.
2. You say: "Update this skill's version."
3. **Phase 1 (Gather):** The agent reads the skill's current version (`1.1.0`) and asks what changed. You describe the new phase.
4. **Phase 2 (Version bump):** The agent recommends a **minor** bump to `1.2.0` because a new phase is a backward-compatible addition. You confirm.
5. **Phase 3 (Apply):** The agent updates `version: "1.2.0"` in SKILL.md, adds an entry to CHANGELOG.md (bootstrapping from git if it didn't exist), and asks if the description needs updating.
6. **Phase 4 (Ship):** The agent commits, asks to push, then offers to install to `~/.cursor/skills/docs-driven-dev/`.

## Semver decision guide

| Bump | When to use | Skill examples |
|------|------------|----------------|
| **Major** | Breaking changes that disrupt existing usage | Removed trigger phrases, restructured workflow phases, changed output file formats, removed features |
| **Minor** | New backward-compatible capabilities | New workflow phases, new trigger phrases (old ones still work), new supporting files, expanded scope |
| **Patch** | Fixes and polish | Typo corrections, wording clarifications, doc improvements, bug fixes in instructions, reordered steps for clarity |
