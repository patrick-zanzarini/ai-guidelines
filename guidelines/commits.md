# Commit Guidelines

Use this guideline only when the user or an established repository workflow authorizes creating a commit or asks for a commit message.

Repository-local commit conventions override the shared formatting defaults below. They do not override preservation of unrelated changes or secret-safety requirements.

## Before Committing

- Inspect `git status --short --untracked-files=all`.
- Inspect the complete diff for every file that will be staged, including generated and binary-file summaries.
- Run verification appropriate to the staged change before committing.
- Check staged paths and content for credentials, tokens, private keys, personal data, and other secrets.
- Stage only files belonging to the requested change.
- Keep commits atomic where practical; split independent changes when doing so improves review or rollback.
- Do not include, rewrite, discard, clean, or stage unrelated user changes.

## Commit Subject

When the repository does not define another convention, use:

```text
type(optional-scope): concise imperative summary
```

Rules:

- Use a lowercase type followed by a colon.
- Use imperative mood: `add`, `fix`, `move`, `update`, or `remove`.
- Describe the smallest accurate repository-visible change.
- Do not end the subject with a period.

Common types are `feat`, `fix`, `docs`, `test`, `refactor`, `perf`, `build`, `ci`, `chore`, `revert`.

For a breaking change, use `!` before the colon and explain the migration in the body:

```text
docs(workflow)!: replace plan and progress files with task records
```

## Commit Body

Add a body when context is not obvious. Include only what helps future readers:

- Why the change exists.
- The main behavior or workflow difference.
- Migration, risk, or follow-up information.

## Multi-Repository Work

- Commit each repository separately.
- Keep each commit scoped to its repository.
- Recheck status and staged content in each repository.
- Report related uncommitted work without staging it.
