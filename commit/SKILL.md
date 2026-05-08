---
name: commit
description: Generates descriptive git commit messages following the Conventional Commits standard. Use when the user wants to commit changes or needs help writing a commit message based on a git diff.
---

# Git Commit Message Generation

Follow these rules to generate a commit message based on the provided `git diff`.

## Rules

1. **Format**:
   `<type>(<scope>): <subject>`
   
   `<body>`

   `<footer>`

2. **Allowed Types**:
   - `feat`: New features
   - `fix`: Bug fixes
   - `docs`: Documentation changes
   - `style`: Formatting (white-space, semi-colons, etc)
   - `refactor`: Code changes that neither fix a bug nor add a feature
   - `perf`: Performance improvements
   - `test`: Adding/correcting tests
   - `build`: Changes that affect the build system or external dependencies
   - `ci`: Changes to CI configuration files and scripts
   - `chore`: Other changes that don't modify src or test files
   - `revert`: Reverts a previous commit

3. **Scope**: Brief and optional (e.g., `ui`, `api`, `config`, `deps`). Use nouns.
4. **Subject**:
   - Use imperative mood ("add", not "added").
   - Max 50 characters.
   - Do not capitalize the first letter.
   - No period at the end.
5. **Body**:
   - Optional. Explain "why" and "what", not "how".
   - Wrap at 72 characters.
6. **Footer**:
   - Optional. Use for referencing issues (e.g., `Fixes #123`) or for `BREAKING CHANGE: <description>`.

## Workflow

1. Analyze the provided `git diff`.
2. Determine the appropriate type and scope. If multiple types apply, prioritize `feat` or `fix`.
3. Write a concise subject.
4. If the changes are complex or introduce breaking changes, provide a body and footer.
5. Output ONLY the commit message text. No markdown blocks, no extra commentary.
