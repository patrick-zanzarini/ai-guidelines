# Task Records

A task record contains a stable implementation Plan and mutable Progress. Use a task record for work that needs planning, resumption, coordination, or handoff.

## When To Create A Task

Create a task record for:

- A persisted plan or tracking record that the user requests.
- Substantial or risky implementation.
- Work that is likely to continue in another session.
- A migration.
- Multi-repository coordination.
- Handoff-sensitive work.
- Work whose decisions or verification state must remain recoverable in the same workspace.

A task record is not required for advisory work, diagnosis without implementation, or a small low-risk single-session change. Create one for these types of work when the user requests it.

## Storage And Naming

- Store task records in `.ai/artifacts/tasks/` in the consuming repository by default.
- Ignore `.ai/artifacts/` or the narrower `.ai/artifacts/tasks/` by default.
- Use `{sequence}_{task-slug}.md` for the filename.
- Start the sequence at `01`.
- Increase the sequence by creation order.
- Use at least two digits for sequence numbers: `01`, `02`, ... `99`, `100`.
- For a new task, use one more than the highest sequence in the task directory.
- Do not fill sequence gaps.
- Do not reuse a sequence from a deleted task.
- Use lowercase kebab-case for `<task-slug>`.
- Do not rename a task when its status changes.

During a v1 migration, preserve the originating plan sequence. If you cannot identify a plan, preserve the progress sequence. If a sequence collision exists, assign the next unused sequence. Record the former identifiers in Progress.

Task records are workspace-local. They do not replace tracked architecture decisions, product specifications, runbooks, or security documentation.

## Source Formatting

- Do not hard-wrap task-record prose.
- Put each paragraph, list item, and numbered step on one source line.
- Let the editor or Markdown renderer wrap text visually.

## Statuses

| Status | Meaning |
|--------|---------|
| `Draft` | The Plan may change. Implementation has not started. |
| `Ready` | The Plan is locked. Implementation may start. |
| `In Progress` | Implementation is active. |
| `Paused` | Work is intentionally inactive but can resume. No external unblock condition is implied. |
| `Blocked` | Work cannot continue until an explicit condition is met. |
| `Verifying` | Implementation is complete. Required checks are running or pending. |
| `Done` | Acceptance criteria and required verification are complete. |
| `Cancelled` | Work ended without completion. Progress contains the reason. |
| `Superseded` | Another task replaced this task. Progress links to the replacement. |

## Metadata Contract

Every task record must contain:

- `ID`: Exactly the sequence-prefixed filename without `.md`.
- `Status`: One allowed status.
- `Created`: An ISO 8601 timestamp with a timezone offset.
- `Updated`: An ISO 8601 timestamp with a timezone offset.
- `Plan Locked`: An ISO 8601 timestamp with a timezone offset. Use `N/A` only while the status is `Draft`.
- `Repository`: A repository name. Use comma-separated repository names for a coordinating task.
- `Branch`: The intended branch or `N/A`.

## Static Plan Contract

The `## Plan` section must contain these sections in this order:

1. `### Objective`
2. `### Acceptance Criteria`
3. `### Scope And Exclusions`
4. `### Implementation Steps`
5. `### Risks And Dependencies`
6. `### Verification Plan`

Use numbered step identifiers such as `P1`, `P2`, and `P3`. Progress uses these identifiers to refer to Plan steps without changing Plan text.

The Plan may change freely while the task status is `Draft`.

When the Plan is approved before implementation:

1. Update `Status` and `Plan Locked` in one task-record change. Set the values to `Ready` and the current timestamp, respectively.

When implementation starts while the task status is `Draft`:

1. Update `Status` and `Plan Locked` in one task-record change. Set the values to `In Progress` and the current timestamp, respectively.

When implementation starts while the task status is `Ready`:

1. Set the task status to `In Progress`.
2. Preserve the existing `Plan Locked` timestamp.

