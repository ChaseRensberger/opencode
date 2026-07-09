---
description: Suggest a Conventional Commits message for the current working changes
agent: plan
---

Suggest a commit message for the current working changes using Conventional Commits 1.0.0.

Inspect the repository changes before answering:
- Run `git status --short`
- Run `git diff --stat`
- Run `git diff --cached`
- Run `git diff`
- If untracked files are relevant, read only the necessary files to understand their purpose.

Rules:
- Do not modify files, stage changes, or create a commit.
- Prefer one concise commit message unless the changes clearly represent multiple unrelated commits.
- Use this format:

```text
<type>[optional scope]: <description>
```

- Use `feat` for new user-facing behavior, `fix` for bug fixes, and otherwise choose from `docs`, `style`, `refactor`, `perf`, `test`, `build`, `ci`, or `chore`.
- Use a scope only when there is a clear package, module, feature area, or configuration area.
- Use `!` or a `BREAKING CHANGE:` footer only when the diff clearly introduces a breaking API or behavior change.

Output:
1. The recommended commit message in a copyable code block.
2. A one-sentence rationale.
3. If the changes should be split into multiple commits, list the suggested commit messages instead.

Additional user guidance:
$ARGUMENTS
