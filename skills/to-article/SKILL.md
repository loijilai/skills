---
name: to-article
description: Turn a discussion session or a half-written draft into a clear, consistent, readable article.
disable-model-invocation: true
---

Default the article's language to whatever the repo's `AGENTS.md`/`CLAUDE.md` `## Language` section specifies, or the language the user is writing in if there's no such section. This is only the starting default for the prose — the terminology rules below are separate and apply regardless of which language you write in.

## Determine the source

- **Session mode** — no draft text/file given: draw the article from the current conversation.
- **Draft mode** — the user pasted text or gave a file path: treat it as the base to complete and restructure, preserving their actual points and voice.

Either way, act as an editor, not a ghostwriter: if a gap needs filling with content that isn't already in the draft or the conversation (a missing explanation, a transition, a claim that needs support), discuss it with the user rather than inventing it silently. If the user asks for an example to make a passage easier to follow, look it up and verify it's actually correct before adding it — don't fabricate one. Only skip verification if the example is a plain illustration with nothing to get wrong (e.g. a toy `x = 1, y = 2` walkthrough).

## Align before writing

Before drafting, have a short exchange with the user — a small-scale version of a grilling session, not a full interview:

- Propose a working title and an outline: each section heading plus one line on what that section will cover and which points from the source it draws on.
- Ask the user to confirm, reorder, cut, merge, or flag anything you missed or over-weighted — per section, not just the outline as a whole.
- Surface anywhere you're genuinely unsure what's in scope, rather than guessing.

## Glossary pass (before writing)

Walk the source once and, for every domain term/concept and abbreviation that will appear, decide up front — this becomes the single source of truth the whole article must follow:

- **One canonical name** per concept, used everywhere (no synonyms — don't call the same thing "節點" in one paragraph and "Node" in another).
- **One zh/en treatment** per term — kept in English, translated, or bilingual on first mention — the same choice every time it appears, not decided occurrence by occurrence.
- **Abbreviations**: full name first, short form in parentheses on first use ("Application Programming Interface（API）"), short form only after that.
- **A one-sentence plain definition** for first mention, written for a reader encountering the term for the first time.

Keep this glossary as your own working state — don't dump it into the article as a term list. The article should read as a normal piece of writing, not a glossary with prose wrapped around it.

## Write the article

- Structure: a title and section headings that follow the actual shape of the ideas — not a generic template forced onto unrelated content. Paragraphs sized for readability.
- Formatting: pick one rule per category (casing, punctuation/symbols, units, version numbers) and hold it for the whole article.
- Terminology: every term and abbreviation exactly as decided in the glossary pass, every time it's used.

## Consistency self-check

Before saving, re-scan the draft specifically for:

- the same concept referred to by two different names,
- a term used before its first-mention definition appears,
- mixed zh/en treatment for the same term,
- an abbreviation used before it's spelled out.

Fix anything you find.

## Save and report

Derive `<slug>` from the article title (kebab-case, ASCII). Write to `articles/<slug>.md` under the current working directory, creating `articles/` if it doesn't exist.

Exception: if the source was a draft _file_, ask the user whether to overwrite that file in place or save as a new `articles/<slug>.md` — don't assume.

Tell the user the exact path written and give a short summary of the structure produced (the section headings), not the full content inline.
