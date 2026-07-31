# Interviewing And Discovery

Use this guideline to resolve important uncertainty before you lock a task Plan or make a consequential implementation choice.

## Inspect First

Before you ask the user a question:

1. Read the applicable instructions.
2. Read the applicable source-of-truth documents.
3. Inspect the applicable code, configuration, tests, schemas, and current behavior.
4. Separate discoverable facts from product preferences and tradeoffs.
5. Resolve facts from the repository or system when practical.

Do not ask the user to find information that you can safely discover from the available context.

## Discovery Categories

| Category | Focus |
|----------|-------|
| Unclear specifications | Ambiguous behavior, undefined rules, and missing acceptance criteria |
| Contradictions | Conflicting requirements, documentation, designs, or existing behavior |
| Edge cases | Boundaries, errors, validation, permissions, and exceptional paths |
| Potential issues | Security, performance, compatibility, migration, integration, and operational risks |
| Scope | Boundaries, affected users or systems, dependencies, and whether to split the work |

The categories do not have fixed priorities. Assign an impact level to each issue:

- `Blocker`: You would have to guess about a material decision to lock the Plan or implement the change.
- `High`: The answer changes architecture, user-visible behavior, security, data handling, or major effort.
- `Medium`: The answer changes a contained implementation choice or acceptance detail.
- `Low`: You can use a reasonable default with little risk.

## Ask Questions

- Ask only a question that materially improves correctness or alignment.
- Ask about blockers before lower-impact issues.
- Ask about high-impact tradeoffs before medium-impact or low-impact issues.
- Group a small number of related questions.
- Do not use the discovery categories as a question checklist.
- Give concrete options when the choice is bounded.
- Recommend a default.
- Explain the important tradeoff of the recommended default.
- Ask a follow-up question only when an answer identifies another material ambiguity.

## Assumptions And Deferrals

- Record a reasonable default for low-impact uncertainty.
- Record each implementation or verification assumption in the task Plan.
- The user may explicitly defer a blocker.
- Record each blocker deferral.
- Record the consequence of a deferred blocker.
- Record when the deferred decision must be made.
- Do not let a request to skip questions override a safety gate.
- Do not let a request to skip questions override external-effect approval.
- Do not let a request to skip questions override a blocking product decision.

## When Discovery Can Be Brief

Use brief discovery or no questions when one of the following conditions applies:

- The request and acceptance criteria contain all necessary decisions.
- A simple defect has a clear reproduction and expected behavior.
- The repository defines one clear existing pattern.
- The change is small and low risk.
- The user has already made the applicable decisions.

Discovery is complete when all blockers are resolved or explicitly deferred. Remaining assumptions must be safe to record.
