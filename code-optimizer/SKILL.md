---
name: code-optimizer
description: Tidies, cleans, and optimizes code by removing dead code, unused imports, and reducing unnecessary repetition. Use to maintain high code quality and adhere to DRY principles.
---

# Code Optimizer Skill

This skill provides a comprehensive workflow for tidying, cleaning, and optimizing the codebase. It goes beyond simple formatting to ensure the code is lean, efficient, and maintainable.

## Workflow

### 1. Scope Selection
Before starting the cleanup, the user must select the scope of the operation:
- **Kotlin / Jetpack Compose**: Focuses on Kotlin source files and Compose components.
- **Rust**: Focuses on Rust source files.
- **All**: Applies cleanup to the entire codebase.

### 2. Code Tidying & Formatting
Ensure the codebase follows the project's formatting standards based on the selected scope.
- **Kotlin and Gradle KTS**:
  ```bash
  ./gradlew spotlessApply
  ```
- **Rust**:
  ```bash
  cd rust && cargo fmt
  ```

### 3. Dead Code Removal
Identify and remove code that is no longer reachable or used within the selected scope.
- **Unused Imports/Variables**: Scan for and remove unused imports, local variables, and private members.
- **Unreachable Logic**: Remove blocks of code that can never be executed (e.g., code after a `return` or within `if (false)`).

### 3. DRY (Don't Repeat Yourself) & Boilerplate Reduction
Minimize unnecessary code repetition and verbosity by identifying patterns that can be abstracted or simplified.
- **Logic Consolidation**: If a specific logic or calculation is repeated in multiple places, extract it into a helper function or a shared utility.
- **Boilerplate Reduction**: Leverage language-specific features to reduce verbosity (e.g., Kotlin's `apply`/`let`, extension functions, or data classes). In Compose, use `CompositionLocal` or shared modifiers to avoid excessive parameter drilling.
- **Component Reusability**: For UI code, identify repeated patterns and consolidate them into reusable components.

### 4. Structural Cleaning
- **Comment Cleanup**: Remove "TODO" comments that have been addressed or commented-out code blocks that are no longer needed.
- **Formatting Consistency**: Ensure consistent naming conventions and vertical spacing across the modified files.

## Guidelines
- **Run before commits**: Always execute this workflow before submitting a PR or requesting a commit.
- **Incremental Changes**: When removing dead code or refactoring for DRY, ensure the changes are verified by existing tests.
- **Tooling**: Leverage built-in IDE inspections or linting tools (e.g., `detekt`, `clippy`) when available to assist in identifying cleanup candidates.
