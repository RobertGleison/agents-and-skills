---
name: commit_writter
description: Always use this skill when committing code changes. Trigger on any commit, git commit, save changes, or commit message task.
---

# Commit
ALWAYS follow this workflow when committing. Never run `git commit` without it.

## Prerequisites

Before committing, check the current branch:

```bash
git branch --show-current
```

**If you're on `main` or `master`, you MUST create a feature branch first** — unless the user explicitly asked to commit to main. Do not ask the user whether to create a branch; just proceed with branch creation using the `create-branch` skill. After it completes, verify the branch changed:

```bash
git branch --show-current
```

If still on `main` or `master` (e.g., the user aborted branch creation), stop — do not commit.

## Phase 1: Review Changes

```bash
git status
git diff --staged
```

If nothing is staged, identify which files should be staged. Group related changes into logical commits — one concern per commit.

**Never commit:**
- `.env`, credentials, secrets, API keys
- Large binaries or generated files
- Unrelated changes (split into separate commits)

## Phase 2: Generate Commit Message

### Format

```
type: concise description

[optional body — explain WHY, not WHAT]
```

### Types

| Type | When |
|------|------|
| `feat` | New feature or capability |
| `fix` | Bug fix |
| `docs` | Documentation only |
| `style` | Formatting, no logic change |
| `refactor` | Code restructure, no behavior change |
| `perf` | Performance improvement |
| `test` | Adding or fixing tests |
| `build` | Build system or dependencies |
| `ci` | CI/CD configuration |
| `chore` | Maintenance, tooling, config |
| `revert` | Reverting a previous commit |

### Rules

- **Subject line:** imperative mood, lowercase, no period, max 72 chars
- **Body:** wrap at 72 chars, explain motivation and context when non-obvious
- **No ticket IDs in commits** — tickets are linked in the PR

### AI Attribution
Never add coauthored by any agent. The only author is me.

## Phase 3: Commit

```bash
git add <specific files>
git commit -m "$(cat <<'EOF'
type: description

optional body
EOF
)"
```

Verify with `git log --oneline -3` after committing.

## Commit Sizing

Prefer small, focused commits:
- **One logical change per commit** — don't mix a bug fix with a refactor
- **Tests with implementation** — test changes go in the same commit as the code they test
- **If you can't summarize in 72 chars, the commit is too big** — split it

## Examples

### Simple fix

```
fix: handle expired refresh tokens gracefully

The refresh token flow silently failed for tokens older than 30 days,
causing users to be logged out without a re-auth prompt. Now returns
a proper 401 with a refresh hint.
```

### Feature with scope

```
feat: add patient enrollment endpoint

Adds POST /api/v1/patients/enroll for batch patient enrollment.
Validates insurance data against the eligibility service before
persisting.
```

### Refactor

```
refactor: extract shared validation logic

Move duplicate validation code from three endpoints into a shared
validator class. No behavior change.
```

### One-liners (for small changes)

```
fix: handle expired refresh tokens gracefully
test: add coverage for rate limiting edge cases
ci: add Go lint step to PR workflow
docs: update API authentication guide
```