# Code Style Guide

Conventions for Python code in this repository.

## Variable Naming

- Use descriptive names: `run_ids`, not `r`
- Use `snake_case` for variables and functions: `user_id`, `run_state`
- Use meaningful names even for short-lived variables

## Type Hints

Type hints are required on all function signatures.

```python
def stop_duplicate_runs(project: str, entity: str) -> list[str]:
    ...
```

## Function Documentation

Use Google-style docstrings for all public functions and classes:

```python
def stop_duplicate_runs(project: str, entity: str) -> list[str]:
    """
    Stop concurrent W&B runs that duplicate the latest active run.

    Args:
        project: W&B project name
        entity: W&B entity (user or team)

    Returns:
        List of run IDs that were stopped.

    Raises:
        wandb.errors.CommError: If the W&B API is unreachable.
    """
```

## Code Organization

- Keep functions focused — single responsibility principle
- Extract complex logic into separate functions
- Group related functionality together

## Error Handling

Provide informative, specific error messages. Don't swallow exceptions silently.

```python
# Good
try:
    run.finish()
except wandb.errors.CommError as e:
    logger.error(f"Failed to finish run {run.id}: {e}")
    raise

# Bad
try:
    run.finish()
except:
    pass  # Silent failures hide bugs
```

## Logging

Prefer `logging` over `print` for anything beyond simple recipe demonstration scripts. When a recipe is meant to be read as an example, `print` is fine — but make the output meaningful, not noise.

```python
logger.info("Found %d duplicate runs to stop", len(duplicates))
```

## Recipe Structure

Each recipe directory should contain:

- A `README.md` describing what the recipe does and how to run it
- A dependency manifest (`pyproject.toml` + `uv.lock`, or `Pipfile` + `Pipfile.lock`)
- The recipe scripts themselves, named for what they do (`stop_runs.py`, not `main.py` unless there's only one entry point)
- A `.env.example` if env vars are required (never commit `.env`)
