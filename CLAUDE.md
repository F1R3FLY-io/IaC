# Claude System Instructions
 
## Project Context
- This is a Python-based Infrastructure as Code (IaC) project for deploying web applications to Oracle Cloud Infrastructure (OCI).
- The project provides deployment automation for React/TypeScript applications built with Vite and pnpm.
- Uses Python scripts to manage OCI resources and deploy web applications.
- Supports generalized deployment patterns for modern web applications.
 
## Commands
- Setup: `uv sync` (automatically creates virtual environment and installs dependencies)
- Deploy: `uv run deploy.py` or `uv run scripts/deploy.py`
- Test: `uv run pytest` or `uv run pytest tests/`
- Lint: `uv run flake8 .` or `uv run pylint src/`
- Format: `uv run black .` and `uv run isort .`
- Type Check: `uv run mypy .`
- Quick script execution: `uvx script-name` for standalone scripts
- Use the `/quick-commit` slash command for git add/commit operations; use the `/recursive-push` command for git push operations. Do not run `git add`, `git commit`, or `git push` directly unless explicitly requested.
- `git mv` is permitted but requires user confirmation.
- Never discard user changes; avoid destructive git commands.
- DO NOT ever remove tests from linting or type checks.
- Run `uv run pytest && uv run flake8 .` to test code changes before proceeding to next task.
- DO NOT execute deployment scripts without explicit user permission.
 
## Code Style Preferences
- **Python**: Use Python 3.9+ with type hints for all functions and classes.
- **Imports**: Organize imports - standard library first, third-party next, local imports last.
- **Structure**: Use classes for OCI resource management, functions for utilities.
- **Naming**: snake_case for functions/variables, PascalCase for classes, UPPER_CASE for constants.
- **Error Handling**: Use proper exception handling with logging, avoid bare except clauses.
- **Configuration**: Use environment variables and config files for sensitive data.
- **Documentation**: Include docstrings for all classes and functions.
- Follow PEP 8 style guidelines with Black formatting.
- Use type hints consistently throughout the codebase.
- When adding new scripts or modules, include comprehensive unit tests using pytest.
- Use organized file structure: src/, scripts/, tests/, config/, docs/
- Use `pyproject.toml` for project configuration and dependency management with uv
 
## Common Tasks
- Create deployment scripts for React/Vite applications
- Manage OCI resources (compute instances, load balancers, storage)
- Handle environment-specific configurations
- Implement proper logging and error handling
- Use OCI Python SDK for resource management
- Test deployment scripts in isolated environments
- Use `uv add` to add new dependencies to pyproject.toml
- Use `uv run` for executing scripts with the project's virtual environment

## Best Practices
- Never hardcode credentials or sensitive information
- Use OCI configuration files and environment variables
- Implement proper resource cleanup and rollback mechanisms
- Include comprehensive error handling and logging
- Follow infrastructure as code principles
- Use pytest for testing deployment logic
- Implement idempotent deployment operations
- Work with the user to develop deployment strategies using a test-driven approach
- Leverage uv's fast dependency resolution and package management
- Use `uv lock` to ensure reproducible builds across environments

## Attributions

- Do not include any references to Claude co-authoring commits or code.
