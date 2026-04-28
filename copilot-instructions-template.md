# Copilot Instructions

## Summary
<!-- Brief 2-3 sentence description of what this project does -->

## Terminology
<!-- List domain-specific terms with explanations -->
<!-- Example:
- **Term1** - Definition
- **Term2** - Definition
-->

## Architecture
<!-- Short summary of the architecture with "why" behind decisions -->
<!-- Reference important files -->
<!--
Why: [Explain architectural decisions]

Key files:
- `path/to/file.py` - Description
- `path/to/config.yaml` - Description
-->

## Development Environment

### Package Management
<!-- Add your package manager instructions here -->
<!-- Example for conda:
- Create environment: `conda env create -f environment.yml`
- Activate: `conda activate project-name`
- Add packages: `conda install package` or `pip install package`
- Update environment.yml when adding dependencies
-->

### Shell Scripts
- Scripts must be run with the correct conda environment **already active** in the
  caller's shell. Never source `conda.sh` or call `conda activate` inside a script
  that takes positional arguments — bash's `$@` leaks into conda's shell function
  and causes `ArgumentError`.
- Add a guard at the top of every shell script to fail fast if the wrong env is active:
  ```bash
  if [[ "$(basename "${CONDA_PREFIX:-}")" != "your-env-name" ]]; then
    echo "ERROR: activate the your-env-name conda environment first." >&2
    exit 1
  fi
  ```
- Never hardcode absolute Python interpreter paths (e.g. `/data/.../bin/python`) —
  use plain `python` after the env is active.

### Code Quality Tools
<!-- Add your project-specific tools -->
<!-- Example:
- **Type checking**: `mypy .` or `pyright`
- **Formatting**: `black .` or `ruff format .`
- **Linting**: `ruff check . --fix` or `flake8`
- **Testing**: `pytest`
-->

### Line Length and Formatting
- Maximum 88 characters per line (or adjust to your preference)
- Use parentheses for long strings:
  ```python
  message = (
      "This is a very long string that needs "
      "to be split across multiple lines"
  )
  ```
- Multi-line function calls with proper indentation
- Split long imports across multiple lines

## Task Planning and Problem-Solving

### Before Starting Any Task
Always complete these steps in order:

1. **Check for existing solutions**: Search `docs/error.md` for similar issues already
   solved
2. **State assumptions explicitly**: Before implementing, surface what you're assuming.
   If uncertain, ask rather than guessing.
3. **Surface tradeoffs**: If multiple valid interpretations or approaches exist, present
   them — don't pick silently.
4. **Provide a full plan** of your changes before writing any code
5. **List behaviors that will change** and components affected
6. **List test cases to add** or existing tests to update
7. **Search for reusable code**: Before adding any code, always check if you can reuse
   or reconfigure existing code

If something is unclear, stop. Name what's confusing. Ask before proceeding.

### Goal-Driven Execution
Transform vague tasks into verifiable goals before starting:

- "Add validation" → "Write tests for invalid inputs, then make them pass"
- "Fix the bug" → "Write a test that reproduces it, then make it pass"
- "Refactor X" → "Ensure tests pass before and after"

For multi-step tasks, state a brief plan:
```
1. [Step] → verify: [check]
2. [Step] → verify: [check]
3. [Step] → verify: [check]
```

Strong success criteria let you loop independently. Weak criteria ("make it work")
require constant clarification.

