# Source Comments

This document is the single source of truth for ordinary source comments. [AI-Exclusive Source Comments](ai-exclusive-comments.md) owns comments that start with an `AI-<CATEGORY>:` marker.

## Rules

- Write a comment only for a reason, constraint, or consequence that the code, names, and types do not show.
- Do not restate visible code behavior.
- When a better name, type, or test can make the code clear, use it instead of a comment.
- State durable facts only. Do not write conversation history, implementation plans, or temporary reasoning.
- When a rule has an owner document, link to the owner document. Do not copy the rule.
- When you change code, update or remove each comment that the change makes incorrect.

## Generated Boilerplate

After you scaffold a project or a file with a generator, remove the generated comments that the project does not use. Examples are documentation links, section titles, and commented-out example configuration.

Do not change comments in third-party, vendored, or tool-owned files that a tool regenerates.

## Review Checklist

- [ ] Each comment states something that the code does not show.
- [ ] No comment restates visible code behavior.
- [ ] No unused generated boilerplate comment remains.
- [ ] The change updates or removes each affected comment.
