# Commit Guidelines

Use this guideline when creating commits, drafting commit messages, or summarizing changes for a commit.

## Goals

A commit description should let a reviewer understand:

- What changed.
- Why the change was made.
- How the behavior, workflow, or artifact layout is affected.
- What verification was run.
- Whether any known risk or follow-up remains.

## Before Committing

- Inspect `git status --short --untracked-files=all`.
- Inspect the diff for every file that will be staged.
- Stage only files that belong to the requested change.
- Do not include unrelated local changes in the commit.
- Do not rewrite, discard, or clean user changes unless the user explicitly asks.

## Commit Subject

Write the first line as a concise imperative summary:

```text
Add commit message guidelines
```

Rules:

- Use imperative mood: `Add`, `Fix`, `Move`, `Update`, `Remove`.
- Keep it specific to the user-visible or repository-visible change.
- Avoid vague subjects like `Update docs`, `Fix stuff`, or `Changes`.
- Prefer the smallest accurate scope over a broad label.
- Do not end the subject with a period.

## Commit Body

Add a body when the change is not obvious from the subject or when context will help future readers.

Use short paragraphs or bullets. Include:

- Motivation: why the change exists.
- Scope: the main files, systems, or workflows affected.
- Behavior: what is different after the commit.
- Verification: tests, commands, or checks that were run.
- Risk or follow-up: only when relevant.

Example:

```text
Add commit message guidelines

Document how agents should write commit subjects and bodies, including
what context to capture before committing and how to report verification.

Verification:
- Reviewed guideline links from AGENTS.md and README.md
```

## Verification Notes

When the commit affects code, include the relevant test command in the handoff and, when useful, the commit body.

When the commit affects docs only, a link check, markdown review, or `git diff --check` is usually enough.

If verification could not be run, state that directly and explain why.

## Multi-Repo Work

When a task touches more than one repository:

- Commit each repository separately.
- Keep each commit scoped to that repository's changes.
- Report any related uncommitted changes in other repositories.
- Never stage files from a different repository by accident.
