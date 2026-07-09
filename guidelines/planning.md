# Planning

Guidelines for creating implementation plans through structured discovery.

---

## File Output

- **Location**: Save all plans to the consuming repository's `.ai/artifacts/plans/` folder.
- **Naming**: Use date-prefixed format: `YYYY-MM-DD_{feature-name}_{plan-name}.md`.
  - Example: `.ai/artifacts/plans/2026-01-30_authentication_oauth-integration.md`
  - Example: `.ai/artifacts/plans/2026-01-30_dashboard_performance-refactor.md`
- **One plan per task**: Each distinct task gets its own plan file.
- **Update, don't duplicate**: If revisiting a plan, update the existing file rather than creating a new one.
- **Persistence rule**: Interactive plan approval does not write files; create or update the `.ai/artifacts/plans/*.md` file before implementation work starts.

## Workflow Authority

- [Workflow](workflow.md) defines workflow sequencing and planning gates.
- This file defines planning artifact standards only.

---

## Interview Content for Planning

Use [Interviewing](interviewing.md) to gather and document clarifications that affect plan quality.

### Planning-Specific Emphasis

| Category | Priority | Why Critical |
|----------|----------|--------------|
| Contradictions | Blocker | Resolve conflicts before proceeding |
| Unclear Specs | Blocker | Missing details cause rework |
| Potential Issues | High | Technical risks affect approach |
| Edge Cases | High | Boundary conditions impact design |
| Scope | Medium | Determine if task should be split into phases |

### When Interview Content May Be Abbreviated

Use abbreviated discovery notes in the plan when:

- User explicitly states: "Skip interview and proceed directly".
- Task is a trivial bug fix with clear reproduction steps.
- User provides answers to standard interview questions upfront.

---

## Plan Output Format

### Rules

| Rule | Rationale |
|------|-----------|
| **No code blocks** | Plans describe what to change, not how to write it |
| **Use symbol refs** | Reference `methodName` or `ClassName` instead of code |
| **Use file links** | Link to repository paths for navigation |
| **Concise steps** | Keep steps actionable, not explanatory |
| **No implementation** | Save implementation details for execution phase |

### Exception: Non-Obvious Decisions

Include minimal code snippets only when:

- Demonstrating a non-obvious architectural decision.
- Showing a pattern choice between multiple valid approaches.
- Clarifying an API contract or interface shape.

### Structure

```markdown
## Plan: [Brief Title]

[1-2 sentence summary of what will be accomplished]

### Steps

1. [Action verb] [target] - [brief rationale if non-obvious]
2. ...

### Considerations

- [Open question or decision point]
- [Risk or dependency to monitor]
```

---

## Iterative Planning

If discovery reveals significant gaps:

1. Pause plan creation.
2. Ask clarifying questions.
3. Resume only after critical uncertainties are resolved.

Do not draft a plan with unresolved blockers; document them as questions instead.
