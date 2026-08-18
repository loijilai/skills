---
name: implement
description: "Implement a piece of work based on a spec or set of tickets."
disable-model-invocation: true
---

Implement the work described by the user in the spec or tickets.

The issue tracker should have been provided to you. If `docs/agents/issue-tracker.md` is missing, tell the user to run `/setup-skills`.

Fetch the ticket the user names. If they name none, fetch the next unblocked ticket.

Use /tdd where possible, at pre-agreed seams.

Run typechecking regularly, single test files regularly, and the full test suite once at the end.

Tick each acceptance criterion as it goes green.

Once done, use /code-review to review the work.

Mark the ticket done.

Commit your work to the current branch.
