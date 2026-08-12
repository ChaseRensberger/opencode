---
name: wingman-commits
description: Use when writing, reviewing, or suggesting Wingman git commit messages. Applies Conventional Commits 1.0.0 with Wingman-specific commit hygiene.
---

# Wingman Commits

Use this skill when writing, reviewing, or suggesting commit messages for Wingman.

## Core Rule

Use Conventional Commits 1.0.0. Commit messages must be explicit, scoped when useful, and honest about the change.

Default shape:

```text
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

## Before Writing A Commit

Inspect the intended diff before proposing a message:

```sh
git status
git diff --staged
git diff
```

If the user asks you to commit, also inspect recent style:

```sh
git log --oneline -10
```

Stage only the files that belong to the requested change. Never use `git add -A`, `git commit -a`, or stage unrelated dirty work.

## Required Format

The first line must include:

- A type, such as `feat`, `fix`, `docs`, `test`, or `chore`
- An optional noun scope in parentheses
- An optional `!` for breaking changes
- A colon and space
- A short description

Examples:

```text
fix(provider): handle missing model refs
feat(web): add session history detail
docs: document provider configuration
test(api): cover agent creation validation
```

## Types

Use the narrowest truthful type.

- `feat`: Adds a user-visible feature or capability. SemVer minor.
- `fix`: Fixes a bug. SemVer patch.
- `docs`: Documentation-only changes.
- `test`: Adds or changes tests without changing runtime behavior.
- `refactor`: Restructures code without changing behavior.
- `perf`: Improves performance.
- `build`: Build system, packaging, release, or dependency pipeline changes.
- `ci`: CI workflow changes.
- `chore`: Maintenance that does not fit another type.
- `style`: Formatting-only changes with no behavior change.
- `revert`: Reverts previous commits.

Prefer `fix`, `feat`, `docs`, or `test` over `chore` when they apply.

## Scopes

Use a scope when it clarifies the affected area. Keep scopes lowercase, short, and noun-like.

Good Wingman scopes include:

- `api`
- `agent`
- `config`
- `docs`
- `history`
- `provider`
- `session`
- `tool`
- `ui`
- `web`

Omit the scope when the change is broad or the type already carries enough context.

## Descriptions

Write the description in imperative mood and lowercase unless a proper noun requires capitalization.

Good:

```text
fix(session): preserve tool errors in history
docs: clarify supported provider setup
```

Avoid:

```text
fixed session history bug
update docs
misc cleanup
```

The description should complete this sentence: "This commit will ..."

## Bodies

Use a body when the commit needs context that does not fit in the title.

The body must begin one blank line after the description. Use it to explain why the change was needed, important tradeoffs, or non-obvious behavior.

Example:

```text
fix(provider): reject empty model refs

Provider config accepted empty model refs and failed later during session
startup. Validate the value while loading config so users get an actionable
error before starting an agent.
```

Do not add a body just to restate the diff.

## Footers

Footers are optional and must appear one blank line after the body, or one blank line after the description if there is no body.

Footer tokens use `-` instead of spaces, except `BREAKING CHANGE`.

Examples:

```text
Refs: WING-123
Reviewed-by: Chase
BREAKING CHANGE: provider config no longer accepts implicit model ids
```

## Breaking Changes

Breaking changes must be marked with either `!` in the prefix or a `BREAKING CHANGE:` footer. Use both when the title benefits from the warning and the footer needs detail.

Examples:

```text
feat(config)!: require provider prefixes in model refs

BREAKING CHANGE: model refs must now use provider/model form.
```

```text
fix(api)!: remove legacy session payload shape
```

`BREAKING CHANGE` must be uppercase. `BREAKING-CHANGE` is equivalent in footers, but prefer `BREAKING CHANGE`.

## Reverts

Use `revert` for commits that undo previous work. Include references when useful.

Example:

```text
revert: restore previous provider discovery behavior

Refs: abc1234
```

## Commit Splitting

If the diff legitimately needs more than one type, prefer multiple commits when feasible.

Examples:

- Runtime bug fix plus new docs: usually split into `fix` and `docs`.
- Feature plus tests for that feature: usually one `feat` commit.
- Refactor plus behavior change: split unless the refactor is purely incidental and small.

## Review Checklist

When reviewing a proposed commit message, check:

- The type accurately describes the user-visible or maintenance intent.
- The scope, if present, names the affected area.
- The description is specific and imperative.
- Breaking changes are marked with `!` or `BREAKING CHANGE:`.
- The body explains why when needed.
- Footers follow git-trailer-like syntax.
- The message does not claim unrelated work.

## Source

Based on Conventional Commits 1.0.0:

https://www.conventionalcommits.org/en/v1.0.0/
