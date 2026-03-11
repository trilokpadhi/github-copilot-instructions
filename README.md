# github-copilot-instructions

A reusable template for `.github/copilot-instructions.md` that aligns GitHub Copilot's responses with the conventions and standards of your project.

## What is `copilot-instructions.md`?

GitHub Copilot reads `.github/copilot-instructions.md` at the root of a repository and uses it as persistent context for every conversation in that repo. This lets you teach Copilot about your:

- Technology stack and language preferences
- Coding standards and style guides
- Project structure and architecture patterns
- Testing, documentation, and security requirements
- Git workflow and PR guidelines

## Usage

1. Copy [`.github/copilot-instructions.md`](.github/copilot-instructions.md) into your project's `.github/` directory.
2. Fill in the `<!-- ... -->` placeholder sections with details specific to your project.
3. Remove any sections that don't apply.
4. Commit the file — Copilot will pick it up automatically.

## Template Sections

| Section | Purpose |
|---|---|
| **Project Overview** | High-level description of the project and its goals |
| **Technology Stack** | Languages, frameworks, databases, and tooling in use |
| **Coding Standards** | General and language-specific style rules |
| **Project Structure** | Directory layout and where key files live |
| **Testing** | Testing strategy, coverage expectations, and tooling |
| **Error Handling** | How to handle and log errors consistently |
| **Security** | Secrets management, input validation, and least-privilege principles |
| **Documentation** | Docstring and README conventions |
| **Git Workflow** | Commit message format (Conventional Commits) and branch naming |
| **Pull Request Guidelines** | PR size, description, and review expectations |
| **Dependencies** | How to evaluate, pin, and manage third-party libraries |
| **Performance** | Guidance on profiling, caching, and query optimization |

## Tips

- Keep the instructions concise — Copilot performs best when context is clear and focused.
- Update the file whenever your team adopts new conventions.
- Use this as a living document alongside your other project documentation.
