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
<!-- Example:
Why: [Explain architectural decisions]

Key files:
- `path/to/file.py` - Description
- `path/to/config.yaml` - Description
-->

## Task Planning and Problem-Solving

### Before Starting Any Task
Always complete these steps in order:

1. **Provide a full plan** of your changes before writing any code
2. **List behaviors that will change** and components affected
3. **List test cases to add** or existing tests to update
4. **Check for existing solutions**: Search `docs/error.md` for similar issues already solved
5. **Search for reusable code**: Before adding any code, always check if you can reuse or reconfigure existing code to achieve the result

### DRY Principle (Critical)
Always follow the DRY (Don't Repeat Yourself) principle:

- **Before creating any new function**: Search the entire codebase for similar functionality
- **Before duplicating logic**: Extract common code into a reusable helper function with clear parameters
- **Prefer parameterization**: Add optional parameters to existing functions rather than creating near-duplicate functions
- **If you copy-paste code**: Stop immediately, refactor into a shared function first, then use it in both places

### Code Reusability Workflow
1. **Search first**: Use grep/semantic search to find functions with similar names or purposes
2. **Evaluate extension**: Can the existing function be extended with a parameter instead of creating a new one?
3. **Extract common logic**: If >3 lines are duplicated, extract into a helper function

### Automatic Verification for Agent Mode
After adding or changing code, always verify that everything still works by running *each* of the following checks:

<!-- Add your project-specific verification commands here -->
<!-- Example:
1. `npm run lint` to run the linter
2. `npm run test` to run tests
3. `npm run build` to verify build succeeds
-->

Complete the task only after all checks pass. If any check fails, fix the issue before claiming completion.

### Model-Specific Instructions
- Always focus on simplicity and precision, not comprehensiveness
- When debugging, change one thing at a time — avoid rewriting entire functions
- When writing tests, focus on the happy path and only the most critical edge cases
- Before adding a new helper function, always verify a similar function doesn't already exist
- Avoid over-engineering — if a simple solution works, prefer it over a complex one

## Coding Guidelines

### Simplicity and Readability
- Always prefer clear, straightforward code over clever or complex solutions
- Avoid nested conditionals deeper than 2 levels — extract into named helper functions instead
- Keep functions under 50 lines — if longer, split into smaller functions with descriptive names
- Always use descriptive variable names — prefer `user_input_validator` over `uiv` or `validator`

### DRY and Code Reuse (Mandatory)
- Always follow the DRY principle — never duplicate code
- Before writing any new function, search for similar functions in the codebase
- Before duplicating logic across files, extract common code into appropriate shared module
- Always extract repeated code blocks (>3 lines) into reusable functions

### Type Annotations and Documentation
- Always use type hints for all function signatures
- Always include docstrings for classes and non-trivial functions with format:
```python
  def function_name(param: Type) -> ReturnType:
      """Brief description.
      
      Args:
          param: Description of parameter
          
      Returns:
          Description of return value
      """
```
- Avoid redundant comments that just restate the code — only comment non-obvious logic

### File and Folder Structure
- **Source code**: Always place implementation code in appropriate directories (e.g., `src/`)
- **Test and scratch code**: Always place test files and experimental code in designated test directories
  - Keep root directory clean of temporary or exploratory scripts
- **Generated documentation**: Always create in `docs/` folder (create if doesn't exist)
  - Naming format: `docs/{feature}.md` (e.g., `docs/api-design.md`, `docs/deployment.md`)
  - Update `README.md` with brief usage examples, place detailed explanations in `docs/`
- **Configuration**: Always use config files for configurable parameters — never hardcode values that might change

### Documentation Standards
- **Error tracking**: Always document errors in `docs/error.md` (create if doesn't exist) with this exact structure:
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
- **Feature documentation**: Always update `README.md` with brief usage examples AND create detailed docs in `docs/{feature}.md`
- **Inline comments**: Only use for non-obvious logic. Avoid comments that restate code

### Configuration Management
- **Config file**: Always use config files for parameters — never hardcode these values
- **Shared constants**: Place shared constants in a dedicated constants module or config, not scattered across files

## Error Handling and Documentation

### Before Fixing Any Issue
1. **Check error.md**: Search `docs/error.md` for the error message or similar symptoms
2. **Verify not already fixed**: Ensure the issue hasn't been addressed in recent commits
3. **Document if novel**: If this is a new error, prepare to document it in `docs/error.md`

### Error Documentation Template
When documenting errors in `docs/error.md`, use this structure:
```markdown
### [Error Category: Specific Error Name]
**Date Encountered**: YYYY-MM-DD

**What failed**:
- Exact error message or observable symptom
- Context: when does it happen

**Why it failed**:
- Root cause analysis
- Related configuration or assumptions that broke

**How we fixed it**:
- Code changes with file references
- Configuration adjustments
- Testing steps to verify fix

**Prevention**:
- How to avoid this in future (if applicable)
```

## General Guidelines

When working on this codebase, always follow these principles:

1. **Plan before coding**: Provide a full plan, list behavior changes, and list test cases before writing any code
2. **DRY principle**: Before adding any function, search for existing functions that can be reused or extended
3. **Simplicity over complexity**: When choosing between simple and complex solutions, always choose the simple one
4. **Document rigorously**: Every significant change should be documented appropriately
5. **Verify before completion**: Always run automatic verification steps before claiming task completion
