---
description: "Run web frontend formatting tools"
args: "[all|file_pattern]"
---

# Web Frontend Format

Run comprehensive formatting on HTML, JavaScript, CSS files.

## Usage
- `/webformat` - Format only changed/staged web files (git diff)
- `/webformat all` - Format all web files in project
- `/webformat src/` - Format files in src/ directory  
- `/webformat file.js` - Format specific file

## Actions Performed

### Web Files (HTML, JS, CSS)
```bash
# Get changed files if no arguments
if [ -z "$ARGUMENTS" ]; then
  FILES=$(git diff --name-only --diff-filter=AM HEAD | grep -E '\.(html?|js|jsx|ts|tsx|css|scss|sass)$')
  STAGED_FILES=$(git diff --name-only --cached --diff-filter=AM | grep -E '\.(html?|js|jsx|ts|tsx|css|scss|sass)$')
  ALL_CHANGED="$FILES $STAGED_FILES"
elif [ "$ARGUMENTS" = "all" ]; then
  ALL_CHANGED=$(find . -name "*.html" -o -name "*.js" -o -name "*.jsx" -o -name "*.ts" -o -name "*.tsx" -o -name "*.css" -o -name "*.scss" -o -name "*.sass" | grep -v node_modules | grep -v .git)
else
  ALL_CHANGED="$ARGUMENTS"
fi

# Format with prettier (if available)
if command -v prettier >/dev/null 2>&1; then
  prettier --write $ALL_CHANGED
elif command -v npx >/dev/null 2>&1; then
  npx prettier --write $ALL_CHANGED
fi

# Lint JavaScript/TypeScript files
JS_FILES=$(echo $ALL_CHANGED | tr ' ' '\n' | grep -E '\.(js|jsx|ts|tsx)$')
if [ -n "$JS_FILES" ] && command -v eslint >/dev/null 2>&1; then
  eslint --fix $JS_FILES
elif [ -n "$JS_FILES" ] && command -v npx >/dev/null 2>&1; then
  npx eslint --fix $JS_FILES
fi

# Lint CSS files
CSS_FILES=$(echo $ALL_CHANGED | tr ' ' '\n' | grep -E '\.(css|scss|sass)$')
if [ -n "$CSS_FILES" ] && command -v stylelint >/dev/null 2>&1; then
  stylelint --fix $CSS_FILES
elif [ -n "$CSS_FILES" ] && command -v npx >/dev/null 2>&1; then
  npx stylelint --fix $CSS_FILES
fi

# Validate HTML files
HTML_FILES=$(echo $ALL_CHANGED | tr ' ' '\n' | grep -E '\.(html?)$')
if [ -n "$HTML_FILES" ] && command -v htmlhint >/dev/null 2>&1; then
  htmlhint $HTML_FILES
elif [ -n "$HTML_FILES" ] && command -v npx >/dev/null 2>&1; then
  npx htmlhint $HTML_FILES
fi
```

## Default Behavior
Runs only on web files (HTML, JS, CSS) that are modified or staged in git, helping maintain clean commits without reformatting the entire frontend codebase unnecessarily.