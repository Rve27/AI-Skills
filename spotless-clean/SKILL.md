---
name: spotless-clean
description: Cleans and tidies up Kotlin, Gradle KTS, and Rust code using Spotless and Cargo FMT. Use when code formatting needs to be enforced or before committing changes.
---

# Spotless Clean

This skill provides a streamlined workflow for ensuring the codebase follows the project's formatting standards.

## Workflow

1. **Kotlin and Gradle KTS**: Run Spotless to apply formatting rules.
   ```bash
   ./gradlew spotlessApply
   ```

2. **Rust**: Run Cargo FMT to format Rust source files.
   ```bash
   cd rust && cargo fmt
   ```

## Guidelines
- Always run these commands before submitting a PR or asking for a commit.
- If `./gradlew spotlessApply` fails, check for syntax errors in your Kotlin files.
- Ensure the Rust toolchain is installed and `rustfmt` is available for Cargo FMT.
