# CLAUDE.md Framework

A modular AI development framework for Claude Code that ensures consistent, maintainable, and high-quality code across projects.

## What is this?

This repository provides a structured approach to AI-assisted development through:

- **Modular Guidelines**: Language-specific best practices and workflows
- **Smart Commands**: Custom slash commands for formatting, committing, and quality control
- **Quality Automation**: Integrated linting, formatting, and validation tools
- **Git Integration**: Intelligent commit workflows with history cleanup

## Quick Start

1. Copy the `.claude/` directory to your project
2. Run `/validate_setup` to verify integration
3. Start developing with AI assistance

## Key Features

- **Development Phase**: Use `/commit dev` for detailed development commits
- **Quality Control**: Language-specific formatting with `/format`, `/pyformat`, `/webformat`
- **History Management**: Clean up commits with `/merge` and `/reword`
- **Extensible**: Add new languages and workflows as needed

## Structure

```
.claude/
├── settings.json          # Project configuration
├── commands/              # Custom slash commands
└── guidelines/            # Modular documentation by domain
```

## Recommended Statusline

For enhanced Claude Code experience, install the statusline configuration:
[chongdashu/cc-statusline](https://github.com/chongdashu/cc-statusline)

## Spec-Driven Development

Spec-Driven Development flips the script on traditional software development. For decades, code has been king —
specifications were just scaffolding we built and discarded once the "real work" of coding began.
Spec-Driven Development changes this: specifications become executable,
directly generating working implementations rather than just guiding them.

[github/spec-kit](https://github.com/github/spec-kit)
