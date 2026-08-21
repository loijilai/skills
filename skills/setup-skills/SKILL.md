---
name: setup-skills
description: Configure this repo for the engineering skills — issue tracker and domain doc conventions, optionally committing the result. Run once, before the first use of the other skills.
disable-model-invocation: true
---

# Setup Skills

Write the per-repo configuration the other engineering skills read:

- `docs/agents/issue-tracker.md` — where issues live, and the operations on them
- `docs/agents/domain.md` — where `CONTEXT.md` and ADRs live, and how to consume them

Both are copied verbatim from this skill's seed files. The other skills treat them as a behavioural contract, so copying — rather than regenerating from a description — is what keeps them identical across every repo.

Writing those two files is the whole job. Git is an extra, and only on request — this may be someone else's repo.

## 1. Explore

Whether `docs/agents/` already exists, plus `git rev-parse --git-dir`, `git log --oneline -1`, and `git status --short`.

That is the whole exploration. This skill creates no `CONTEXT.md`, no `docs/adr/`, and no `issues/` — each appears when work actually produces it — so whether they exist changes nothing here.

## 2. Present and confirm

**`docs/agents/` exists** — the repo is already configured. List the files found, say that they are meant to be hand-edited and that a rerun replaces them with the seed versions, and ask whether to overwrite. Continue only on an explicit yes.

**`docs/agents/` is absent** — show the user both files, path and full contents, and let them edit before anything lands.

Then, as separate questions defaulting to no — a yes to one is not a yes to another:

- **not a repo** — `git init` here? Name the directory in full, so a wrong working directory is caught first.
- **commit?** — name the branch, quote the step-4 message, and mention any dirty or staged state already there.

Anything short of an explicit yes is a no: write the files, skip step 4.

## 3. Write

From this skill's own folder:

```bash
mkdir -p docs/agents
cp issue-tracker.md docs/agents/issue-tracker.md
cp domain.md docs/agents/domain.md
```

Copy the bytes. Apply the user's step-2 edits, if any, to the copies afterwards.

## 4. Commit — only if step 2 said yes

`git init` first if that was agreed and there is no repo yet. Stage only your own two files, never `git add -A` — the working tree may hold changes that are not yours to commit.

Message, under this repo's `<type>: <message>` convention. `chore:` for both: agent configuration is neither a user-facing feature nor human documentation.

| Case                          | Message                                              |
| ----------------------------- | ---------------------------------------------------- |
| repo you just `git init`ed    | `chore: initial commit with engineering skills setup` |
| repo that already had commits | `chore: configure engineering skills`                 |

## 5. Report

Which two files now exist, and that both are theirs to edit directly — rerunning this skill is for starting over, not for tweaking. Then the git outcome: which commit on which branch, or that the files are written but uncommitted and left for them to stage.
