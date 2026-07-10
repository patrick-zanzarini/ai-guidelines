# Interviewing And Discovery

Guidance for resolving decision-relevant uncertainty before locking a task Plan or making a consequential implementation choice.

## Inspect First

Before questioning the user:

1. Read applicable instructions and source-of-truth documents.
2. Inspect relevant code, configuration, tests, schemas, and current behavior.
3. Separate discoverable facts from product preferences and tradeoffs.
4. Resolve facts from the repository or system whenever practical.

Do not ask the user to locate information that can be discovered safely from available context.

## Discovery Categories

| Category | Focus |
|----------|-------|
| Unclear specifications | Ambiguous behavior, undefined rules, missing acceptance criteria |
| Contradictions | Conflicting requirements, documentation, designs, or existing behavior |
| Edge cases | Boundaries, errors, validation, permissions, and exceptional paths |
| Potential issues | Security, performance, compatibility, migration, integration, and operational risk |
| Scope | Boundaries, affected users or systems, dependencies, and whether work should be split |

Categories do not have fixed priorities. Classify each discovered issue by its impact:

- `Blocker`: implementation or Plan locking would require guessing about a material decision.
- `High`: the answer changes architecture, user-visible behavior, security, data handling, or major effort.
- `Medium`: the answer changes a contained implementation choice or acceptance detail.
- `Low`: a reasonable default can be used with little risk.

## Asking Questions

- Ask only questions whose answers materially improve correctness or alignment.
- Prioritize blockers, then high-impact tradeoffs.
- Batch a small number of related questions instead of running a category checklist.
- Present concrete options when the choice is bounded.
- Recommend a default and explain its meaningful tradeoff.
- Ask follow-up questions only when the response reveals another material ambiguity.

## Assumptions And Deferral

- Document reasonable defaults for low-impact uncertainty.
- Record assumptions that affect implementation or verification in the task Plan.
- A user may explicitly defer a blocker; record the deferral, its consequence, and the later decision point.
- Do not let a request to skip interviews override safety, external-effect approval, or a genuinely blocking product decision.

## When Discovery Can Be Brief

Brief or no questioning is appropriate when:

- The request and acceptance criteria are already decision-complete.
- A simple bug has clear reproduction and expected behavior.
- The repository establishes an unambiguous existing pattern.
- The change is trivial and low risk.
- The user has already provided the relevant decisions.

Discovery is complete when blockers are resolved or explicitly deferred and remaining assumptions are safe to document.
