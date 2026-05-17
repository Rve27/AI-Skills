# AI-Skills

A collection of specialized expert skills for the Gemini CLI, designed to automate and standardize common software engineering tasks.

## 🚀 Overview
AI-Skills is a repository of reusable skills that extend the capabilities of the Gemini CLI. These skills provide structured workflows, expert procedural guidance, and standard templates to help developers maintain high engineering standards and improve productivity within their local development environments.

By leveraging these skills, developers can automate repetitive tasks like writing commit messages, maintaining documentation, and optimizing code, ensuring consistency and quality across their projects.

## ✨ Key Features
- **Git Commit Generation**: Automatically generates descriptive, Conventional Commits-compliant messages based on git diffs.
- **README Maintenance**: Provides a structured workflow for keeping project documentation synchronized with the evolving codebase using enterprise-grade standards.
- **Code Optimization**: Tidies, cleans, and optimizes code by removing dead code, improving Compose stability, and reducing unnecessary repetition.
- **Standardized Templates**: Includes reference templates and specialized guidance for modern development patterns.

## 🛠️ Tech Stack
- **Platform**: [Gemini CLI](https://github.com/google/gemini-cli)
- **Documentation**: Markdown (with YAML front matter)
- **Version Control**: Git

## 📂 Project Structure
```text
AI-Skills/
├── code-optimizer/             # Code formatting, cleaning, and optimization skill
├── commit/                     # Git commit message generation skill
├── optimize-compose-stability/ # Jetpack Compose performance optimization skill
└── readme-updater/             # README maintenance and synchronization skill
    └── references/             # Enterprise-grade documentation templates
```

## ⚙️ Getting Started

### Prerequisites
- [Gemini CLI](https://github.com/google/gemini-cli) installed and configured.

### Installation & Activation
1. Clone the repository to your local machine:
   ```bash
   git clone https://github.com/Rve27/AI-Skills.git
   ```
2. Navigate to the project directory:
   ```bash
   cd AI-Skills
   ```
3. Activate a skill using the Gemini CLI:
   ```bash
   # Example: Activate the commit skill
   gemini activate-skill ./commit/SKILL.md
   ```

## 🏗️ Architecture
Each skill in this repository is designed as a modular unit following the Gemini CLI skill specification. This includes:
- **SKILL.md**: The entry point containing metadata, detailed instructions, and a specific workflow (Research -> Strategy -> Execution).
- **Expert Guidance**: Specialized procedural knowledge embedded within the skill to handle complex tasks.
- **Reference Assets**: Supporting documents and templates located in `references/` directories to ensure output consistency.

