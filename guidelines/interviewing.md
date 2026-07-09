# Interviewing

Structured discovery process for clarifying requirements before implementation.

---

## Interview Categories

| Category | Focus |
|----------|-------|
| Unclear Specifications | Ambiguous requirements, undefined business rules, missing detail |
| Contradictions | Conflicts between requirements or with existing behavior |
| Edge Cases | Boundary conditions, error scenarios, validation limits |
| Potential Issues | Technical constraints, integrations, performance, security |
| Scope | Task boundaries, affected user roles, complexity assessment |

---

## Category Details

### Unclear Specifications

Ask about:

- Ambiguous requirements or missing details in user flows.
- Undefined business rules or logic.
- Vague acceptance criteria that need clarification.
- Missing context about existing functionality.

Example questions:

- "What should happen when the user clicks X but condition Y is not met?"
- "Is there a specific business rule for how Z should be calculated?"
- "What existing functionality does this feature interact with?"

### Contradictions

Ask about:

- Requirements that conflict with each other.
- Behavior that contradicts existing functionality.
- Inconsistencies between design and stated requirements.
- Conflicting stakeholder expectations.

Example questions:

- "This requirement says X, but the existing behavior does Y. Which is correct?"
- "The design shows A, but the description mentions B. Which takes precedence?"
- "These two acceptance criteria seem to conflict. Can you clarify the expected behavior?"

### Edge Cases

Inquire about:

- Boundary conditions and limits.
- Error scenarios and exception handling.
- Exceptional user paths.
- Data validation limits and constraints.
- Permission edge cases.
- Unusual but possible user interactions.

Example questions:

- "What happens if the user submits an empty form?"
- "How should the system behave when the API is unavailable?"
- "Are there any character limits or format restrictions for this field?"

### Potential Issues

Discuss:

- Technical constraints or limitations.
- Integration dependencies with other systems.
- Performance considerations and expected load.
- Security implications and data protection needs.
- Data migration requirements.
- Backward compatibility with existing features.

Example questions:

- "Does this feature depend on any external APIs or services?"
- "Are there performance requirements, such as response time under 2 seconds?"
- "Will this change affect any existing user workflows?"

### Scope

Confirm:

- Whether the task should be split into smaller parts.
- Which user roles are affected.
- Expected complexity level.
- Dependencies on other work.

Example questions:

- "Should this be one task or broken into multiple smaller tasks?"
- "Which user roles need access to this feature?"
- "Are there any prerequisites that must be completed first?"

---

## Interview Guidelines

1. Use a conversational approach and ask follow-up questions based on responses.
2. Continue iterative clarification until critical uncertainties are resolved.
3. Document important decisions made during discovery.
4. Prioritize blockers that would prevent implementation.

---

## When to Skip Interview

The interview can be abbreviated or skipped when:

- User provides a detailed specification with clear acceptance criteria.
- Task is a simple bug fix with clear reproduction steps.
- User explicitly requests to skip and proceed directly.
- Task is a trivial change with obvious implementation.
