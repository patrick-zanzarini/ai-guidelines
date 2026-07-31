# AGENTS.md Maintenance Guide

Use progressive disclosure to maintain agent instructions. Store reusable process rules in `ai-guidelines`. Keep consuming root instructions small and use them to route work. Store domain instructions near their domains. Store repository-specific cross-domain workflows in `.ai/guidelines/`.

## Instruction Layers

| Scope | Owner location | Content |
|-------|----------------|---------|
| Multiple repositories | `ai-guidelines/guidelines/` | Reusable workflow, tasks, commits, and instruction maintenance |
| One repository, project-wide | Consuming root `AGENTS.md` | Project summary, shared reference, routing, and explicit local exceptions |
| Multiple domains in one repository | `.ai/guidelines/` | Detailed local workflows and tooling |
| One folder, framework, or domain | Domain `AGENTS.md` | Implementation, naming, architecture, and testing rules for that area |

Each rule must have one owner document. Other instruction files must link to the owner. They must contain only necessary context or explicit exceptions.

## Local Exceptions

A consuming root may define an explicit exception to a shared default. Examples include artifact locations, branch conventions, package managers, verification commands, and approval requirements.

For each exception, state:

- The shared default that the exception replaces.
- The replacement rule.
- The scope of the exception.
- A link to the local owner document when detailed guidance exists.

A local exception cannot weaken safety, preservation of user work, secret handling, or external-effect approval gates.

## Add Or Promote Guidance

When you add reusable guidance:

1. Select one owner document in `guidelines/`.
2. Add a new file to the index in `AGENTS.md` when applicable.
3. Link the owner document from `workflow.md` only when the guidance affects a mandatory task flow or gate.
4. Update the README structure when the public standard changes.
5. Update README migration notes when the public standard changes.

Start an experimental or repository-specific rule in the applicable local instructions. Promote the rule only when it applies to multiple repositories. After promotion, remove duplicate local wording. Keep only explicit local exceptions.

## Maintenance Review

### Find Contradictions

1. Compare shared, root, local workflow, and domain instructions.
2. Identify the owner document for each disputed rule.
3. Remove each unnecessary copy of the rule.
4. Replace each necessary scoped copy with a link or explicit exception.

### Keep Actionable Guidance

Keep instructions that are specific enough to change behavior or protect an important constraint. Replace vague guidance such as “write good tests” with repository-specific expectations.

Do not delete a rule only because the rule appears obvious or an agent already knows the rule. Before you delete a rule, answer these questions:

- Does another instruction or reliable control enforce the behavior more reliably?
- Does the rule distinguish this repository or workflow?
- Is the rule specific and testable?
- Would removal increase risk to correctness, security, privacy, or operations?

Keep security-critical guidance explicit or link to a clear owner document. Security-critical guidance includes secret protection and destructive-action constraints.

### Remove Genuine Clutter

Remove or consolidate an instruction when one of these conditions applies:

- The instruction duplicates another instruction and adds no scope-specific meaning.
- The instruction is outdated or refers to removed tooling.
- The instruction is too vague to affect behavior.
- The instruction is in the incorrect layer.
- Reliable automation enforces the instruction, and the automation and ownership are documented.

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

Task records are ignored workspace state. Store durable documentation in the repository's tracked documentation structure.

## Review Checklist

- [ ] Resolve all contradictions between instruction layers.
- [ ] Give each reusable rule one owner document.
- [ ] Make each local exception explicit and scoped.
- [ ] Keep root instructions focused on summary and routing.
- [ ] Store domain rules near the work that they govern.
- [ ] Keep security-critical instructions explicit or link to a clear owner.
- [ ] Update shared indexes and the README structure.
- [ ] Confirm that changed relative links resolve.
- [ ] Confirm that `git diff --check` passes.
