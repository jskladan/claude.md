# Claude Code Integration Guidelines

Patterns and practices for effective Claude Code configuration and workflow integration.

## Configuration Hierarchy
- **Enterprise**: System-wide policies (highest precedence)
- **Project**: `.claude/settings.json` (team shared)
- **Local**: `.claude/settings.local.json` (should be gitignored, personal overrides)
- **User**: `~/.claude/settings.json` (global personal settings)

## Permission Philosophy

No default permissions are created, you can use the following framework
in order to setup `.claude/settings.local.json`.

Example is provided in `.claude/example_settings.local.json`.

### **ALLOW - Enable Safe Productivity**
Grant automatic permission for operations that:
- **Read and explore code**: File reading, searching, Git history inspection
- **Format and lint**: Code quality tools that improve without changing logic
- **Safe Git operations**: Status checks, diffs, commits (user controls what gets committed)
- **Documentation access**: Trusted domains for reference material

*Intent*: Maximize AI productivity for exploration and code quality without risk

### **ASK - Require Confirmation for Impact**
Request permission for operations that:
- **Modify files directly**: Moving, copying, deleting files
- **Change system state**: Installing packages, changing permissions
- **Git operations with side effects**: Pushing, pulling, branch switching, history modification
- **Process management**: Killing processes, system-level changes

*Intent*: Maintain user control over potentially impactful decisions

### **DENY - Block Dangerous Operations**
Explicitly block operations that:
- **Risk data loss**: Low-level disk operations, filesystem formatting
- **Could damage system**: Direct hardware access, dangerous system utilities

*Intent*: Prevent catastrophic accidents regardless of user oversight

## Hooks for Automation
- **Pre-tool**: Validate environment, check dependencies
- **Post-tool**: Auto-format, run tests, update documentation
- **Example**: Auto-run `black` and `isort` after code edits

## Slash Commands
- **Built-in**: `/help`, `/clear`, `/review`, `/model`, `/memory`
- **Custom project commands**: Place in `.claude/commands/`
- **Personal commands**: Place in `~/.claude/commands/`

## Development Workflow Integration
- **Context management**: Use `/memory` to maintain project context across sessions
- **Code review**: Leverage `/review` for automated code review patterns
- **Testing**: Custom commands for project-specific testing and deployment
- **Status line**: Configure to display relevant project information

## Configuration Philosophy

### Configuration Files
- **Project settings**: [settings.json](../settings.json) - Team shared configuration with hooks, and tool preferences
- **Personal settings**: [settings.local.json](../settings.local.json) - Individual overrides (gitignored)

### Configuration Intent

#### **Status Line Configuration**
*Purpose*: Provide contextual awareness without cognitive overhead
- Display current Git branch to prevent wrong-branch commits
- Show active AI model to understand capability context
- Include timestamp for session tracking and debugging

#### **Automation Hooks**
*Purpose*: Maintain code quality without manual intervention
- **Post-edit formatting**: Automatically apply consistent code style
- **Environment validation**: Ensure proper setup before operations
- **Quality gates**: Run checks before critical operations

*Philosophy*: Automate the routine, preserve control over the critical

#### **Tool Preferences**
*Purpose*: Optimize tool behavior for development workflows
- **Extended timeouts**: Allow for complex operations and large codebases
- **Sensible defaults**: Configure tools for typical use cases
- **Output formatting**: Optimize information density and readability

*Balance*: Productivity improvements without hiding important information
