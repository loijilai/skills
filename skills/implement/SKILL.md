---
name: implement
description: "Implement a piece of work based on a ticket, a spec, or what this conversation has settled."
disable-model-invocation: true
---

Implement one piece of work, from a ticket, a spec, or what this conversation has settled.

## Resolve the work

The source is one of: a **ticket**, a **spec**, or the **work settled in this conversation**. Any of the three is valid input.

There is no fallback chain. Never guess, and never silently pick up unrelated work. Name the source you are about to implement, and unless it is unambiguous, confirm it before writing any code. It is unambiguous only when the user named it — an argument identifying a ticket or spec, or an explicit "implement what we just agreed". If the argument is vague, or nothing was named and the conversation has not settled on one piece of work, ask which source to use — offering the candidates: open tickets, an existing spec, or the conversation — and wait.

When the source is a ticket or spec, the issue tracker should have been provided to you; if `docs/agents/issue-tracker.md` is missing, tell the user to run `/setup-skills`. Fetch the named ticket or spec and read its full body. Working from the conversation needs no tracker.

## Build

Use /tdd where possible, at pre-agreed seams.

Run typechecking regularly, single test files regularly, and the full test suite once at the end.

Tick each acceptance criterion as it goes green, if the source has any.

Once done, use /code-review to review the work.

Mark the ticket done — only if the source was a ticket.

Commit your work to the current branch.
