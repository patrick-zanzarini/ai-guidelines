# AI Guidelines

Shared workflow and documentation guidelines for repositories that opt into this agent instruction set.

## Purpose

This repository keeps reusable AI-agent process rules in one place so consuming repositories can keep their root `AGENTS.md` files small and project-specific.

Use it for:

- Shared workflow gates and execution order.
- Planning and progress artifact standards.
- Interviewing guidance before large plans.
- Commit message and staging guidance.
- Progressive-disclosure rules for maintaining `AGENTS.md` files.

## Consuming Repository Setup

In a consuming repository's root `AGENTS.md`, point agents to this repository's shared instructions by direct path:

```md
Before planning, implementation, or design tasks, read [Shared AI Agent Instructions](../ai-guidelines/AGENTS.md) by direct path.
```

Keep consuming repository instructions focused on project summary, local domain routing, and project-specific exceptions.

## Repository Structure

```text
AGENTS.md
guidelines/
  workflow.md
  planning.md
  interviewing.md
  commits.md
  progress.md
  progressive-disclosure.md
```

## Artifact Conventions

Consuming repositories should store AI process artifacts under `.ai/artifacts/`:

- Plans: `.ai/artifacts/plans/*.md`
- Active progress: `.ai/artifacts/progress/progress.md`
- Archived or resumable progress: `.ai/artifacts/progress/{sequence}_progress-{description}.md`

See [guidelines/workflow.md](guidelines/workflow.md), [guidelines/planning.md](guidelines/planning.md), and [guidelines/progress.md](guidelines/progress.md) for the full rules.

## Commit Conventions

Use [guidelines/commits.md](guidelines/commits.md) when creating commits or drafting commit descriptions.
