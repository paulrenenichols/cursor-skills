# Changelog

## [1.0.0] - 2026-03-12

### Added
- Initial release of the update-skill
- 4-phase workflow: gather context, determine version bump, apply updates, commit/push/install
- Semver analysis with major/minor/patch classification rules tailored for Cursor skills
- CHANGELOG.md bootstrapping from git history when no changelog exists
- Post-push installation prompt to copy updated skill to `~/.cursor/skills/`
