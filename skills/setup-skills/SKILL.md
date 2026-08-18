---
name: setup-skills
description: Configure this repo for the engineering skills — issue tracker and domain doc conventions. Run once, before the first use of the other skills.
disable-model-invocation: true
---

# Setup Skills

Write the per-repo configuration the other engineering skills read:

- `docs/agents/issue-tracker.md` — where issues live, and the operations on them
- `docs/agents/domain.md` — where `CONTEXT.md` and ADRs live, and how to consume them

Both are copied verbatim from this skill's seed files. The other skills treat them as a behavioural contract, so copying — rather than regenerating from a description — is what keeps them identical across every repo.

## 1. Explore

Check whether `docs/agents/` already exists.

That is the whole exploration. This skill creates no `CONTEXT.md`, no `docs/adr/`, and no `issues/` — each appears when work actually produces it — so whether they exist changes nothing here.

## 2. Present and confirm

**`docs/agents/` exists** — the repo is already configured. List the files found, say that they are meant to be hand-edited and that a rerun replaces them with the seed versions, and ask whether to overwrite. Continue only on an explicit yes.

**`docs/agents/` is absent** — show the user both files, path and full contents, and let them edit before anything lands.

## 3. Write

From this skill's own folder:

```bash
mkdir -p docs/agents
cp issue-tracker.md docs/agents/issue-tracker.md
cp domain.md docs/agents/domain.md
```

Copy the bytes. Apply the user's step-2 edits, if any, to the copies afterwards.

Then tell the user which two files now exist and that both are theirs to edit directly — rerunning this skill is for starting over, not for tweaking.
