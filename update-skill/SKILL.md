---
name: update-skill
version: "1.0.1"
description: >-
  Guides through updating any Cursor skill: gathers change details, determines
  semver bump (major/minor/patch), updates the version in SKILL.md frontmatter,
  manages CHANGELOG.md (bootstrapping from git history if needed), and offers
  installation after push. Use when updating a skill, bumping a skill version,
  or managing skill changelogs.
---

# Update a Cursor skill

Use this skill when the user wants to update an existing Cursor skill — bump its version, record what changed, and optionally install the updated version.

## When to use

- User says "update this skill", "bump the version", "update the changelog", "release a new version of this skill".
- User has finished making changes to a skill and wants to version and document them.
- User wants to bootstrap a CHANGELOG.md from git history for a skill that doesn't have one.
- Do **not** use for creating a new skill from scratch (use `create-skill` instead).

---

## Phase 1 – Gather context

1. **Identify the skill.** Determine which skill is being updated:
   - If the current working directory is a skill folder (contains `SKILL.md`), use it.
   - If the current repo contains multiple skill folders, ask which one.
   - Otherwise, ask the user for the path to the skill.

2. **Read current state.** Open the skill's `SKILL.md` and extract:
   - `name` from frontmatter
   - `version` from frontmatter (current version)
   - `description` from frontmatter

3. **Ask what changed.** Prompt the user:
   > What changes are you making to this skill? Describe the updates — what was added, changed, fixed, or removed, and why.

   Gather enough detail to determine the scope of the change. Ask follow-up questions if the description is too vague to classify.

---

## Phase 2 – Determine version bump

Analyze the described changes against these semver rules for skills:

### Major (breaking)

Increment the major version when the update breaks existing usage:

- Renamed or removed trigger phrases that users rely on
- Restructured workflow phases (reordered, removed, or merged phases)
- Changed file output formats or directory structures that downstream projects depend on
- Removed features or capabilities
- Changed frontmatter fields in a way that breaks skill discovery
- Any change that would cause a project currently using this skill to break or behave unexpectedly

### Minor (new capability)

Increment the minor version for backward-compatible additions:

- New workflow phases or steps added (existing phases unchanged)
- New file outputs or optional features
- New trigger phrases (existing ones still work)
- New supporting files added to the skill
- Expanded scope that doesn't change existing behavior

### Patch (fix/polish)

Increment the patch version for non-functional improvements:

- Bug fixes in workflow instructions
- Typo corrections, wording clarifications
- Documentation improvements
- Reordering instructions for clarity without changing behavior
- Updating examples

### Present recommendation

Tell the user:

> Based on your changes, I recommend a **[major/minor/patch]** bump from **X.Y.Z** to **A.B.C**. Here's why: [reasoning].

If the change is ambiguous (could reasonably be classified as two different bump levels), present both options with reasoning and ask the user to decide:

> This could be a **minor** bump (because [reason]) or a **major** bump (because [reason]). Which do you prefer?

Calculate the new version string: increment the appropriate segment and reset lower segments to zero (e.g. 1.2.3 → major: 2.0.0, minor: 1.3.0, patch: 1.2.4).

---

## Phase 3 – Apply updates

### 3a. Update SKILL.md version

Update the `version` field in the skill's SKILL.md frontmatter to the new version string. Only change the version value; leave all other frontmatter and content untouched (unless the user's changes require content edits, which should already have been made before invoking this skill).

### 3b. Manage CHANGELOG.md

**If `CHANGELOG.md` does not exist** in the skill folder:

1. Bootstrap it from git history. Run:
   ```
   git log --oneline --follow -- <skill-folder-path>
   ```
2. Scan the commit messages for version-bump patterns (e.g. `v1.2.0`, `bump to 1.1.0`, `<skill-name> v1.0.0:`). Group commits between version bumps into version sections.
3. Format the bootstrapped changelog using the structure below. Use best-effort categorization — if a commit message doesn't clearly fit Added/Changed/Fixed/Removed, place it under Changed. Include a note at the top:
   ```
   > Entries below v[current] were reconstructed from git history.
   ```

**Add a new entry** at the top of the changelog (below the title) for the new version:

```markdown
## [X.Y.Z] - YYYY-MM-DD

### Added
- (new features, if any)

### Changed
- (modifications to existing behavior, if any)

### Fixed
- (bug fixes, if any)

### Removed
- (removed features, if any)
```

Only include categories that have entries. Use the user's change description from Phase 1 to write clear, concise bullet points. Use today's date.

**Changelog title:** If creating the file, start with:

```markdown
# Changelog
```

### 3c. Update README.md

Check the skill's README.md for any version references (e.g. "Current version: X.Y.Z", "v1.2.0", version numbers in example output or install instructions). Update them to the new version. If the README describes capabilities that have changed, update those sections too.

### 3d. Update description (if needed)

If the changes meaningfully alter what the skill does or when it triggers, ask the user whether the `description` in SKILL.md frontmatter should also be updated. Propose a revised description if so.

---

## Phase 4 – Commit, push, and install

### 4a. Commit

Stage the changed files (SKILL.md, CHANGELOG.md, and any other files the user modified) and commit:

```
git add <skill-folder>/
git commit -m "<skill-name> v<new-version>: <short description of changes>"
```

### 4b. Push

Ask the user before pushing:

> Ready to push to remote. Proceed?

If yes, push the current branch to origin.

### 4c. Offer installation

After the push succeeds, ask:

> Do you want to install the latest version to `~/.cursor/skills/<skill-name>/`?

If yes, copy the skill folder to `~/.cursor/skills/<skill-name>/`, overwriting the existing installation:

```
rm -rf ~/.cursor/skills/<skill-name>/
cp -r <skill-folder> ~/.cursor/skills/<skill-name>/
```

Use `rm -rf` before `cp -r` to ensure stale files from a previous version are removed.
