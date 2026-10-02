# Issue tracker: local markdown

Issues and specs for this repo live as markdown files under `issues/`, tracked in git alongside the code.

## Layout

```
issues/
└── <feature-slug>/
    ├── spec.md
    ├── 01-<ticket-slug>.md
    └── 02-<ticket-slug>.md
```

One directory per feature. `spec.md` holds the spec; every other file in the directory is a ticket, numbered from `01`.

The number is the file's identity — nothing else here has one. It carries no state: a ticket's blockers are whatever its `Blocked by:` line says, and whether the work is done is not recorded.

## Operations

The skills name these operations; this file is what they mean here.

- **Publish a spec** — write `issues/<feature-slug>/spec.md`, creating the directory.
- **Publish a ticket** — write `issues/<feature-slug>/<NN>-<slug>.md`. Number from `01` in the order published, which is dependency order, so a ticket's blockers carry lower numbers than it does. Its `Blocked by:` line names them by number and title.
- **Fetch a spec or a ticket** — read the file. The user normally passes a path or a number; a bare number resolves inside the feature directory in play.

## Scope of this file

This file governs where issues live and how to operate on them. What goes *inside* a spec or a ticket belongs to the skills that write them.

Nothing here closes a ticket or records progress on one. Files are written once and then left alone; what is done is whatever is in the code and in git. For a tracker that does carry open and closed, rerun `/setup-skills` and answer github.

## Using a different tracker

Replace the contents of this file with the conventions of whatever you use — GitLab through `glab`, Jira, or prose describing your workflow. The skills only ever name the operations above; this file is the translation layer, and it is the only place that changes.
