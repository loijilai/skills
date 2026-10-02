---
name: implement
description: "Implement a piece of work based on a ticket, a spec, or what this conversation has settled."
disable-model-invocation: true
---

Implement one piece of work, from a ticket, a spec, or what this conversation has settled.

## Resolve the work

The source is one of: a **ticket**, a **spec**, or the **work settled in this conversation**. Any of the three is valid input.

Never guess and never pick up unrelated work. A named ticket or spec is a source; so is a go-ahead on what the conversation just settled ("implement that") — take it as long as it is clear which piece of work it refers to. Otherwise, ask which source to use and wait.

When the source is a ticket or spec, fetch it per `docs/agents/issue-tracker.md` and read its full body. Working from the conversation needs no tracker.

## Build

Use /tdd where possible, at pre-agreed seams.

Run typechecking regularly, single test files regularly, and the full test suite once at the end.

Work through the acceptance criteria in order, if the source has any, and say which ones are green as you report back.

Once done, use /code-review to review the work.

Commit your work to the current branch.

Leave the ticket itself untouched. Nothing here edits it or closes it — the code and the commit are the record, and whether the ticket is done is the user's call to make in their tracker.
