# Task Records

Task records combine a stable implementation Plan with mutable Progress for work that benefits from planning, resumption, coordination, or handoff.

## When To Create A Task

Create a task for:

- An explicitly requested persisted plan or tracking record.
- Substantial or risky implementation.
- Work likely to span sessions.
- Migrations, multi-repository coordination, or handoff-sensitive work.
- Work whose decisions or verification state must be recoverable in the same workspace.

Do not require one for advisory work, diagnosis without implementation, or a small low-risk single-session change unless the user requests it.

## Storage And Naming

- Default location: `.ai/artifacts/tasks/` in the consuming repository.
- Default ignore rule: `.ai/artifacts/` or the narrower `.ai/artifacts/tasks/`.
- Filename: `{sequence}_{task-slug}.md`.
- Start sequences at `01`, increment by creation order, and keep at least two digits (`01`, `02`, ... `99`, `100`).
- For a new task, use one greater than the highest sequence already present in the task directory; do not fill gaps or reuse numbers from deleted tasks.
- Use lowercase kebab-case for `<task-slug>`.
- Never rename a task because its status changes.
- During v1 migration, preserve the originating plan sequence. If no plan exists or can be identified, preserve the progress sequence instead. Resolve a genuine collision by assigning the next unused sequence and recording the former identifiers in Progress.

Task records are workspace-local. They do not replace tracked architecture decisions, product specifications, runbooks, or security documentation.

## Statuses

| Status | Meaning |
|--------|---------|
| `Draft` | The Plan may still change. Implementation has not started. |
| `Ready` | The Plan is locked and implementation may start. |
| `In Progress` | Implementation is active. |
| `Paused` | Work is intentionally inactive but resumable; no external unblock condition is implied. |
| `Blocked` | Work cannot proceed until an explicit condition is met. |
| `Verifying` | Implementation is complete and required checks are running or pending. |
| `Done` | Acceptance criteria and required verification are complete. |
| `Cancelled` | Work ended without completion; the reason is recorded. |
| `Superseded` | Another task replaced this task; link the replacement. |

## Metadata Contract

Every task contains:

- `ID`: exactly the sequence-prefixed filename without `.md`.
- `Status`: one allowed status.
- `Created`: ISO 8601 timestamp with timezone offset.
- `Updated`: ISO 8601 timestamp with timezone offset.
- `Plan Locked`: ISO 8601 timestamp with timezone offset, or `N/A` only while `Draft`.
- `Repository`: repository name or comma-separated repository names for coordinating tasks.
- `Branch`: intended branch or `N/A`.

## Static Plan Contract

The `## Plan` section contains:

1. `### Objective`
2. `### Acceptance Criteria`
3. `### Scope And Exclusions`
4. `### Implementation Steps`
5. `### Risks And Dependencies`
6. `### Verification Plan`

Use numbered step IDs such as `P1`, `P2`, and `P3` so Progress can reference them without changing Plan text.

The Plan may change freely while status is `Draft`. When approved or implementation begins, set status to `Ready` or `In Progress` and record `Plan Locked`. After locking, change the Plan only to consolidate an amendment that has already been recorded as `Accepted`; update the affected operative text so readers do not have to reconcile known-bad or superseded instructions against Progress. Never change the locked Plan for a `Proposed` or `Rejected` amendment, and never erase amendment history. Plans should be concise and implementation-ready. Small snippets, interface shapes, or pseudocode are allowed only when needed to lock a non-obvious contract; avoid implementation-sized code.

## Mutable Progress Contract

The `## Progress` section contains:

1. `### Checklist`
2. `### Current Update`
3. `### Decisions And Issues`
4. `### Plan Amendments`
5. `### Verification Results`

The checklist references Plan step IDs. Update Progress when work starts, a step or phase completes, work pauses or blocks, a material decision occurs, verification changes, or a handoff is prepared. Do not update it after every edit.

Use ISO 8601 timestamps with offsets for updates, decisions, issues, amendments, and verification results.

## Plan Amendments

Never silently rewrite a locked Plan. Record the amendment and its status before changing affected Plan text.

Append amendments under `### Plan Amendments` with:

- Timestamp.
- Status: `Proposed`, `Accepted`, or `Rejected`.
- Reason.
- Affected Plan step IDs or acceptance criteria.
- User confirmation when the amendment materially changes scope, user-visible behavior, risk, or external effects.

Non-material implementation discoveries may be accepted and recorded without pausing. Material amendments remain `Proposed` until confirmed.

After an amendment becomes `Accepted`, consolidate it into the affected Plan clauses when the existing wording is incomplete, contradictory, or superseded. Keep the accepted amendment in Progress as the durable decision record, preserve the original `Plan Locked` timestamp, update task metadata and Current Update, and ensure the resulting Plan is internally consistent. Historical wording belongs in the amendment record rather than remaining as operative Plan guidance.

## Multi-Repository Work

- Keep one coordinating task in the lead repository and list every repository in `Repository` metadata.
- Record repository-specific steps and verification in that task.
- Create another repository-local task only when that repository needs independent resumption or handoff state.
- Commit each repository independently when commits are authorized.

## Consistency Rules

- `Ready`, `In Progress`, `Paused`, `Blocked`, `Verifying`, `Done`, `Cancelled`, and `Superseded` require a `Plan Locked` timestamp.
- `Blocked` requires an explicit unblock condition.
- `Paused` records why work paused and the next resumable step.
- `Done` requires completed acceptance criteria and verification results, or an explicit accepted limitation.
- `Cancelled` records a closeout reason.
- `Superseded` links the replacement task.
- `Updated` matches the latest material Progress entry.

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

- Included: [scope]
- Excluded: [scope]

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
