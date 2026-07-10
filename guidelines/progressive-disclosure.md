# AGENTS.md Maintenance Guide

Maintain agent instructions through progressive disclosure: reusable process rules live in `ai-guidelines`, consuming roots stay small and route work, domain details live near their domains, and repository-specific cross-domain workflows live under `.ai/guidelines/`.

## Instruction Layers

| Scope | Owner location | Content |
|-------|----------------|---------|
| Multiple repositories | `ai-guidelines/guidelines/` | Reusable workflow, tasks, commits, and instruction maintenance |
| One repository, project-wide | Consuming root `AGENTS.md` | Project summary, shared reference, routing, and explicit local exceptions |
| Multiple domains in one repository | `.ai/guidelines/` | Detailed local workflows and tooling |
| One folder, framework, or domain | Domain `AGENTS.md` | Implementation, naming, architecture, and testing rules for that area |

Each rule has one owner document. Other instruction files link to that owner and contain only necessary context or explicit exceptions.

## Local Exceptions

A consuming root may explicitly specialize shared defaults such as artifact location, branch conventions, package managers, verification commands, or approval requirements. State:

- The shared default being overridden.
- The replacement rule.
- The scope of the exception.
- A link to the local owner document when detailed guidance exists.

Local exceptions cannot weaken safety, preservation of user work, secret handling, or external-effect approval gates.

## Adding Or Promoting Guidance

When adding reusable guidance:

1. Choose one owner document under `guidelines/`.
2. Add it to the index in `AGENTS.md` if it is a new file.
3. Link it from `workflow.md` only when it affects mandatory task flow or gates.
4. Update README structure and migration notes when the public standard changes.

Start experimental or repository-specific rules locally. Promote them only when they apply across repositories. Remove duplicated local wording after promotion and retain only true exceptions.

## Maintenance Review

### Find contradictions

Compare shared, root, local workflow, and domain instructions. Decide which document owns each disputed rule and remove or convert other copies into links or explicit exceptions.

### Keep actionable guidance

Retain instructions that are specific enough to change behavior or protect important constraints. Rewrite vague guidance such as “write good tests” into repository-relevant expectations.

Do not delete a rule merely because it appears obvious or an agent may know it by default. Before deletion, ask:

- Is the behavior enforced more reliably elsewhere?
- Does the rule distinguish this repository or workflow?
- Is it specific and testable?
- Would removing it increase correctness, security, privacy, or operational risk?

Security-critical guidance, including secret protection and destructive-action constraints, remains explicit or routes to a clear owner document.

### Remove genuine clutter

Remove or consolidate instructions that are:

- Duplicated without adding scope-specific meaning.
- Outdated or tied to removed tooling.
- Too vague to affect behavior.
- In the wrong layer.
- Better enforced by reliable automation, provided the automation and ownership are documented.

## Recommended Structures

Shared repository:

```text
AGENTS.md
guidelines/
  workflow.md
  tasks.md
  interviewing.md
  commits.md
  progressive-disclosure.md
```

Consuming repository:

```text
AGENTS.md
domain-a/AGENTS.md
domain-b/AGENTS.md
.ai/
  guidelines/
  artifacts/
    tasks/
```

Task records are ignored workspace state; tracked durable documentation remains in the repository's normal documentation structure.

## Review Checklist

- [ ] No unresolved contradictions exist between instruction layers.
- [ ] Every reusable rule has one owner document.
- [ ] Local exceptions are explicit and scoped.
- [ ] Root instructions primarily summarize and route.
- [ ] Domain rules live near the work they govern.
- [ ] Security-critical instructions remain explicit or clearly routed.
- [ ] Shared indexes and README structure are current.
- [ ] Changed relative links resolve and `git diff --check` passes.
