# Changelog

## [1.0.1] - 2026-03-12

### Fixed
- Phase 3 now includes step 3c to check and update version references in the skill's README.md, preventing stale version numbers after a bump

## [1.0.0] - 2026-03-12

### Added
- Initial release of the update-skill
- 4-phase workflow: gather context, determine version bump, apply updates, commit/push/install
- Semver analysis with major/minor/patch classification rules tailored for Cursor skills
- CHANGELOG.md bootstrapping from git history when no changelog exists
- Post-push installation prompt to copy updated skill to `~/.cursor/skills/`
