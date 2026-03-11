# GitHub Copilot Instructions

## Project Overview

<!-- Describe the purpose of this project, its main goals, and target audience. -->
<!-- Example: This is a REST API service for managing user accounts and authentication. -->

## Technology Stack

<!-- List the primary technologies, frameworks, and languages used in this project. -->
<!-- Example:
- **Language**: Python 3.11+
- **Framework**: FastAPI
- **Database**: PostgreSQL with SQLAlchemy ORM
- **Testing**: pytest
- **Containerization**: Docker + Docker Compose
-->

## Coding Standards

### General

- Write clear, readable, and self-documenting code. Prefer descriptive variable and function names over comments.
- Follow the principle of least surprise: code should behave as a reader would expect.
- Keep functions and methods small and focused on a single responsibility.
- Avoid magic numbers and strings; use named constants instead.

### Language-Specific

<!-- Add language-specific guidelines below. Remove sections that don't apply. -->

#### Python
- Follow [PEP 8](https://peps.python.org/pep-0008/) style guidelines.
- Use type hints for all function signatures.
- Use `dataclasses` or `pydantic` models for structured data.
- Prefer f-strings for string formatting.

#### JavaScript / TypeScript
- Follow the existing ESLint and Prettier configuration.
- Use TypeScript strict mode; avoid `any` types.
- Prefer `const` over `let`; avoid `var`.
- Use async/await over raw Promises or callbacks.

#### Java
- Follow standard Java naming conventions (camelCase for methods/variables, PascalCase for classes).
- Use `Optional` instead of returning `null`.
- Prefer immutable objects where possible.

## Project Structure

<!-- Describe the directory layout and where key files live. -->
<!-- Example:
```
src/
  api/        # Route handlers and endpoint definitions
  models/     # Data models and schemas
  services/   # Business logic
  utils/      # Shared utility functions
tests/
  unit/       # Unit tests
  integration/# Integration tests
```
-->

## Testing

- Write tests for all new features and bug fixes.
- Aim for high coverage on business logic; avoid testing implementation details.
- Use descriptive test names that explain the scenario and expected outcome.
- Separate unit tests from integration tests.
- Mock external dependencies (databases, APIs, file system) in unit tests.

## Error Handling

- Always handle errors explicitly; never swallow exceptions silently.
- Log errors with enough context to diagnose the issue (include relevant IDs, inputs, and stack traces).
- Return meaningful error messages to callers; avoid exposing internal implementation details to end users.
- Use structured logging where possible.

## Security

- Never commit secrets, API keys, tokens, or credentials to the repository.
- Use environment variables or a secrets manager for sensitive configuration.
- Validate and sanitize all external inputs (user input, API responses, file contents).
- Follow the principle of least privilege: request only the permissions that are needed.
- Keep dependencies up to date and audit them regularly for known vulnerabilities.

## Documentation

- Keep the `README.md` up to date with setup instructions, usage examples, and any relevant context.
- Document public APIs, functions, and classes with docstrings or JSDoc comments.
- Update `CHANGELOG.md` (if present) when making notable changes.

## Git Workflow

### Commit Messages

Follow the [Conventional Commits](https://www.conventionalcommits.org/) specification:

```
<type>(<scope>): <short summary>

[optional body]

[optional footer(s)]
```

Types: `feat`, `fix`, `docs`, `style`, `refactor`, `test`, `chore`, `perf`, `ci`

Examples:
- `feat(auth): add OAuth2 login support`
- `fix(api): handle null response from upstream service`
- `docs(readme): update local development setup steps`

### Branch Naming

- `feat/<short-description>` for new features
- `fix/<short-description>` for bug fixes
- `chore/<short-description>` for maintenance tasks
- `docs/<short-description>` for documentation-only changes

## Pull Request Guidelines

- Keep PRs small and focused on a single change.
- Write a clear description explaining the *what* and *why* of the change.
- Link to the related issue(s) using `Closes #<issue-number>`.
- Ensure all CI checks pass before requesting a review.
- Respond to review comments promptly and resolve conversations once addressed.

## Dependencies

- Prefer well-maintained, widely-adopted libraries over custom implementations.
- Pin dependency versions in production to ensure reproducible builds.
- Document why a dependency was added if it is not immediately obvious.
- Remove unused dependencies.

## Performance

- Avoid premature optimization; profile before optimizing.
- Be mindful of N+1 query problems when working with databases.
- Cache expensive computations or repeated network calls where appropriate.
- Use pagination for endpoints or queries that can return large data sets.
