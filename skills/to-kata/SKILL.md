---
name: to-kata
description: Extract a self-contained programming practice PRD (a code kata) from the existing codebase, for the user to implement and then compare against the original.
disable-model-invocation: true
---

This approach is modeled on how Franklin practiced writing. The goal is to build a learning loop that produces feedback.

Franklin would first summarize an article, then rewrite it from his summary, and finally compare his version against the original and learn from the differences.

I want to apply the same method to programming, learning from an existing codebase. I'll tell you the direction I want to practice, and you extract a short PRD from the codebase. I'll implement it myself following that PRD, then go back and compare against how the original codebase does it — understanding why it was designed that way and how the feature is implemented — to deepen and broaden what I learn.

This skill's job is to turn a part of the codebase worth practicing into a self-contained programming practice / code kata.

The practice must have a clear goal: a clear scope that can be completed on its own.

When extracting the exercise, ignore hacks, legacy baggage, and overly complex business requirements. The focus should be on the difficulty of the programming itself, design principles, architectural trade-offs, and implementation techniques — not on reproducing the full business logic. You may reframe the scenario to make it more transferable.

```cpp
# Programming Practice PRD

## Practice Goal
<The main skill to practice this time, in one sentence>

## Context
<Minimal problem background>

## Requirements
- ...
- ...
- ...

## Constraints
- ...
- ...
- ...

## Stretch Goal
<One challenge slightly beyond the current comfort zone, but completable on your own>

## Done Criteria
- ...
- ...
- ...

## Reflection Questions
- ...
- ...
- ...
```
