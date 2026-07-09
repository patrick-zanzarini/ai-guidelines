# Workflow

Single source of truth for reusable execution workflow and gates across repositories that reference `ai-guidelines`.

## Mandatory Read Order

When a consuming repository references the shared instructions:

1. Read this workflow file by direct path.
2. Read the consuming repository's root `AGENTS.md` if it has not already been read for the current task.
3. Read any relevant domain `AGENTS.md` files or source-of-truth docs routed by that repository.

If a consuming repository defines stricter gates, follow the stricter requirement.

## Gate Trigger and Sequence

- Progress Gate applies only when the current task has a persisted `.ai/artifacts/plans/*.md` file in the consuming repository, unless the user explicitly asks to skip the progress gate for the current task.
- A plan file for a different task does not trigger Progress Gate for the current task.
- Required sequence for plan-driven implementation:
  1. Persist the plan file in the consuming repository's `.ai/artifacts/plans/` folder.
  2. Update the consuming repository's active `.ai/artifacts/progress/progress.md`, unless the user explicitly asked to skip the progress gate.
  3. Make implementation changes.
- Implementation change means any edit to code, docs, config, tests, scripts, or instruction files.

## Task Flow

### 1. Classify the Request

- **Planning request**: follow [Planning](planning.md) for plan artifact rules.
- **Implementation with a current-task plan**: apply the Progress Gate in this file and use [Progress Tracking](progress.md) for file structure.
- **Direct implementation without a current-task plan**: proceed with consuming-repository and domain rules; `.ai/artifacts/progress/progress.md` tracking is optional.
- **Domain-specific design or content output**: read the consuming repository's domain source-of-truth docs before proposing content.

### 2. Interview Process Before Planning

- Interview-first discovery is mandatory for planning requests.
- Use [Interviewing](interviewing.md) categories to drive questions:
  - Unclear Specifications
  - Contradictions
  - Edge Cases
  - Potential Issues
  - Scope
- Prioritize blocker-level issues first, especially contradictions and unclear specifications.
- Continue clarifications until blocker-level issues are resolved or explicitly deferred by the user.
- Capture key interview decisions in the plan notes before implementation starts.
- Interview may be abbreviated only when allowed by [Planning](planning.md) and [Interviewing](interviewing.md).

### 3. Planning Gate

- Interview-first discovery is mandatory before drafting a plan.
- Do not draft plans with unresolved blocker-level contradictions or unclear specifications.
- Save approved plans under the consuming repository's `.ai/artifacts/plans/` folder before any implementation starts.
- Plan approval in chat does not persist files automatically; implementation is blocked until the plan exists as a `.ai/artifacts/plans/*.md` file.

### 4. Progress Gate

- User skip exemption: if the user explicitly asks to skip the progress gate, do not create or update `.ai/artifacts/progress/progress.md` for the current task.
- Otherwise, if the current task has a persisted plan file, this gate applies.
- When the gate applies, update `.ai/artifacts/progress/progress.md` before any implementation change.
- When the gate applies, update `.ai/artifacts/progress/progress.md` immediately after each completed implementation phase.
- When the gate applies, keep checklist state and `Current Status` synchronized.
- When the gate applies and an update is missed, stop work and update `.ai/artifacts/progress/progress.md` before further edits, verification, or status reporting.

### 5. Implementation

- Apply domain-specific rules from the touched project area.
- Keep changes scoped to the user request.
- Prefer source-of-truth docs over duplicate rules.

### 6. Handoff

- Report what changed and where.
- Include verification results or explicit blockers.
- Suggest the next logical step only when useful.

## Examples

### Compliant Sequence

1. Draft and approve plan in chat.
2. Save the plan to `.ai/artifacts/plans/01_feature_plan.md`.
3. Update `.ai/artifacts/progress/progress.md` for that same feature, unless explicitly skipped.
4. Start implementation edits.

### Violation Sequence

1. Draft and approve plan in chat.
2. Start editing code or docs before saving the plan and updating `.ai/artifacts/progress/progress.md`.
3. Save the plan and update `.ai/artifacts/progress/progress.md` afterward.

This is non-compliant because gate ordering was violated.

## Escalation Rule

If instructions conflict:

1. Follow safety and hard-gate rules first.
2. Prefer consuming-repository domain `AGENTS.md` files for domain-specific behavior.
3. Treat shared guideline files as process authority.
4. Keep consuming-repository root `AGENTS.md` minimal and link to owner documents.
