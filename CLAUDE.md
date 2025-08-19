# Claude AI Assistant Guidelines

Guidelines for AI-assisted development ensuring consistent, maintainable, and high-quality code.

## Overview

This document provides a structured approach to AI-assisted development with modular guidelines organized by domain. Each module can be used independently or as part of the complete framework.

## Quick Start

1. **[Core Guidelines](.claude/guidelines/core.md)** - Essential principles and workflow
2. **[Language-Specific Guidelines](#language-specific-guidelines)** - Technology-focused practices
3. **[Git Practices](.claude/guidelines/git.md)** - Version control and iterative development
4. **[Claude Code Integration](.claude/guidelines/claude-code.md)** - Tool configuration and automation
5. **[Quality Checklist](.claude/guidelines/quality-checklist.md)** - Comprehensive QA framework

## Language-Specific Guidelines

### Programming Languages
- **[Python Development](.claude/guidelines/python.md)** - Virtual environments, formatting, libraries, and best practices
- **[Frontend Development](.claude/guidelines/frontend.md)** - Modern web development with server-side rendering focus

### Adding New Languages
Create new language-specific guidelines following the established patterns:
- Code standards and formatting
- Library preferences and justifications
- Language-specific best practices
- Quality checklist items

## Configuration Structure

```
.claude/
├── settings.json              # Project-wide settings (team shared)
├── settings.local.json        # Personal overrides (gitignored)
├── commands/                  # Custom slash commands
│   ├── commit.md             # Smart commits with style detection
│   ├── format.md             # Unified formatting across all file types
│   ├── merge.md              # Intelligent commit squashing
│   ├── pyformat.md           # Python formatting and linting
│   ├── reword.md             # Smart message rewording with style transformation
│   ├── validate_setup.md     # Framework setup validation
│   └── webformat.md          # Web frontend formatting
└── guidelines/               # Modular documentation
    ├── core.md               # Core principles and workflow
    ├── python.md             # Python-specific guidelines
    ├── frontend.md           # Web UI/Frontend guidelines
    ├── git.md                # Git practices and workflows
    ├── claude-code.md        # Claude Code integration
    └── quality-checklist.md  # Comprehensive QA checklist
```

### Customization

#### For New Projects
1. Copy `.claude/` directory structure
2. Review and adjust `settings.json` for project needs
3. Customize slash commands in `commands/`
4. Add language-specific guidelines as needed
5. Run `/validate_setup` to verify framework integration

#### For Teams
- Share `.claude/settings.json` and `guidelines/` via version control
- Keep `.claude/settings.local.json` gitignored for personal preferences
- Establish team conventions for slash command naming

#### For Personal Use
- Configure `~/.claude/settings.json` for global preferences
- Add personal commands to `~/.claude/commands/`
- Customize guidelines for individual workflow

## Development Workflow Integration

The modular structure supports the iterative development approach:

1. **Development Phase**: Use `/commit dev` for verbose commits with detailed context
2. **Quality Assurance**: Follow language-specific checklists
3. **History Cleanup**: Use `/merge` and `/reword` with style control for clean final history
4. **Continuous Improvement**: Refine guidelines based on project experience

## Extensions

This framework is designed to be extended:

- **New Languages**: Add guidelines following established patterns
- **New Tools**: Extend Claude Code integration patterns
- **Custom Workflows**: Add project-specific slash commands
- **Team Standards**: Customize guidelines for organizational needs

---

*Living document - adapt to project needs while maintaining core principles.*
