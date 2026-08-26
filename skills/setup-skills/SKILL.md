---
name: setup-skills
description: Configure this repo for the engineering skills — issue tracker, domain doc, and language conventions, optionally committing the result. Run once, before the first use of the other skills.
disable-model-invocation: true
---

# Setup Skills

Write the per-repo configuration the other engineering skills read:

- `docs/agents/issue-tracker.md` — where issues live, and the operations on them
- `docs/agents/domain.md` — where `CONTEXT.md` and ADRs live, and how to consume them
- `AGENTS.md` — the single source of agent instructions for this repo; carries which language each kind of output is written in. Appended, never overwritten.
- `CLAUDE.md` — one line, `@AGENTS.md`, so Claude Code picks the above up

All of it is copied from this skill's seed files, never regenerated from a description — the other skills treat these as a behavioural contract, and copying is what keeps the bytes identical across every repo. The two `docs/agents/` files go over verbatim; `language.md` is appended to `AGENTS.md` with one blank substituted from the user's answer; `CLAUDE.md` is a single import line. Step 3 is a script, so none of it depends on retyping.

Writing those files is the whole job. Git is separate — this may be someone else's repo, so ask before touching it.

## 1. Explore

Whether `docs/agents/` already exists; whether `AGENTS.md` does and already carries a `## Language` section; whether `CLAUDE.md` does and, if so, whether it already imports `AGENTS.md`; plus `git rev-parse --git-dir`, `git log --oneline -1`, and `git status --short`.

That is the whole exploration. This skill creates no `CONTEXT.md`, no `docs/adr/`, and no `issues/` — each appears when work actually produces it — so whether they exist changes nothing here.

## 2. Present and confirm

**`docs/agents/` exists** — the repo is already configured. List the files found, say that they are meant to be hand-edited and that a rerun replaces them with the seed versions, and ask whether to overwrite. Continue only on an explicit yes.

**`docs/agents/` is absent** — show the user both files, path and full contents, and let them edit before anything lands.

Then, as separate questions — a yes to one is not a yes to another:

- **prose language** — which language for specs, tickets, `CONTEXT.md`, ADRs? Default English. The answer fills the blank in step 3. A `## Language` section already in `AGENTS.md` is theirs: show it, skip the question, write nothing.

Then the two git questions — ask them, and wait for the answer rather than assuming one either way:

- **not a repo** — `git init` here? Name the directory in full, so a wrong working directory is caught first.
- **commit?** — name the branch, quote the step-4 message, and mention any dirty or staged state already there.

Writing the files does not wait on these; step 4 does.

## 3. Write

Mechanical, from this skill's own folder. Run it — do not retype any of these bytes from the descriptions above.

```bash
mkdir -p docs/agents
cp issue-tracker.md docs/agents/issue-tracker.md
cp domain.md docs/agents/domain.md

# The one variable in this whole step: the prose language from step 2.
# Not $LANG — that is a real environment variable.
PROSE_LANG='English'

if ! grep -q '^## Language$' AGENTS.md 2>/dev/null; then
  if [ -s AGENTS.md ]; then
    # close an unterminated last line, then leave one blank line
    [ "$(tail -c1 AGENTS.md | wc -l)" -eq 0 ] && printf '\n' >> AGENTS.md
    printf '\n' >> AGENTS.md
  fi
  sed "s/<language>/$PROSE_LANG/g" language.md >> AGENTS.md
fi

if [ ! -e CLAUDE.md ]; then
  printf '@AGENTS.md\n' > CLAUDE.md
elif ! grep -q '^@AGENTS\.md$' CLAUDE.md; then
  printf '@AGENTS.md\n\n' | cat - CLAUDE.md > CLAUDE.md.tmp && mv CLAUDE.md.tmp CLAUDE.md
fi
```

Apply the user's step-2 edits, if any, to the copies afterwards — never to the seeds.

Why it is a script and not prose to follow: the other skills read `AGENTS.md` and `docs/agents/*` as a behavioural contract, so the bytes have to be the same in every repo. Retyping five lines by hand drifts.

Both halves are guarded, so a second run adds nothing: an existing `## Language` section and an existing `@AGENTS.md` import are left exactly as they are.

`AGENTS.md` is appended to, never overwritten — the rest of the file is not yours. It is also the single source: the block goes there even when the repo already keeps its agent instructions in `CLAUDE.md`. `CLAUDE.md` only ever gains one import line, at the top, with every other byte untouched.

That last case — a `CLAUDE.md` that already had content — leaves the repo with two sources of instruction. Deliberate: rewriting someone's `CLAUDE.md` is not this skill's call. Say so in step 5 and let them fold it into `AGENTS.md` themselves.

## 4. Commit — if step 2 said yes

`git init` first if that was agreed and there is no repo yet. Stage only the files you wrote, never `git add -A` — the working tree may hold changes that are not yours to commit.

Message, under this repo's `<type>: <message>` convention. `chore:` for both: agent configuration is neither a user-facing feature nor human documentation.

| Case                          | Message                                              |
| ----------------------------- | ---------------------------------------------------- |
| repo you just `git init`ed    | `chore: initial commit with engineering skills setup` |
| repo that already had commits | `chore: configure engineering skills`                 |

## 5. Report

Which files now exist or changed, and that all are theirs to edit directly — rerunning this skill is for starting over, not for tweaking. If `CLAUDE.md` kept content of its own, name it as a second source of instruction and suggest folding it into `AGENTS.md`. Then the git outcome: which commit on which branch, or that the files are written but uncommitted and left for them to stage.
