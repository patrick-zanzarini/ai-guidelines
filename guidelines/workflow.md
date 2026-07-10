# Workflow

Single source of truth for reusable request classification, execution gates, verification, and handoff across repositories using these shared guidelines.

## Mandatory Read Order

1. Read this workflow by direct path.
2. Read the consuming repository's root `AGENTS.md`.
3. Read relevant routed domain instructions and source-of-truth documents.

Within project guidance, safety and external-effect gates cannot be relaxed. Shared workflow rules are defaults; an explicit consuming-repository exception may specialize process details such as artifact location, project commands, or domain-specific approval requirements.

## Classify The Request

| Class | Expected behavior | Task record |
|-------|-------------------|-------------|
| Advisory or review | Inspect and answer without mutation. | Not required |
| Diagnosis | Determine and explain the cause; do not fix unless requested. | Usually not required |
| Direct low-risk implementation | Implement a clear, small, single-session change. | Optional |
| Tracked implementation | Plan and execute substantial, risky, multi-session, migration, multi-repo, or handoff-sensitive work. | Required |
| Externally impactful work | Prepare the work, then obtain explicit approval before the external or irreversible action. | Required when implementation is substantial or resumable |

Create a task when the user explicitly requests a persisted plan or tracking record, even if the work would otherwise be small. Use [Tasks](tasks.md) for its schema and lifecycle.

## Discovery Gate

- Inspect available repository and system context before asking questions.
- Ask only about unresolved decisions that materially affect scope, behavior, architecture, risk, or acceptance.
- Resolve blocker-level contradictions before locking a Plan.
- Document reasonable non-blocking assumptions instead of turning every uncertainty into an interview.
- Use [Interviewing](interviewing.md) for question selection and prioritization.

## Task Gate

When a task record is required:

1. Create the task under the consuming repository's configured task location.
2. Complete its Plan while status is `Draft`.
3. Resolve or explicitly defer blocker-level uncertainties.
4. Set it to `Ready` and record `Plan Locked`, or lock it as implementation begins.
5. Update mutable Progress at material checkpoints during implementation.

Task-record creation and maintenance are process operations, not implementation changes, and do not recursively trigger another task gate. If a required update is missed, reconcile it at the next safe checkpoint; do not interrupt an atomic edit merely to update prose.

## Implementation Gate

- Apply instructions for every touched project area.
- Keep changes scoped to the request and preserve unrelated work.
- Use the locked Plan as the baseline for tracked work.
- Record deviations as Plan amendments. Obtain user confirmation before accepting amendments that materially expand scope, change user-visible behavior, increase risk, or add external effects.

## External-Effect Approval Gate

Explicit user authorization is required immediately before destructive or irreversible operations, production changes, deployments, publication, credential or secret changes, paid actions, or messages/actions affecting external people or systems when that authorization has not already been clearly granted.

Approval for planning or local implementation does not imply approval for the external action.

## Verification Gate

- Run the narrowest meaningful checks first, followed by broader checks proportionate to risk.
- Verify changed documentation, configuration, generated output, and migrations as well as source code.
- Record verification results in the task when one exists.
- If verification cannot run, state what remains unverified, why, and the resulting risk. Do not claim completion beyond the evidence.

## Commit And Handoff

- Commit only when the user or established repository workflow authorizes it; follow [Commit Guidelines](commits.md).
- Report what changed, where it changed, verification results, and unresolved risks or blockers.
- For tracked work, leave Progress consistent with the handoff state and update task status accordingly.
- Suggest a next step only when it is useful.
