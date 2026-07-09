# AGENTS.md Maintenance Guide

This document explains how to maintain `AGENTS.md` files using progressive disclosure: keep shared process rules in `ai-guidelines`, keep consuming repository roots minimal, and keep domain-specific details in local domain files.

## Principles

- **Shared `ai-guidelines/AGENTS.md`**: reusable process guidance and links to shared guidelines.
- **Consuming repository root `AGENTS.md`**: project summary, mandatory shared-instruction reference, and domain routing.
- **Domain files**: detailed instructions live in their respective folders inside the consuming repository.
- **Load on demand**: agents read only what is needed for the current task.

## Maintenance Process

When adding or revising instructions, follow these five steps.

### 1. Find Contradictions

Identify instructions that conflict with each other across shared, root, and domain files.

Examples of contradictions:

- Shared workflow says to persist a plan before implementation, but a local root says plans are optional for the same task type.
- Root says to use one package manager, but a domain file says to use another.
- Multiple files define the same convention differently.

Action: for each contradiction, decide which version owns the rule and update or remove the other.

### 2. Identify the Essentials

Extract only what belongs in each layer.

| Keep in Shared `ai-guidelines` | Keep in Consuming Root | Move to Domain File |
|-------------------------------|------------------------|---------------------|
| Reusable workflow gates | One-sentence project description | Framework-specific patterns |
| Planning/progress standards | Mandatory shared-instruction reference | Naming conventions |
| Interviewing guidance | Workspace/domain routing | Testing strategies |
| AGENTS maintenance process | Truly project-wide exceptions | Code organization details |

Rule: if an instruction only matters for one domain, put it in that domain file.

### 3. Group the Rest

Organize remaining instructions into logical categories within domain files, such as:

- Runtime or framework conventions.
- Dependency and package-manager rules.
- State, data, or persistence rules.
- Testing and verification rules.
- Documentation or content standards.

### 4. Create the File Structure

Recommended shared repository structure:

```text
ai-guidelines/
├── AGENTS.md
└── guidelines/
    ├── workflow.md
    ├── planning.md
    ├── interviewing.md
    ├── progress.md
    └── progressive-disclosure.md
```

Recommended consuming repository structure:

```text
AGENTS.md              # Root: project summary, shared-instruction reference, domain routing
domain-a/
└── AGENTS.md          # Domain-specific instructions
domain-b/
└── AGENTS.md          # Domain-specific instructions
.ai/
└── artifacts/
    ├── plans/         # Consuming-repository plans
    └── progress/      # Active progress.md plus archived progress-{description}.md files
```

When adding a new reusable guideline, place it under `ai-guidelines/guidelines/` and add a row for it in `ai-guidelines/AGENTS.md`.

### 5. Flag for Deletion

Remove instructions that are:

| Type | Example | Why Delete |
|------|---------|------------|
| **Redundant** | "Use meaningful variable names" | AI already knows this |
| **Too vague** | "Write good tests" | Not actionable |
| **Overly obvious** | "Don't commit secrets" | Universal knowledge |
| **Outdated** | References to removed libraries | No longer relevant |
| **Duplicate** | Same rule in multiple files | Keep one source of truth |

Questions to ask:

- Would an experienced developer need this instruction?
- Is this specific enough to change behavior?
- Does the AI already follow this pattern by default?

## Review Checklist

Before committing `AGENTS.md` changes:

- [ ] No contradictions between shared, root, and domain files.
- [ ] Consuming root file fits on one screen when practical.
- [ ] Each instruction is actionable and specific.
- [ ] Domain-specific rules are in domain files.
- [ ] Reusable process rules are in `ai-guidelines`.
- [ ] All links are valid.
- [ ] No redundant or obvious instructions remain.
