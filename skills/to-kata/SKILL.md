---
name: to-kata
description: Extract one minimal, self-contained feature from the existing codebase as a code kata, for the user to implement and then compare against the original.
disable-model-invocation: true
---

This approach is modeled on how Franklin practiced writing. The goal is to build a learning loop that produces feedback.

Franklin would first summarize an article, then rewrite it from his summary, and finally compare his version against the original and learn from the differences.

I want to apply the same method to programming, learning from an existing codebase. I'll tell you the direction I want to practice, and you extract a kata from the codebase. I'll implement it myself, then go back and compare against how the original codebase does it — understanding why it was designed that way — to deepen and broaden what I learn.

## The unit: one minimal feature

Building a whole project is like playing the entire song every time you practice. Instead, isolate the part that matters and drill it.

- One run = one minimal working feature (e.g. "practice OAuth" → a minimal OAuth login flow).
- Keep only the core mechanism of the direction. Cut or pre-provide everything else (UI, DB, extra providers, error pages…).
- Specify only the entry point and observable behavior. Do not prescribe functions, helpers, or internal structure — decomposing the feature is part of the practice.
- Ignore hacks, legacy baggage, and business complexity. You may reframe the scenario to make it more transferable.

```markdown
# Code Kata

## Practice Goal
<The core concept to drill, in one sentence>

## Context
<Minimal problem background>

## Feature
- Entry point: <API / command / public interface>
- Expected behavior: <observable input → output / user-visible flow>

## Out of Scope
- <What was cut or is provided, so I don't build it>

## Stretch Goal
<One challenge slightly beyond the comfort zone>

## Reflection Questions
- How did you decompose the feature into functions? Where does the original draw its boundaries, and why?
- ...
```