After Plan locking, change the Plan only to consolidate an amendment with the status `Accepted`. Update the affected operative text so that the Plan does not contain known incorrect or superseded instructions. Do not change the locked Plan for a `Proposed` or `Rejected` amendment. Do not remove amendment history.

Keep the Plan concise and ready for implementation. Include a small snippet, interface shape, or pseudocode only when it defines a non-obvious contract. Do not include implementation-sized code.

## Mutable Progress Contract

The `## Progress` section must contain these sections in this order:

1. `### Checklist`
2. `### Current Update`
3. `### Decisions And Issues`
4. `### Plan Amendments`
5. `### Verification Results`

The checklist must refer to Plan step identifiers.

Update Progress at each of these checkpoints:

- Work starts.
- A step or phase is complete.
- Work pauses or becomes blocked.
- A material decision occurs.
- Verification status changes.
- A handoff is prepared.

Do not update Progress after every edit.

Use ISO 8601 timestamps with offsets for updates, decisions, issues, amendments, and verification results.

## Plan Amendments

Do not silently rewrite a locked Plan. Record the amendment and its status before you change the affected Plan text.

Add each amendment under `### Plan Amendments`. Include:

- The timestamp.
- The status: `Proposed`, `Accepted`, or `Rejected`.
- The reason.
- The affected Plan step identifiers or acceptance criteria.
- User confirmation when the amendment materially changes scope, user-visible behavior, risk, or external effects.

You may accept and record a non-material implementation discovery without pausing work. A material amendment must remain `Proposed` until the user confirms it.

After an amendment becomes `Accepted`:

1. Consolidate the amendment into the affected Plan clauses when the existing text is incomplete, contradictory, or superseded.
2. Keep the accepted amendment in Progress as the durable decision record.
3. Preserve the original `Plan Locked` timestamp.
4. Update the task metadata.
5. Update Current Update.
6. Confirm that the Plan is internally consistent.

Keep historical wording in the amendment record. Do not keep historical wording as operative Plan guidance.

## Multi-Repository Work

- Keep one coordinating task in the lead repository.
- List every applicable repository in the `Repository` metadata.
- Record repository-specific steps and verification in the coordinating task.
- Create a repository-local task only when that repository needs independent resumption or handoff state.
- Commit each repository independently when commits are authorized.

## Consistency Rules

- A status of `Ready`, `In Progress`, `Paused`, `Blocked`, `Verifying`, `Done`, `Cancelled`, or `Superseded` requires a `Plan Locked` timestamp.
- A `Blocked` task must state an explicit unblock condition.
- A `Paused` task must state why work paused.
- A `Paused` task must state the next resumable step.
- A `Done` task requires completed acceptance criteria and verification results, or an explicitly accepted limitation.
- A `Cancelled` task must contain a closeout reason.
- A `Superseded` task must link to the replacement task.
- `Updated` must match the latest material Progress entry.

## Template

```markdown
# Task: [Title]

**ID:** 01_task-slug
**Status:** Draft
**Created:** YYYY-MM-DDTHH:MM:SS-03:00
**Updated:** YYYY-MM-DDTHH:MM:SS-03:00
**Plan Locked:** N/A
**Repository:** repository-name
**Branch:** N/A

## Plan

### Objective

[Outcome]

### Acceptance Criteria

- [Observable result]

### Scope And Exclusions

- Included: [Scope]
- Excluded: [Scope]

### Implementation Steps

1. **P1:** [Action and target]
2. **P2:** [Action and target]

### Risks And Dependencies

- [Risk, dependency, or none]

### Verification Plan

- [Check and expected result]

## Progress

### Checklist

- [ ] **P1:** [Step title]
- [ ] **P2:** [Step title]

### Current Update

- **YYYY-MM-DDTHH:MM:SS-03:00:** [Current state and next step]

### Decisions And Issues

- None.

### Plan Amendments

- None.

### Verification Results

- Not run yet.
```
