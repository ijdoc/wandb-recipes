# Contributing to wandb-recipes

This guide covers the development workflow for contributing to wandb-recipes. All changes — new recipes, bug fixes, and documentation — follow the same process.

## Workflow: Issue → Branch → PR

### 1. Create an Issue

```bash
gh issue create --title "Issue title" --body "Description..." --label "label"
```

- Describe the problem or recipe clearly
- Propose an approach
- List affected files or recipes

### 2. Create a Branch

```bash
git checkout -b fix/42-issue-description
# or
git checkout -b feature/42-issue-description
```

- **Always include the issue number** immediately after the prefix (e.g. `fix/42-`, `feature/42-`)
- Use a short, descriptive slug after the number
- Prefix with `fix/`, `feature/`, `docs/`, `refactor/`, `chore/`, etc.

### 3. Implement Changes

- Keep changes scoped to a single recipe when possible
- Update documentation alongside code (see [Documentation Principles](../README.md#documentation-principles))
- Follow [Code Style](./code-style.md)

### 4. Commit and Push

Follow [Conventional Commits](https://www.conventionalcommits.org/) format:

```
<type>(<scope>): <subject>

<body>

<footer>
```

**Types:**
- `feat`: New recipe or new capability in an existing recipe
- `fix`: Bug fix
- `docs`: Documentation only changes
- `style`: Code style changes (formatting, etc.)
- `refactor`: Code change that neither fixes a bug nor adds a feature
- `perf`: Performance improvements
- `test`: Adding or updating tests
- `build`: Changes to build system or dependencies
- `ci`: Changes to CI configuration (e.g. `.github/workflows/`)
- `chore`: Other changes that don't modify source or test files

**Scope** is typically the recipe directory (e.g. `stop-multiple-runs`, `graphql`) or `docs`, `ci`.

**Examples:**

```bash
# IMPORTANT: Stage ONLY the files changed for this specific commit.
# Never use 'git add .', 'git add -A', or 'git commit -a'.
git add stop-multiple-runs/stop_runs.py docs/contributing/README.md

git commit -m "fix(stop-multiple-runs): handle missing run state

- Treat None state as not-running rather than raising
- Add early return when no duplicates are found

Fixes #12"

git push -u origin fix/12-handle-missing-state
```

**Commit Message Rules:**

1. **Subject line (first line)**:
   - Use imperative mood ("add" not "added" or "adds")
   - Don't capitalize first letter after colon
   - No period at the end
   - Maximum 72 characters

2. **Body (optional)**:
   - Separate from subject with blank line
   - Explain WHAT and WHY, not HOW
   - Use bullet points for multiple changes
   - Wrap at 72 characters

3. **Footer (optional)**:
   - Reference issues: one keyword per line — `Fixes #123`, `Closes #45`, `Relates to #67`
   - Multiple issues: use separate lines, not comma-separated (`Closes #45, #46` is not reliably parsed by GitHub)
   - Breaking changes: `BREAKING CHANGE: <description>`

### 5. Critical Git Practices

- **DO** stage specific files: `git add file1.py file2.md`
- **DON'T** use `git add .`, `git add -A`, or `git commit -a` — these stage everything, including unrelated work-in-progress and files that should stay untracked
- **DO** review staged changes with `git diff --cached` before committing
- **DO** keep commits atomic — one logical change per commit

Why explicit staging matters: it prevents accidentally committing unrelated changes from parallel work, temporary files, experiments, or files that should remain untracked.

### 6. Dependency Management (Lock Files)

When a recipe declares dependencies, the lock file must be regenerated and committed in the same commit as the manifest change. Otherwise other people (and CI) get a different dependency tree than you do.

**For recipes using `uv` / `pyproject.toml`:**

```bash
cd <recipe-dir>
# 1. Edit pyproject.toml
# 2. Regenerate the lock file
uv lock
# 3. Stage both files together
git add pyproject.toml uv.lock
git commit -m "feat(<recipe>): add <dependency>"
```

**For recipes using `pipenv` / `Pipfile`:**

```bash
cd <recipe-dir>
# 1. Edit Pipfile (or use `pipenv install <pkg>`)
# 2. Regenerate the lock file
pipenv lock
# 3. Stage both files together
git add Pipfile Pipfile.lock
git commit -m "feat(<recipe>): add <dependency>"
```

Never commit a `Pipfile`/`pyproject.toml` change without the corresponding lock file update.

### 7. Create a Pull Request

```bash
gh pr create --title "Title" --body "Description..." --base main
```

- Reference the issue in the PR body — `Fixes #N` on its own line
- Explain what was changed and why
- List what you tested

### 8. Merge After Review

```bash
gh pr merge <PR-number> --squash --delete-branch
```

## Why This Workflow?

- Creates a clear history of changes
- Enables discussion before implementation
- Makes review easy
- Allows reverting cleanly if needed
- Documents the reasoning behind each change

## Adding a New Recipe

1. **Open an issue** describing the recipe and its purpose
2. **Create a branch** following the naming convention
3. **Create a top-level directory** for the recipe (e.g. `my-recipe/`)
4. **Add a `README.md`** in the recipe directory that describes:
   - What the recipe does
   - How to run it (commands, env vars)
   - Dependencies and how to install them
5. **Add the recipe to the table** in [`docs/README.md`](../README.md)
6. **Open a PR** following the workflow above
