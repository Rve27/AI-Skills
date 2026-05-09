---
name: readme-updater
description: Automates the maintenance and synchronization of enterprise-grade README.md files. Use this to ensure professional documentation that reflects the current tech stack, directory structure, build instructions, and community standards (Security, Contributing, Support).
---

# Readme Updater (Enterprise Grade)

## Overview
This skill provides a structured, professional workflow for keeping project `README.md` files up-to-date. It focuses on "Enterprise Grade" documentation which includes automated badges, deep technical insights, and standardized community sections.

## Workflow

### 1. Discovery & Inventory
Scan the workspace to identify all existing documentation and metadata:
- **Root README**: The primary entry point.
- **Support Docs**: Identify `CONTRIBUTING.md`, `SECURITY.md`, `CODE_OF_CONDUCT.md`, and `LICENSE`.
- **Module READMEs**: (e.g., `rust/README.md`, `app/README.md`) For specialized sub-system details.

### 2. Deep Codebase Analysis
Gather ground truth to populate the enterprise template:
- **Badges & CI**: Scan `.github/workflows/*.yml` to identify CI/CD status badges. Check `build.gradle.kts` or `package.json` for current version numbers.
- **Tech Stack**: Analyze dependency files (`libs.versions.toml`, `Cargo.toml`, `go.mod`) to list specific versions of key frameworks.
- **Project Structure**: Use `list_directory` to create an accurate tree-view of the architecture.
- **Getting Started**: Verify build commands by checking scripts and configuration files. Ensure prerequisites (JDK, Node, Rust versions) are explicitly stated.

### 3. Documentation Drafting (Enterprise Standards)
Follow the template in `references/readme-template.md` with these enhancements:
- **Table of Contents**: Always maintain an up-to-date TOC with internal anchor links.
- **Visuals & Badges**: Ensure badges use current repository paths and reflect real CI states.
- **Community Standards**: 
  - If `CONTRIBUTING.md` exists, link it prominently.
  - Populate the **Security** section with instructions to refer to `SECURITY.md`.
  - Provide a clear **Support** section with links to Issues, Discussions, or contact methods found in the project.
- **Architecture**: Move beyond simple descriptions. Briefly explain *why* certain patterns (e.g., Clean Architecture, MVVM) were chosen.

### 4. Implementation & Validation
- **Surgical Updates**: Use `replace` for targeted section updates to preserve manually added notes. Use `write_file` only for total README refreshes.
- **Link Validation**: Ensure all internal (anchors) and external (badges, docs) links are functional.
- **Formatting**: Ensure consistent use of Markdown emojis and horizontal rules for professional spacing.

## Guidelines for Different READMEs

### Root README.md
- **Professional Header**: Name, description, and high-signal badges.
- **Onboarding**: Focus on the fastest path from `git clone` to a running build.
- **Governance**: Include the Contributing, Security, and License sections.

### Technical/Module README.md
- **Deep Dive**: Focus on implementation details, performance considerations, and internal API usage.
- **Native/JNI**: Specifically document the bridge layer, memory management, and cross-compilation requirements.

## References
- [readme-template.md](references/readme-template.md): The authoritative enterprise-grade structure.
