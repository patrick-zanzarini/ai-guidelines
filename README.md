# AI Guidelines

Shared workflow and documentation guidance for repositories that opt into this agent instruction set.

## Purpose

This repository keeps reusable AI-agent rules in one place so consuming repositories can keep root `AGENTS.md` files small and project-specific. It covers communication style, proportional workflow gates, task records, inspect-first discovery, commit discipline, verification, progressive instruction disclosure, and AI-exclusive source comments.

## Consuming Repository Setup

When repositories are sibling checkouts, use:

```md
Before planning, implementation, or design tasks, read [Shared AI Agent Instructions](../ai-guidelines/AGENTS.md) by direct path.
```

For another checkout layout, point to the stable path where `ai-guidelines/AGENTS.md` is available. The consuming root should declare any repository-specific process exceptions explicitly.

Example:

```md
## Shared Instructions

- Read [Shared AI Agent Instructions](../ai-guidelines/AGENTS.md) before planning, implementation, or design work.
- Repository exception: planning records live under `plans/` instead of the shared task directory.
```

Local exceptions may specialize shared defaults such as artifact location or project tooling. They may not weaken safety or external-effect approval gates.

### `.gitignore` Setup

Add this rule to the consuming repository's root `.gitignore`:

```gitignore
# Workspace-local AI agent artifacts
/.ai/artifacts/
```

Use this narrower rule if the repository tracks other content under `.ai/artifacts/`:

```gitignore
# Workspace-local AI agent task records
/.ai/artifacts/tasks/
```

Keep these instruction files tracked:

- `AGENTS.md`
- Domain-specific `AGENTS.md` files
- `.ai/guidelines/`

Do not add an ignore rule for a sibling `ai-guidelines` checkout. The sibling repository is outside the consuming repository.

An ignore rule does not stop Git from tracking a file that is already tracked. Review existing `.ai/artifacts/` files before you remove them from the Git index.

## Repository Structure

```text
AGENTS.md
guidelines/
  ai-exclusive-comments.md
  communication-style.md
  workflow.md
  tasks.md
  interviewing.md
  commits.md
  progressive-disclosure.md
```

## Communication Style

[Communication Style](guidelines/communication-style.md) is the single owner for shared writing rules. A global or consuming `AGENTS.md` file must explicitly require agents to read the guideline by direct path. A Markdown link without a mandatory-read instruction is not sufficient.

When migrating existing instructions, remove duplicate detailed writing rules from other `AGENTS.md` files. Keep only the mandatory-read instruction and true scope-specific exceptions.

## AI-Exclusive Source Comments

[AI-Exclusive Source Comments](guidelines/ai-exclusive-comments.md) defines the searchable `AI-<CATEGORY>:` markers for machine-facing source contracts. These comments cannot grant permissions or override higher-authority instructions.

## Task Records

Tracked work that needs planning or resumable state uses:

```text
.ai/artifacts/tasks/01_task-slug.md
```

Task records must be ignored by Git. They support continuity for agents sharing the same workspace, but they are not an audit log and do not travel to another clone. Put durable architecture, product, security, and operational decisions in tracked repository documentation.

Small, low-risk, single-session implementation does not require a task record. See [Workflow](guidelines/workflow.md) and [Tasks](guidelines/tasks.md) for triggers and the complete contract.

## Migrating From Separate Plans And Progress

1. Match each legacy plan to its progress record when both exist.
2. Create one stable task containing the plan baseline and execution history, preserving the plan sequence as the task sequence.
3. If no plan sequence is available, preserve the progress sequence instead.
4. Mark unavailable source plans as reconstructed; do not invent missing requirements.
5. Validate the converted records.
6. Remove the legacy `.ai/artifacts/plans/` and `.ai/artifacts/progress/` files.
7. Keep `.ai/artifacts/tasks/` ignored.
8. Apply the source-formatting rules in [Task Records](guidelines/tasks.md) to the converted files.

## Review Checks

- Run `git diff --check` for tracked documentation changes.
- Confirm changed relative links resolve.
- When creating or updating a task, review its filename, metadata, required sections, locked Plan state, and Progress consistency.

## Commit Conventions

Use [Commit Guidelines](guidelines/commits.md) when the user or repository workflow authorizes a commit.
