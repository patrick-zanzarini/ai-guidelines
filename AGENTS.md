# Shared AI Agent Instructions

Reusable workflow and documentation guidelines for repositories that opt into this `ai-guidelines` repository.

## Mandatory Read

When a consuming repository references this file, read [Workflow](guidelines/workflow.md) by direct path before planning, implementation, or design tasks.

After the shared workflow is read, follow the consuming repository's local `AGENTS.md` and any relevant domain instructions if they have not already been read for the current task.

## Guideline Index

| Guideline | When to read |
|-----------|--------------|
| [Workflow](guidelines/workflow.md) | Required first read for planning, implementation, and design tasks. |
| [Planning](guidelines/planning.md) | Plan file standards, naming, and structure. |
| [Interviewing](guidelines/interviewing.md) | Clarifying requirements before planning or large implementation. |
| [Progress Tracking](guidelines/progress.md) | `.ai/artifacts/progress/progress.md` format, switching rules, consistency checks, and template. |
| [Progressive Disclosure](guidelines/progressive-disclosure.md) | Maintaining `AGENTS.md` structures and instruction routing. |

## Universal Standards

### Interaction Behavior

- If the user asks a question only and does not explicitly request implementation, answer the question first and do not change files or code.

### Execution Gates

- Workflow and execution gates are defined in [Workflow](guidelines/workflow.md).
- Use [Progress Tracking](guidelines/progress.md) for consuming-repository `.ai/artifacts/progress/progress.md` structure, switching behavior, and consistency rules.

### Process Artifacts

- Plans, progress files, and implementation notes belong in the consuming repository unless the user explicitly asks to update this shared resource repository.

### Mermaid Diagrams

- Use dark mode for Mermaid diagrams with `%%{init: {'theme': 'dark'}}%%` at the top of each diagram.
