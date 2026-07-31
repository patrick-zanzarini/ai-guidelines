# Commit Guidelines

Use this guideline only when the user or repository workflow authorizes a commit. Also use this guideline when the user requests a commit message.

Repository-specific commit conventions replace the shared formatting defaults in this document. They do not permit changes to unrelated work. They do not weaken secret-safety requirements.

## Before Committing

1. Inspect `git status --short --untracked-files=all`.
2. Split independent changes when separate commits improve review or rollback.
3. Stage only files that belong to the requested change.
4. Inspect the complete staged diff for each text file.
5. Inspect the staged summary for each generated or binary file.
6. Run verification that is applicable to the staged change.
7. If verification changes proposed commit content, return to step 3.
8. Inspect `git status --short --untracked-files=all` again.
9. Inspect the complete staged diff again.
10. Check staged paths and content for credentials, tokens, private keys, personal data, and other secrets.
11. Confirm that each commit is atomic when practical.

Do not include, rewrite, discard, clean, or stage unrelated user changes.

## Commit Subject

When the repository does not define a different convention, use:

```text
type(optional-scope): concise imperative summary
```

Apply these rules:

- Use a lowercase type followed by a colon.
- Use an imperative verb such as `add`, `fix`, `move`, `update`, or `remove`.
- Describe the smallest accurate repository-visible change.
- Do not end the subject with a period.

Common types are `feat`, `fix`, `docs`, `test`, `refactor`, `perf`, `build`, `ci`, `chore`, and `revert`.

For a breaking change, add `!` before the colon. Explain the migration in the commit body.

```text
docs(workflow)!: replace plan and progress files with task records
```

## Commit Body

Add a body when the subject does not give sufficient context. Include only information that helps future readers:

- The reason for the change.
- The main behavior or workflow difference.
- Migration, risk, or follow-up information.

## Multi-Repository Work

For each repository:

1. Create a separate commit.
2. Keep the commit in the repository's scope.
3. Inspect repository status again.
4. Inspect staged content again.
5. Report related uncommitted work without staging it.