### DRY Principle (Critical)
Always follow the DRY (Don't Repeat Yourself) principle:

- **Before creating any new function**: Search the entire codebase for similar
  functionality
- **Before duplicating logic**: Extract common code into a reusable helper function
  with clear parameters
- **Prefer parameterization**: Add optional parameters to existing functions rather
  than creating near-duplicate functions
- **If you copy-paste code**: Stop immediately, refactor into a shared function first,
  then use it in both places

### Code Reusability Workflow
1. **Search first**: Use grep/semantic search to find functions with similar names or
   purposes
2. **Evaluate extension**: Can the existing function be extended with a parameter
   instead of creating a new one?
3. **Extract common logic**: If >3 lines are duplicated, extract into a helper function

### Build Iteratively
- Start with minimal functionality and verify it works before adding complexity
- Test frequently with realistic inputs and validate outputs
- Create testing environments for components that are difficult to validate directly
- Push implementation details to the edges; keep core logic clean

## Coding Guidelines

### Simplicity and Readability (Philosophy)
- **Less Code = Less Debt**: Minimize code footprint
- **Simplicity over complexity**: When choosing between simple and complex solutions,
  always choose the simple one
- **Nothing speculative**: No features beyond what was asked. No abstractions for
  single-use code. No "flexibility" or "configurability" that wasn't requested.
- **Self-check**: Ask yourself — "Would a senior engineer say this is overcomplicated?"
  If yes, simplify. If you write 200 lines and it could be 50, rewrite it.
- **Early returns**: Use to avoid nested conditions
- Always prefer clear, straightforward code over clever or complex solutions
- Avoid nested conditionals deeper than 2 levels — extract into named helper functions
  instead
- Keep functions under 50 lines — if longer, split into smaller functions with
  descriptive names
- Keep functions focused and small — each should do one thing well

### Surgical Changes
**Touch only what you must. Clean up only your own mess.**

When editing existing code:
- Don't "improve" adjacent code, comments, or formatting
- Don't refactor things that aren't broken
- Match existing style, even if you'd do it differently
- If you notice unrelated dead code, mention it — don't delete it

When your changes create orphans:
- Remove imports/variables/functions that **your** changes made unused
- Don't remove pre-existing dead code unless explicitly asked

The test: every changed line should trace directly to the user's request.

### Naming Conventions
- **Functions/variables**: `snake_case`
- **Classes**: `PascalCase`
- **Constants**: `UPPER_SNAKE_CASE`
- **Handlers**: Prefix with `handle_` (e.g., `handle_user_input`)
- Always use descriptive names — prefer `user_input_validator` over `uiv` or
  `validator`

### DRY and Code Reuse (Mandatory)
- Always follow the DRY principle — never duplicate code
- Before writing any new function, search for similar functions in the codebase
- Before duplicating logic across files, extract common code into appropriate shared
  module
- Always extract repeated code blocks (>3 lines) into reusable functions
- **Constants over functions**: Use constants where possible to reduce overhead
- Please use simple human readable code instead of clever code — if a simple solution
  works, prefer it over a complex one, even if it means writing more lines. The goal
  is to minimize cognitive load for future readers, not to minimize line count.

### Type Annotations and Documentation (Required)
- **Type hints required** for all function signatures
- Use explicit None checks for Optional types
- Add type narrowing for strings when needed
- Always include docstrings for classes and non-trivial functions:
  ```python
  def function_name(param: Type) -> ReturnType:
      """Brief description.

      Args:
          param: Description of parameter

      Returns:
          Description of return value
      """
  ```
- Public APIs must have docstrings
- Avoid redundant comments that just restate the code — only comment non-obvious logic
- Mark issues in existing code with `TODO:` prefix

### Code Style
- Use **f-strings** for formatting (not % or .format())
- Prefer **functional, immutable approaches** when not verbose
- Follow **existing patterns** in the codebase exactly
- **Minimal changes**: Only modify code related to the task at hand
- **Function ordering**: Define composing functions before their components

### File and Folder Structure
- **Source code**: Always place implementation code in appropriate directories
  (e.g., `src/`)
- **Test and scratch code**: Always place test files and experimental code in
  designated test directories — keep the root directory clean
- **Analysis and summary scripts**: Extract result analysis, statistics, and reporting
  code into standalone Python scripts (e.g., `summarize_*.py`). Never embed multi-line
  Python inside shell heredocs — call the separate script instead.
- **Generated documentation**: Always create in `docs/` folder (create if doesn't
  exist)
  - Naming format: `docs/{feature}.md` (e.g., `docs/api-design.md`)
  - Update `README.md` with brief usage examples; place detailed explanations in
    `docs/`
- **Configuration**: Always use config files for configurable parameters — never
  hardcode values that might change
- **File organization**: Balance with simplicity — use an appropriate number of files
  for the project scale

### Testing Requirements
- **New features require tests**
- **Bug fixes require regression tests**
- Test edge cases and error conditions
- Test thoroughly before claiming completion
<!-- Add your testing framework: pytest, unittest, etc. -->

## Documentation Standards

### Error Tracking
Always document errors in `docs/error.md` (create if doesn't exist) with this exact
structure:
```markdown
### [Error Category: Specific Error Name]
**Date Encountered**: YYYY-MM-DD

**What failed**:
- Exact error message or observable symptom
- Context: when it happens

**Why it failed**:
- Root cause analysis
- Related configuration or assumptions that broke

**How we fixed it**:
- Code changes with file references
- Configuration adjustments
- Testing steps to verify fix

**Prevention**:
- How to avoid this in future
```

### Feature Documentation
- **README.md**: Brief usage examples and high-level overview
- **docs/{feature}.md**: Detailed explanations, architecture decisions, examples
- **Inline comments**: Only for non-obvious logic

### Configuration Management
- Always use config files for parameters — never hardcode these values
- Place shared constants in a dedicated constants module or config, not scattered
  across files

## Error Handling and Resolution

### Before Fixing Any Issue
1. **Check error.md**: Search `docs/error.md` for the error message or similar
   symptoms
2. **Verify not already fixed**: Ensure the issue hasn't been addressed in recent
   commits
3. **Document if novel**: If this is a new error, prepare to document it in
   `docs/error.md`

### Common Type Errors
- Add explicit None checks for Optional types
- Use type narrowing for strings
- Verify function signatures match
- Get full line context when debugging
- Match existing patterns in codebase

## Git Workflow

### Branch Strategy
- **Never commit directly to `main`** — always use feature branches
- Branch naming: `fix/auth-timeout`, `feat/api-pagination`, `chore/ruff-fixes`
- Keep one logical change per branch for easier review and rollback

### Commit Practices
- Make **atomic commits** (one logical change per commit)
- Use conventional commit style: `type(scope): short description`
  - Examples: `feat(eval): add new metric`, `fix(cli): handle missing API key`
- Link issues in commits/PRs: `Fixes #123` for auto-linking
- Check `git status` before commits

### Pull Request Workflow
1. Create or reference an issue first
2. `git checkout -b feat/issue-123-description`
3. Commit in small, logical increments
4. Open **draft PR early** for visibility
5. Convert to ready when functionally complete and tests pass
6. Create detailed PR message:
   - Focus on high-level problem and solution
   - Explain "why", not just "what"
   - Don't go into code specifics unless it adds clarity
7. Merge after reviews and checks pass

## Automatic Verification

After adding or changing code, always verify by running:
<!-- Add your project-specific verification commands -->
<!-- Example:
1. `black .` - Format code
2. `ruff check . --fix` - Fix linting issues
3. `mypy .` - Type check
4. `pytest` - Run all tests
-->

Complete the task only after all checks pass. If any check fails, fix the issue before
claiming completion.

## General Principles

When working on this codebase, always follow these principles:

1. **Think before coding**: State assumptions, surface tradeoffs, and ask when
   uncertain — before writing a single line
2. **Plan before coding**: Provide a full plan, list behavior changes, and test cases
   before writing any code
3. **Define verifiable goals**: Transform tasks into checkable success criteria, not
   vague intentions
4. **DRY principle**: Before adding any function, search for existing functions that
   can be reused or extended
5. **Simplicity over complexity**: Choose simple solutions over complex ones; nothing
   speculative
6. **Surgical changes**: Touch only what the task requires; don't improve adjacent code
7. **Build iteratively**: Start minimal, verify, then extend
8. **Test thoroughly**: Edge cases, errors, and realistic inputs
9. **Document rigorously**: Every significant change should be documented
10. **Follow existing patterns**: Match the codebase style exactly
11. **Verify before completion**: Run all automatic verification steps

## Model-Specific Instructions

- Always focus on simplicity and precision, not comprehensiveness
- When debugging, change **one thing at a time** — avoid rewriting entire functions
- When writing tests, focus on the happy path and only the most critical edge cases
- Before adding a new helper function, always verify a similar function doesn't already
  exist
- Avoid over-engineering — if a simple solution works, prefer it over a complex one
