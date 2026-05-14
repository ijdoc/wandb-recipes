# CLAUDE.md

Guidance for Claude Code (claude.ai/code) when working in this repository.

## Project Overview

wandb-recipes is a collection of independent recipes / examples for working with Weights & Biases. Each top-level directory is a self-contained recipe with its own dependencies and entry points.

**Documentation source of truth**: [`docs/`](./docs/). Always update the relevant doc in the same PR as the code change.

## Development Guidelines

All changes follow the [Contribution Guide](./docs/contributing/README.md) (Issue → Branch → PR). Key rules to always apply:

- **Always create an issue** before starting work — `gh issue create ...`
- **Branch naming**: `<type>/<issue#>-slug` (e.g. `fix/42-handle-empty-state`)
- **Stage explicitly**: never use `git add .`, `git add -A`, or `git commit -a` — stage specific files by name
- **Commit format**: Conventional Commits — `<type>(<scope>): <subject>`
- **Lock files**: when a dependency manifest changes (`pyproject.toml`, `Pipfile`), regenerate the lock file (`uv lock` or `pipenv lock`) and commit both files together
- **Update docs alongside code**: any behavioral change must update the relevant file under `docs/` in the same PR

See [`docs/contributing/README.md`](./docs/contributing/README.md) for the full workflow and [`docs/contributing/code-style.md`](./docs/contributing/code-style.md) for Python conventions.

## Repository Structure

- `docs/` — Source of truth for workflows, conventions, and contribution rules
- `<recipe>/` — Each top-level directory is a self-contained recipe (e.g. `stop-multiple-runs/`, `graphql/`)
- `.github/` — GitHub Actions workflows and PR/issue templates
