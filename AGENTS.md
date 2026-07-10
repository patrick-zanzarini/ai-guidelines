# Shared AI Agent Instructions

Reusable workflow and documentation guidelines for repositories that opt into this `ai-guidelines` repository.

## Mandatory Read

Before planning, implementation, or design work, read [Workflow](guidelines/workflow.md) by direct path. Then read the consuming repository's root `AGENTS.md` and relevant routed domain instructions if they have not already been read for the current task.

## Guideline Index

| Guideline | Authority |
|-----------|-----------|
| [Workflow](guidelines/workflow.md) | Request classification, execution gates, verification, approval, and handoff. |
| [Tasks](guidelines/tasks.md) | Task-record triggers, schema, static Plan contract, mutable Progress contract, and lifecycle. |
| [Interviewing](guidelines/interviewing.md) | Inspect-first discovery, decision-relevant questions, assumptions, and issue prioritization. |
| [Commit Guidelines](guidelines/commits.md) | Commit authorization, staging discipline, message structure, and verification notes. |
| [Progressive Disclosure](guidelines/progressive-disclosure.md) | Instruction ownership, placement, overrides, promotion, pruning, and review. |

Each reusable rule has one owner document. Other files should link to the owner instead of redefining the rule.

## Universal Standards

### Interaction Behavior

- If the user asks a question, review, or diagnosis without requesting implementation, answer it without changing files or external state.
- Preserve unrelated and user-owned changes. Do not rewrite, discard, clean, stage, or commit them without explicit authorization.

### Process Artifacts

- Shared defaults place workspace-local task records under `.ai/artifacts/tasks/` in the consuming repository.
- Task records are ignored by Git and are not durable cross-clone documentation. Promote lasting decisions into tracked project documentation.
- A consuming root `AGENTS.md` may explicitly define a different artifact convention as a repository-specific process exception.
