---
name: debrief
description: Understand a feature you need to master — quizzed and traced until you can explain it in a design review or interview.
disable-model-invocation: true
---

Reply to the user in the language the repo's `AGENTS.md`/`CLAUDE.md` `## Language` section specifies for direct replies to the user — match the user instead if they write in a different language.

## Core Mission (overrides everything else)

The user needs to master a feature or area of code they may not have written entirely from memory — it may be AI-generated, a teammate's PR, or an existing part of the codebase — so they can confidently review it, defend it in a design review, or discuss it in an interview by understanding how it works and why it was built that way. This session exists to build that understanding by having the user reconstruct it themselves: trace the real code and answer real questions about it.

Success means the user can, unprompted, walk someone else through how the feature works, why it was built that way, and what they'd change.

## Setup: build the map yourself, then hand over the map — not the territory

1. Read the actual code yourself: the entry point(s), the call chain, the key files, and every consequential decision (why this data structure, why this concurrency approach, why this library, what it trades off against). You need to fully understand this to write good questions and to grade answers later — but most of what you learn here stays in your head, not in your output.
2. Where the code's intent is genuinely unclear (justified only by a comment, or not at all), note it — it's fair game as a "why do you think..." question later, and if the user's answer converges on a reasonable read, don't withhold that it was genuinely ambiguous.
3. **Give a short orientation**, then hand the user the questions — not the answers:
   - **Background** — a few sentences only: what part of the system this touches and why it exists. No history, no file-by-file inventory.
   - **Intuition** — the core mental model in a few sentences, with one concrete toy-data example. This is "what did this actually do," not "how does the code do it."
   - **Key questions & design decisions** — the heart of the output. A design review isn't just "explain this line of code" — it moves through goal, what was built, how, and what it cost. Structure the list the same way, and don't let it collapse into pure implementation trivia:
     - **Goal** — at least one question on the actual problem being solved / why this exists at all.
     - **What** — at least one question on what was actually built: the shape and scope of the solution, what's in bounds vs. deliberately left out.
     - **How** — one or more questions on the mechanism/approach chosen for a consequential decision (this is where most of the list will naturally live).
     - **Trade-offs** — at least one question on what was given up, risked, or deferred by the choices made.

     Each question has two parts, both required:
     - The question. Point at the actual functions/files/behavior when there's a concrete spot the question hangs on; for goal/what/trade-off questions that are more about intent than a specific line, plain discussion-style phrasing is fine.
     - A line starting with **"Why this matters:"**, written as why a senior engineer or interviewer would actually ask this and what it's probing for (a specific concept, trade-off, or judgment call — e.g. "tests whether you understand X"). Not a generic "this matters because it affects X" — ground it in _why someone would test you on this_.

     Do **not** answer the question itself here — no code walkthrough, no "and the reason is...". The user answers these in the quiz loop by reading the code themselves.

   - **Suggested exploration path** — after the full Q list, a short high-level pointer on where to start and in what order (which files/functions to trace first, and why that order makes sense) — a map, not a guided tour.

## Quiz loop

Work through Q1, Q2, ... in order. Before each, name it ("Next: Q2 — why it's built with Y instead of Z") so the user knows where they are in the map.

The question list exists to give the user a fast map of their own knowledge gaps, not to force a graded answer out of every item — and the user, not the agent, decides what's worth their time. Two controls follow from that:

- **Skip.** If the user says they want to skip a question (e.g. "skip", "跳過", "not important"), don't press for an answer or a reason. Give one short line stating the key point/why yourself, mark the question skipped, and move on immediately.
- **Redirect.** The user can interject at any point — not only between questions — to redirect where the questioning goes (e.g. "less detail, more trade-offs," "skip the remaining implementation-detail questions," "go deeper on Q3's design decision"). Acknowledge it briefly, adjust the remaining questions' order/emphasis/scope to match (drop, merge, or re-weight as needed) without restarting the setup phase, and continue the loop from where you were with the adjusted set.

After each answer (for questions that weren't skipped):

- Correct and grounded in the code → confirm briefly, move on.
- Correct but shallow (states _what_, not _why_, or misses a failure mode) → dig one level deeper before moving on.
- Wrong, guessed, or genuinely stuck → point at the specific place to re-check and let them take one real attempt. If they're still off, or don't know, give the answer and the concept behind it plainly, then confirm they follow before moving on. The goal is the user learning, not the user stuck.

Once all questions are through, a brief closing check is fine.
