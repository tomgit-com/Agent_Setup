# AGENTS.md

## Build/Lint/Test Commands

This repository contains shell scripts and Python code with no formal test framework.

### Bash Scripts
- **ShellCheck linting:** `shellcheck <script_name>`
- **Syntax validation:** `bash -n <script_name>`
- **Execution:** Check individual script usage below

### Python Scripts
- **Syntax validation:** `python3 -m py_compile <script_name>`
- **Execution:** `python3 <script_name>`

### All Scripts
- **Syntax validation (all bash scripts):** `for f in *.sh; do bash -n "$f"; done`

No formal test commands exist. Run scripts directly after review.

## Code Style Guidelines

### Bash Coding Standards
- Follow POSIX-compliant syntax where possible
- Use lowercase function names with underscores: `get_physical_ram_gb()`
- Use `snake_case` for variable names
- Quote variables: `"$variable"` to prevent word splitting
- Use `[]` for tests instead of `[[]]` for portability
- Prefer functions over complex one-liners for readability
- Include error handling with exit codes
- Use `local` for function-scoped variables
- comment out with `#` and single space after

### Shell Script Guidelines
- Scripts should be executable with `chmod +x`
- Include shebang at top: `#!/bin/bash`
- Add comments for complex logic or non-obvious calculations
- Prefer interactive prompts over command-line flags where applicable
- Use absolute paths in scripts for reliability
- Test changes in a VM or non-production environment first
- Follow the `set -euo pipefail` pattern for strict error handling
- Handle missing dependencies gracefully with informative error messages

### Python Coding Standards
- Follow PEP 8 style guidelines
- Use 4-space indentation
- Type hints for function signatures where applicable
- Use `snake_case` for functions and variables
- Capitalize constants: `SYSTEM_RAM_RESERVE = 16`
- Include docstrings for public functions
- Use try/except for file I/O errors
- Prefer f-strings for string formatting (Python 3.6+)

### General Guidelines
- Scripts should be executable with `chmod +x`
- Include shebang at top: `#!/bin/bash` or `#!/usr/bin/env python3`
- Add comments for complex logic or non-obvious calculations
- Prefer user prompts over command-line flags where interactive
- Always backup config files before modification
- Use absolute paths in scripts for reliability
- Test changes in a VM or non-production environment first

### Error Handling
- Bash: Check `$?` or use `set -euo pipefail` for strict error handling with pipefail
- Python: Catch `FileNotFoundError` for missing files
- Always validate user input before processing
- Exit with code 1 on errors, 0 on success

### Naming Conventions
- Files: `snake_case` with descriptive names
- Constants: `UPPER_SNAKE_CASE`
- Functions: `lowercase_with_underscores`
- Variables: lowercase with underscores (bash), lowercase (Python)
