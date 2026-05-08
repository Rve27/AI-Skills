---
name: readme-updater
description: Automates the maintenance and synchronization of README.md files across a project. Use this when you need to update project documentation to reflect the current tech stack, directory structure, build instructions, or JNI/Native implementation details.
---

# Readme Updater

## Overview
This skill provides a structured workflow for keeping project `README.md` files up-to-date with the evolving codebase. It is particularly effective for multi-language projects (e.g., Kotlin/Android + Rust) where documentation needs to cover both high-level architecture and low-level technical details like JNI bridges.

## Workflow

### 1. Discovery
Scan the workspace to identify all existing `README.md` files.
- **Root README**: Usually provides the project overview, setup, and high-level architecture.
- **Module READMEs**: (e.g., `rust/README.md`, `app/README.md`) Provide specialized information for that specific module.

### 2. Codebase Analysis
Before updating, gather the latest "ground truth" from the code:
- **Build Configuration**: Read `build.gradle.kts`, `settings.gradle.kts`, `Cargo.toml`, and `libs.versions.toml` to identify versions, dependencies, and build requirements.
- **Project Structure**: Use `list_directory` to map the current layout.
- **Technical Details**: For JNI/Native projects, check `lib.rs` and `utils/` classes to understand the bridge implementation.
- **CI/CD**: Check `.github/workflows` for deployment or testing procedures.

### 3. Documentation Drafting
Apply the following standards when drafting updates:
- **Consistency**: Maintain a professional, technical tone. Use consistent terminology (e.g., "RvSystem Monitor" instead of "System Monitor").
- **Structure**: Follow the template in `references/readme-template.md` if available.
- **Technical Accuracy**: Ensure build commands and prerequisites are correct and tested.
- **Visuals**: Include badges (build status, license) and ensure placeholders for screenshots are correctly referenced.

### 4. Implementation & Validation
- Update the files using surgical `replace` calls or `write_file` for complete rewrites.
- Validate that all internal links and relative paths within the READMEs are correct.

## Guidelines for Different READMEs

### Root README.md
- **Project Name & Description**: High-level value proposition.
- **Key Technologies**: List main frameworks and languages.
- **Getting Started**: Clear, step-by-step instructions for new developers.
- **Architecture**: Brief overview of the project structure and Clean Architecture principles.
- **Build Commands**: The most common Gradle/Cargo tasks.

### Rust/Native README.md
- **Native Implementation**: Explain the purpose of the Rust backend.
- **JNI Bridge**: How to compile and link the native library.
- **Prerequisites**: Specific tools like `cargo-ndk`, NDK versions.
- **Memory/Performance**: Notes on native efficiency and hardware parsing.

## References
- [readme-template.md](references/readme-template.md): Standard structure for README files.
