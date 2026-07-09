# AGENTS.md Maintenance Guide

This document explains how to maintain agent instructions using progressive disclosure: keep shared process rules in `ai-guidelines`, keep consuming repository roots minimal, keep domain-specific details in local domain files, and keep repo-specific cross-domain workflows in local `.ai/guidelines/` files.

## Principles

- **Shared `ai-guidelines/AGENTS.md`**: reusable process guidance and links to shared guidelines.
- **Consuming repository root `AGENTS.md`**: project summary, mandatory shared-instruction reference, and domain routing.
- **Domain files**: detailed instructions live in their respective folders inside the consuming repository.
- **Local `.ai/guidelines/` files**: repository-specific workflows that are broader than one source folder but not reusable enough for shared guidelines.
- **Load on demand**: agents read only what is needed for the current task.

## Choosing Where Guidelines Belong

Use progressive disclosure to keep instructions close to the work they govern and reusable rules in the shared repository.

| Instruction scope | Put it here | Purpose |
|-------------------|-------------|---------|
| Applies across multiple repositories | `ai-guidelines/guidelines/` | Reusable process, workflow, planning, progress, commit, and instruction-maintenance standards |
| Routes agents inside one repository | Consuming root `AGENTS.md` | Project summary, mandatory shared link, workspace map, domain routing, and rare project-wide exceptions |
| Applies to one folder, framework, or domain | Domain `AGENTS.md` | Implementation conventions, framework rules, naming, testing, and local design constraints for that domain |
| Applies across multiple local domains but is repo-specific | Consuming repo `.ai/guidelines/` | Detailed local workflows that should not bloat root `AGENTS.md` and are not yet shared standards |

Decision checklist:

- If the rule should affect more than one repository, add or update a shared guideline.
- If the rule only tells agents where to go inside one repository, keep it in root `AGENTS.md`.
- If the rule only affects one folder or domain, put it in that domain's `AGENTS.md`.
- If the rule is repo-specific but useful across multiple local domains, put it in `.ai/guidelines/` and link it from the relevant `AGENTS.md` files.

### Adding Shared Guidelines

When adding a new reusable guideline:

1. Create or update the owner document under `ai-guidelines/guidelines/`.
2. Add a row to `ai-guidelines/AGENTS.md` when creating a new guideline file.
3. Link from `workflow.md` only if the guideline changes mandatory task flow or execution gates.
4. In consuming repositories, link to the shared guideline instead of duplicating the full rule.

### Promoting Local Guidelines

Start a rule locally when it is repo-specific, experimental, or tied to one project's tooling. Promote it to shared only when it is reusable across repositories or clearly process-level.

When promoting a rule:

- Move the reusable rule into the shared owner document.
- Remove duplicate local wording.
- Keep only repository-specific exceptions in the consuming repository.

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

| Keep in Shared `ai-guidelines` | Keep in Consuming Root | Keep in Local `.ai/guidelines/` | Move to Domain File |
|-------------------------------|------------------------|--------------------------------|---------------------|
| Reusable workflow gates | One-sentence project description | Repo-specific cross-domain workflows | Framework-specific patterns |
| Planning/progress standards | Mandatory shared-instruction reference | Local test or verification procedures | Naming conventions |
| Interviewing guidance | Workspace/domain routing | Local tool usage that spans folders | Testing strategies |
| AGENTS maintenance process | Truly project-wide exceptions | Detailed local process notes | Code organization details |

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
├── guidelines/        # Repo-specific workflows broader than one domain
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
- [ ] Repo-specific cross-domain workflows are in local `.ai/guidelines/` files and linked from the relevant `AGENTS.md` files.
- [ ] Reusable process rules are in `ai-guidelines`.
- [ ] All links are valid.
- [ ] No redundant or obvious instructions remain.
