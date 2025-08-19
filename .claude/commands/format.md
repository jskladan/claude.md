---
description: "Run all available formatting tools"
args: "[all|file_pattern]"
---

# Unified Format

Run comprehensive formatting across all supported file types by orchestrating specialized formatting commands.

## Usage
- `/format` - Format only changed/staged files (git diff)
- `/format all` - Format all supported files in project
- `/format src/` - Format files in src/ directory  
- `/format file.py` - Format specific file

## Actions Performed

The unified format command delegates to specialized formatting commands based on file types found:

### File Type Detection and Delegation
```bash
# Determine which files need processing
if [ -z "$ARGUMENTS" ]; then
  # Get changed files for analysis
  CHANGED_FILES=$(git diff --name-only --diff-filter=AM HEAD)
  STAGED_FILES=$(git diff --name-only --cached --diff-filter=AM)
  ALL_FILES="$CHANGED_FILES $STAGED_FILES"
elif [ "$ARGUMENTS" = "all" ]; then
  # Scan entire project
  ALL_FILES=$(find . -type f \( -name "*.py" -o -name "*.html" -o -name "*.js" -o -name "*.jsx" -o -name "*.ts" -o -name "*.tsx" -o -name "*.css" -o -name "*.scss" -o -name "*.sass" \) | grep -v node_modules | grep -v .git | grep -v __pycache__)
else
  # Use provided argument
  ALL_FILES="$ARGUMENTS"
fi

# Check for Python files
PYTHON_FILES=$(echo "$ALL_FILES" | tr ' ' '\n' | grep '\.py$' | tr '\n' ' ')
if [ -n "$PYTHON_FILES" ]; then
  echo "🐍 Running Python formatting..."
  /pyformat $ARGUMENTS
fi

# Check for web files
WEB_FILES=$(echo "$ALL_FILES" | tr ' ' '\n' | grep -E '\.(html?|js|jsx|ts|tsx|css|scss|sass)$' | tr '\n' ' ')
if [ -n "$WEB_FILES" ]; then
  echo "🌐 Running web frontend formatting..."
  /webformat $ARGUMENTS
fi

# Summary
if [ -z "$PYTHON_FILES" ] && [ -z "$WEB_FILES" ]; then
  echo "ℹ️  No supported file types found for formatting"
else
  echo "✅ Formatting complete!"
fi
```

## Supported File Types

### Python Files (.py)
- Delegates to `/pyformat` command
- Uses `black` and `isort` for formatting
- Optional `flake8` and `mypy` for additional checks

### Web Frontend Files
- Delegates to `/webformat` command  
- **HTML**: `.html`, `.htm` - validation with `htmlhint`
- **JavaScript**: `.js`, `.jsx`, `.ts`, `.tsx` - formatting with `prettier`, linting with `eslint`
- **CSS**: `.css`, `.scss`, `.sass` - formatting with `prettier`, linting with `stylelint`

## Default Behavior
Intelligently detects file types in changed/staged files and runs appropriate specialized formatting commands. Provides granular control while maintaining ease of use.