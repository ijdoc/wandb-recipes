# wandb-recipes

A collection of self-contained recipes and solutions for [Weights & Biases](https://wandb.ai) users.

Each recipe lives in its own top-level directory and solves a single, focused problem — managing runs, querying the API, automating workflows, and so on. New recipes are typically shared as published [marimo](https://marimo.io) or [Colab](https://colab.research.google.com) notebooks; smaller utilities ship as plain Python scripts.

## Recipes

| Recipe | Description |
|--------|-------------|
| [`stop-multiple-runs/`](./stop-multiple-runs/) | Detect and stop duplicate concurrent W&B runs |
| [`graphql/`](./graphql/) | Examples of querying the W&B public GraphQL API (Colab) |

## Contributing

Contributions are welcome. The workflow is **Issue → Branch → PR** with Conventional Commits — see [`docs/contributing/README.md`](./docs/contributing/README.md) for the full guide, and [`docs/contributing/code-style.md`](./docs/contributing/code-style.md) for Python conventions.

When adding a new recipe:

1. Create a top-level directory named for what the recipe does
2. Include a `README.md` describing the problem, how to run it, and any required environment variables
3. Pin dependencies with a lock file (`uv.lock` preferred; `Pipfile.lock` accepted)
4. Add the recipe to the table above

## License

[Apache 2.0](./LICENSE)
