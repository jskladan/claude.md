---
description: "Run code formatting tools"
args: "[all|file_pattern]"
---

# Format Code

Run comprehensive code formatting on the specified files or changed files.

## Usage
- `/pyformat` - Format only changed/staged files (git diff)
- `/pyformat all` - Format all Python files in project
- `/pyformat src/` - Format files in src/ directory  
- `/pyformat file.py` - Format specific file

## Actions Performed

### Python Files
```bash
# Get changed files if no arguments
if [ -z "$ARGUMENTS" ]; then
  FILES=$(git diff --name-only --diff-filter=AM HEAD | grep '\.py$')
  STAGED_FILES=$(git diff --name-only --cached --diff-filter=AM | grep '\.py$')
  ALL_CHANGED="$FILES $STAGED_FILES"
elif [ "$ARGUMENTS" = "all" ]; then
  ALL_CHANGED=$(find . -name "*.py" -not -path "./.venv/*" -not -path "./venv/*")
else
  ALL_CHANGED="$ARGUMENTS"
fi

# Format with black
black $ALL_CHANGED

# Sort imports
isort $ALL_CHANGED

# Optional: Run additional linters
# flake8 $ALL_CHANGED
# mypy $ALL_CHANGED
```

## Default Behavior
Runs only on files that are modified or staged in git, helping maintain clean commits without reformatting the entire codebase unnecessarily.