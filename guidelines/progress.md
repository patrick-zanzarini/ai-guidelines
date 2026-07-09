# Progress Tracking Guidelines

Guidelines for maintaining a consuming repository's active `.ai/artifacts/progress/progress.md` so agents can resume implementation quickly.

---

## Canonical File

- Keep active implementation state in `.ai/artifacts/progress/progress.md`.
- Treat `.ai/artifacts/progress/progress.md` as the single active feature record.
- Keep archived or resumable progress records in `.ai/artifacts/progress/{sequence}_progress-{description}.md`.
- Keep planning artifacts in `.ai/artifacts/plans/`; link them from progress files instead of duplicating plan text.

---

## Switching Active Progress

- Use `progress.md` only for the current active plan or tracked implementation.
- Start archive sequences at `01`, increment them in archive order, and keep at least two digits (`01`, `02`, ... `99`, `100`).
- Before starting a different persisted plan, rename the current `progress.md` to `{sequence}_progress-{description}.md`, where `{sequence}` is the next zero-padded archive number and `{description}` is a short kebab-case feature description.
- When resuming a previous plan, first archive the current `progress.md` if it exists, then rename that plan's `{sequence}_progress-{description}.md` back to `progress.md`.
- If no active work is being tracked, `.ai/artifacts/progress/` may contain only archived `{sequence}_progress-{description}.md` files.
- Do not keep duplicate active progress records for the same plan.

---

## Workflow Authority

- [Workflow](workflow.md) defines execution timing gates.
- This file defines `.ai/artifacts/progress/progress.md` content, switching behavior, structure, and consistency requirements.

---

## Required File Structure

Use this structure in `.ai/artifacts/progress/progress.md`:

1. `# Feature: [Feature Name]`
2. Metadata block (`Status`, `Started`, `Target Branch`, `Plan`)
3. `## 1. Overview`
4. `## 2. Implementation Plan` with phase checklists
5. `## 3. Current Status` with latest timestamped update
6. `## 4. Decisions & Known Issues` with dated entries

### Metadata Rules

- `Status` must be one of: `In Progress`, `Testing`, `Blocked`, `Done`, `Cancelled`.
- `Started` uses `YYYY-MM-DD`.
- `Target Branch` should match the active git branch goal.
- `Plan` must link to a `.ai/artifacts/plans/*.md` file when one exists; otherwise set `none`.

---

## Implementation Plan Rules

- Organize work by phases, for example: Setup, Core Logic, UI/UX, Verification.
- Use markdown checkboxes for tasks (`- [ ]` / `- [x]`).
- Mark blockers inline using `**BLOCKER:**`.
- Keep at most one phase actively progressing at a time.
- Move completed tasks to checked items; do not delete completed history during active work.

---

## Current Status Rules

- Update `Latest Update` every time progress changes.
- Keep update text short and actionable: what is done, what is active, what is next.
- If blocked, clearly state the unblock condition.

---

## Decisions & Known Issues Rules

- Record decisions with date and rationale:
  - `**[YYYY-MM-DD] Decision:** ...`
- Record known issues with date and current state:
  - `**[YYYY-MM-DD] Issue:** ...`
- Keep unresolved issues visible until closed.

---

## Consistency Checks Required

After each update, verify there are no contradictions:

- `Status` matches checklist state, for example, `Done` is not valid with unchecked required verification tasks.
- `Blocked` status includes at least one explicit blocker.
- `Cancelled` status includes a closeout reason in `Decisions & Known Issues`.
- `Current Status` aligns with active phase and next task.
- `Latest Update` reflects the most recent phase completion or implementation step.
- Decisions and issues are consistent with blockers and progress claims.

---

## Edge Cases

- **No plan exists yet:** `progress.md` tracking is optional; if used, set `Plan` to `none` and add a dated decision explaining why.
- **Hotfix starts before plan or branch naming is final:** keep current `Target Branch`, then update metadata once finalized.
- **Work stops due to priority change or dependency:** use `Blocked` and include resume condition.
- **Verification cannot run due to environment or tooling outage:** keep `Status` as `Blocked` or `Testing`, add explicit blocker, and list pending checks in the verification phase.
- **Large feature with many sessions:** keep one feature record and continue phase checklists; do not create parallel active feature records.

---

## Suggested Improvements

- Add explicit verification exit criteria in the verification phase for each feature.
- Add owner or ETA details to blocker lines when available.
- Keep `Latest Update` timestamps in consistent local format (`YYYY-MM-DD HH:MM`).
- Close resolved issues by appending outcome and resolution date.

---

## When to Archive Or Replace `progress.md`

Replace `progress.md` with a new feature record only when:

1. Current feature status is `Done` or `Cancelled`.
2. Final `Latest Update` and remaining follow-ups are captured.
3. New work is materially different in scope.

Archive procedure for incomplete or resumable work:

1. Update `Current Status` with the pause or handoff state.
2. Rename `.ai/artifacts/progress/progress.md` to `.ai/artifacts/progress/{sequence}_progress-{description}.md` using the next archive sequence number.
3. Create or restore `.ai/artifacts/progress/progress.md` for the newly active plan.

Replacement procedure for completed or cancelled work:

1. Finalize current feature state in `Current Status`.
2. Rename the completed record to `{sequence}_progress-{description}.md` if future reference is useful, or replace it only when the repository does not need a separate archive.
3. Carry forward only unresolved items that apply to the new scope.

Resume procedure:

1. Archive the current `progress.md` if another task is active.
2. Rename the target `.ai/artifacts/progress/{sequence}_progress-{description}.md` to `.ai/artifacts/progress/progress.md`.
3. Update `Latest Update` to describe the resumed state before implementation edits.

---

## Template

```markdown
# Feature: [Feature Name]

**Status:** [In Progress / Testing / Blocked / Done / Cancelled]
**Started:** YYYY-MM-DD
**Target Branch:** [e.g., develop]
**Plan:** `../plans/01_feature-name_plan-name.md` or none

## 1. Overview
[Brief description of the feature, user story, or main objective.]

## 2. Implementation Plan

### Phase 1: Setup & Scaffolding
- [ ] [task]

### Phase 2: Core Logic
- [ ] [task]
- [ ] **BLOCKER:** [what is blocked and why]

### Phase 3: UI/UX
- [ ] [task]

### Phase 4: Verification
- [ ] [task]

## 3. Current Status
> **Latest Update:** [YYYY-MM-DD HH:MM]
> Working on [Task Name]. [Current state + immediate next step.]

## 4. Decisions & Known Issues
- **[YYYY-MM-DD] Decision:** [decision and rationale]
- **[YYYY-MM-DD] Issue:** [issue and current investigation state]
```
