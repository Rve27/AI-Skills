# AI-Skills

A collection of specialized expert skills for the Gemini CLI, designed to automate and standardize common software engineering tasks.

## 🚀 Overview
AI-Skills is a repository of reusable skills that extend the capabilities of the Gemini CLI. These skills provide structured workflows, expert procedural guidance, and standard templates to help developers maintain high engineering standards and improve productivity within their local development environments.

## ✨ Key Features
- **Git Commit Generation**: Automatically generates descriptive, Conventional Commits-compliant messages based on git diffs.
- **README Maintenance**: Provides a structured workflow for keeping project documentation synchronized with the evolving codebase.
- **Automated Formatting**: Streamlines code tidying for Kotlin, Gradle, and Rust using Spotless and Cargo FMT.
- **Standardized Templates**: Includes reference templates (e.g., for READMEs) to ensure consistency across projects.

## 🛠️ Tech Stack
- **Gemini CLI**: The core platform for executing these skills.
- **Markdown**: Skills are defined using Markdown with YAML front matter for metadata.
- **Git**: Integrated version control workflows.

## 📂 Project Structure
```text
AI-Skills/
├── commit/           # Git commit message generation skill
├── readme-updater/   # README maintenance and synchronization skill
└── spotless-clean/   # Code formatting and tidying skill
```

## ⚙️ Getting Started

### Prerequisites
- [Gemini CLI](https://github.com/google/gemini-cli) installed and configured.

### Installation
1. Clone the repository to your local machine.
   ```bash
   git clone https://github.com/Rve27/AI-Skills.git
   ```
2. Activate a skill using the Gemini CLI:
   ```bash
   # Example: Activate the commit skill
   gemini activate-skill ./commit/SKILL.md
   ```

## 🏗️ Architecture
Each skill in this repository follows a consistent structure:
- **SKILL.md**: Contains metadata, detailed instructions, and a workflow for the Gemini CLI to follow.
- **References/Templates**: Supporting documents and templates used by the skill to generate or update files.
