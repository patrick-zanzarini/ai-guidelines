# Shared AI Agent Instructions

Reusable workflow and documentation guidelines for repositories that opt into this `ai-guidelines` repository.

## Mandatory Read

Before responding to a user request, read [Communication Style](guidelines/communication-style.md) by direct path if you have not already read it for the current task.

Before planning, implementation, or design work, read [Workflow](guidelines/workflow.md) by direct path. Then read the consuming repository's root `AGENTS.md` and relevant routed domain instructions if they have not already been read for the current task.

## Guideline Index

| Guideline | Authority |
|-----------|-----------|
| [Communication Style](guidelines/communication-style.md) | Writing style, response structure, plans, procedures, technical instructions, and user-facing error messages. |
| [Workflow](guidelines/workflow.md) | Request classification, execution gates, verification, approval, and handoff. |
| [Tasks](guidelines/tasks.md) | Task-record triggers, schema, static Plan contract, mutable Progress contract, and lifecycle. |
| [Interviewing](guidelines/interviewing.md) | Inspect-first discovery, decision-relevant questions, assumptions, and issue prioritization. |
| [Commit Guidelines](guidelines/commits.md) | Commit authorization, staging discipline, and message structure. |
| [Progressive Disclosure](guidelines/progressive-disclosure.md) | Instruction ownership, placement, overrides, promotion, pruning, and review. |

Each reusable rule has one owner document. Other files should link to the owner instead of redefining the rule.

## Universal Standards

### Interaction Behavior

- **MANDATORY:** When the user asks a question, answer the question.
- A project-specific question authorizes the read-only investigation that is necessary to answer it. Inspect relevant files and run non-mutating commands when the answer depends on project state.
- Do not modify files or change local or external state unless the user explicitly requests a change.
- Before a state-changing action, confirm that the user's request authorizes the action. Do not treat necessary read-only investigation as a state-changing action.
- Do not run a command only because the user asks what the command does.
- Preserve unrelated and user-owned changes. Do not rewrite, discard, clean, stage, or commit them without explicit authorization.

### Process Artifacts

- Shared defaults place workspace-local task records under `.ai/artifacts/tasks/` in the consuming repository.
- Task records are ignored by Git and are not durable cross-clone documentation. Promote lasting decisions into tracked project documentation.
- A consuming root `AGENTS.md` may explicitly define a different artifact convention as a repository-specific process exception.
