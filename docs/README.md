# wandb-recipes Documentation

This is the source of truth for how we work in this repository. Keep it in sync with the code — when behavior changes, update the relevant doc in the same PR.

## Sections

### Contributing
- [Contribution Guide](./contributing/README.md) — Workflow: Issue → Branch → PR, commit conventions, dependency management
- [Code Style](./contributing/code-style.md) — Python conventions for recipes

## Recipes

Each top-level directory is an independent recipe / example:

| Recipe | Purpose |
|--------|---------|
| [`stop-multiple-runs/`](../stop-multiple-runs/) | Detect and stop duplicate concurrent W&B runs |
| [`graphql/`](../graphql/) | W&B public API GraphQL examples |

When adding a new recipe, give it its own top-level directory with a `README.md` describing what it does and how to run it.

## Documentation Principles

1. **`docs/` is the source of truth.** Behavioral rules, workflows, and conventions live here — not scattered across recipe READMEs.
2. **Update docs alongside code.** Any PR that changes how something works updates the relevant doc in the same commit set.
3. **Recipe READMEs describe the recipe.** Cross-cutting rules (git workflow, code style) belong in `docs/`, not duplicated per recipe.
4. **Be specific.** Include the actual command, the actual file path, the actual error message.
