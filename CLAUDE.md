# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Purpose

This is a **meta-repository for project ideas and planning**. It contains no application code - only GitHub Issues for potential projects. Each issue should eventually get its own dedicated repository when work begins.

**Important**: Pull requests to this repo should be rare. Think twice before modifying anything here.

## Build System

This project uses [`just`](https://github.com/casey/just) as its task runner.

### Common Commands

```bash
just list              # List all available recipes
just compliance_check  # Run Chicks' repo compliance checks
just clean_readme      # Generate a clean README from template
```

### Git Workflow Commands

```bash
just branch <name>     # Create new branch with timestamp prefix (format: $USER/YYYY-MM-DD-<name>)
just pr                # Create PR with last commit message as title
just prweb             # Open current PR in browser
just merge             # Merge PR, delete branch, sync back to main
just sync              # Return to main branch and pull latest
```

The workflow expects:

- Main branch is `main`
- Branch naming: `$USER/YYYY-MM-DD-description`
- PR body auto-generated from last commit message
- After PR creation, watches checks if `.github/workflows` exists

## Repository Standards

The compliance check (`just compliance_check`) enforces these standards:

- `README.md`, `LICENSE`, `.gitignore`, `.gitattributes`, `.editorconfig`
- `.github/CODE_OF_CONDUCT.md`, `.github/CONTRIBUTING.md`, `.github/SECURITY.md`
- `.github/pull_request_template.md`, `.github/ISSUE_TEMPLATE/`
- `.github/CODEOWNERS`
- `justfile` (this build system itself)
- GitHub repo description (>16 chars)

## Language Preferences for New Projects

When projects spin off from issues here, preferred languages are:

**Definitely acceptable**: Go, Rust, Perl, Bash

**Possibly acceptable**: Python, C/C++, Lua, JavaScript

**Strongly discouraged**: PHP, Java, BASIC/VB, C#, Pascal, Matlab

## Justfile Architecture

The main `justfile` imports two modules:

- `.just/compliance.just` - Repository compliance checks with colorful output
- `.just/gh-process.just` - GitHub workflow automation (branch, PR, merge)

Color variables (e.g., `{{BLUE}}`, `{{GREEN}}`, `{{RED}}`, `{{NORMAL}}`) are used for terminal output formatting.
