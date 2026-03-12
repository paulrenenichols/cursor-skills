# Scaffold-docs reference

## Folder tree (create in project)

```
_docs/
├── README.md
├── planning/
│   ├── setup/
│   │   ├── new-project-setup.md       # copied from skill
│   │   ├── new-milestone-setup.md     # copied from skill
│   │   └── explorations-evaluation.md # copied from skill
│   ├── milestones/
│   │   └── 00-initial-milestones/     # README in Phase 2; definition files in Phase 3
│   └── explorations/
├── milestones/                        # populated in Phase 3 (01-setup, 02-mvp, etc.)
└── progress/                          # progress/<milestone>/<phase>.md when phases run
```

## Path mapping (flat 00-initial-milestones)

| Content            | Path |
|--------------------|------|
| Overview           | `_docs/planning/milestones/00-initial-milestones/README.md` |
| User flow          | `_docs/planning/milestones/00-initial-milestones/user-flow.md` |
| Auth               | `_docs/planning/milestones/00-initial-milestones/auth.md` |
| Tech stack         | `_docs/planning/milestones/00-initial-milestones/tech-stack.md` |
| UI rules           | `_docs/planning/milestones/00-initial-milestones/ui-rules.md` |
| Theme rules        | `_docs/planning/milestones/00-initial-milestones/theme-rules.md` |
| Project rules      | `_docs/planning/milestones/00-initial-milestones/project-rules.md` |

No `project-overview/` or `definition/` subfolders. All of the above live in the same folder.

## Order of definition docs

1. README.md (overview)
2. user-flow.md
3. auth.md
4. tech-stack.md
5. ui-rules.md + theme-rules.md
6. project-rules.md
7. Milestones/phases/phase-plans under `_docs/milestones/`

## Attribution in _docs/README.md

When creating the initial `_docs/README.md`, add:

`This _docs/ folder was scaffolded by the **scaffold-docs** skill (vX.Y.Z).`

Read `version` from `~/.cursor/skills/scaffold-docs/SKILL.md` frontmatter and substitute for X.Y.Z.
