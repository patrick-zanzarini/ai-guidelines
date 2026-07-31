# Workflow

This document is the single source of truth for reusable request classification, execution gates, verification, and handoff.

## Mandatory Read Order

1. Read this workflow by direct path.
2. Read the consuming repository's root `AGENTS.md`.
3. Read the applicable domain instructions.
4. Read the applicable source-of-truth documents.

Safety and external-effect gates cannot be relaxed by project guidance.

Shared workflow rules are defaults. A consuming repository may define an explicit process exception for artifact locations, project commands, or domain-specific approval requirements.

## Classify The Request

| Class | Required behavior | Task record |
|-------|-------------------|-------------|
| Advisory or review | Inspect the applicable context. Answer without mutation. | Not required |
| Diagnosis | Determine and explain the cause. Do not fix the cause unless the user requests a fix. | Usually not required |
| Direct low-risk implementation | Implement a clear, small, single-session change. | Optional |
| Tracked implementation | Plan and execute substantial, risky, multi-session, migration, multi-repository, or handoff-sensitive work. | Required |
| Externally impactful work | Prepare the work. Get explicit approval before the external or irreversible action. | Required when implementation is substantial or resumable |

Create a task record when the user requests a persisted plan or tracking record. Create the record even when the work is small. Use [Task Records](tasks.md) for the schema and lifecycle.

## Discovery Gate

1. Inspect the available repository and system context.
2. Identify unresolved decisions that affect scope, behavior, architecture, risk, or acceptance.
3. Resolve blocker-level contradictions before you lock a Plan.
4. Record reasonable non-blocking assumptions.
5. Ask the user only about decisions that remain unresolved.

Use [Interviewing And Discovery](interviewing.md) to select and prioritize questions.

## Task Gate

When a task record is required:

1. Create the task record in the configured task location.
2. Complete the Plan while the task status is `Draft`.
3. Resolve or explicitly defer each blocker-level uncertainty.
4. When the Plan is approved before implementation, update `Status` and `Plan Locked` in one task-record change. Set the values to `Ready` and the current timestamp, respectively.
5. When implementation starts from `Draft`, update `Status` and `Plan Locked` in one task-record change. Set the values to `In Progress` and the current timestamp, respectively.
6. When implementation starts from `Ready`, set the task status to `In Progress`. Preserve the existing `Plan Locked` timestamp.
7. Update Progress at material implementation checkpoints.

Task-record creation and maintenance are process operations. These operations do not trigger another task gate.

If a required update is missing, add the update at the next safe checkpoint. Do not interrupt an atomic edit only to update the task record.

## Implementation Gate

- Apply the instructions for each project area that you change.
- Keep each change in the requested scope.
- Preserve unrelated work.
- Use the locked Plan as the baseline for tracked work.
- Record each deviation as a Plan amendment.
- Get user confirmation before you accept an amendment that materially expands scope.
- Get user confirmation before you accept an amendment that changes user-visible behavior, increases risk, or adds external effects.

## External-Effect Approval Gate

Get explicit user authorization immediately before any of the following actions when the user has not already given clear authorization:

- A destructive or irreversible operation.
- A production change.
- A deployment or publication.
- A credential or secret change.
- A paid action.
- A message or action that affects an external person or system.

Authorization for planning or local implementation does not authorize an external action.

## Verification Gate

1. Run the narrowest meaningful checks.
2. Run broader checks that are proportionate to the risk.
3. Verify changed source code when applicable.
4. Verify changed documentation, configuration, generated output, and migrations when applicable.
5. Record verification results in the task record when a task record exists.

If a required check cannot run, state which check did not run. State the cause and the resulting risk. Do not claim completion without evidence.

## Commit And Handoff

1. Create a commit only when the user or repository workflow authorizes a commit.
2. Follow [Commit Guidelines](commits.md) when you create a commit.
3. Report what changed and where the change occurred.
4. Report verification results.
5. Report unresolved risks or blockers.
6. Make Progress consistent with the handoff state for tracked work.
7. Update the task status for tracked work.
8. Suggest a next step only when the suggestion is useful.
