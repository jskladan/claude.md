---
description: "Validate Claude Code framework setup and configuration"
args: ""
---

# Framework Setup Validation

Validates the Claude Code framework configuration and environment to ensure proper integration and functionality.

## Usage
- `/validate_setup` - Run comprehensive validation of framework setup

## Validation Categories

### 1. Configuration Integrity
- **JSON validity**: Parse and validate all `.claude/*.json` files
- **Settings structure**: Verify required fields and proper nesting
- **Permission syntax**: Validate permission rules follow `Tool(pattern:*)` format
- **Hook configuration**: Check hook commands and file path references

### 2. Environment Dependencies
- **Tool availability**: Verify tools referenced in hooks exist in PATH
- **Git repository**: Confirm project is in a Git repository
- **File permissions**: Check Claude Code can read/write framework files
- **Python environment**: For Python projects, validate virtual environment

### 3. Runtime Verification
- **Hook execution**: Test sample hook execution (dry run)
- **Slash command discovery**: Verify custom commands are loadable
- **Permission enforcement**: Test ALLOW/ASK/DENY rules are active
- **Settings inheritance**: Confirm local overrides work properly

## Process

### 1. Configuration Analysis
```bash
# Validate JSON files
find .claude -name "*.json" -exec python -m json.tool {} \;

# Check settings structure
cat .claude/settings.json | python -c "import json, sys; config=json.load(sys.stdin); print('✓ Valid configuration')"
```

### 2. Environment Check
```bash
# Check required tools
which black isort prettier eslint git

# Verify Git repository
git status > /dev/null 2>&1 && echo "✓ Git repository" || echo "✗ Not a Git repository"

# Check Python environment
echo $VIRTUAL_ENV || python -c "import sys; print('✓ Python available:', sys.executable)"
```

### 3. Integration Test
```bash
# Test hook availability
python -c "import subprocess; subprocess.run(['black', '--version'])" 2>/dev/null && echo "✓ Black available"

# Check file access
ls -la .claude/ && echo "✓ Framework files accessible"
```

## Success Criteria
- All JSON files parse successfully
- Required tools are available in environment
- Framework files are readable by Claude Code
- No permission conflicts in configuration
- Hooks can execute without errors

## Common Issues & Fixes

### Configuration Problems
- **Invalid JSON**: Fix syntax errors in `.claude/*.json`
- **Missing permissions**: Add required tools to ALLOW list
- **Hook failures**: Install missing formatting tools

### Environment Issues
- **Tool not found**: Install via `pip install black isort` or `npm install -g prettier eslint`
- **Git not initialized**: Run `git init` in project root
- **Permission denied**: Check file permissions with `ls -la .claude/`

### Integration Problems
- **Hooks not triggering**: Verify hook syntax in settings.json
- **Commands not found**: Check `.claude/commands/` directory structure
- **Settings ignored**: Ensure proper JSON syntax and file locations

## Output Format
```
🔍 Validating Claude Code Framework Setup...

Configuration Integrity:
✓ .claude/settings.json - Valid JSON
✓ Permission syntax - All rules valid
✓ Hook configuration - 2 hooks configured
⚠ .claude/settings.local.json - Not found (optional)

Environment Dependencies:
✓ Git repository detected
✓ black (22.3.0) available
✓ isort (5.10.1) available
✗ prettier not found - run: npm install -g prettier

Runtime Verification:
✓ Framework files accessible
✓ Custom slash commands loaded (4 found)
✓ Permission enforcement active

Summary: 8/9 checks passed
Action required: Install prettier for web formatting
```

## Integration
This command verifies the framework is ready for productive AI-assisted development with minimal friction and maximum reliability.