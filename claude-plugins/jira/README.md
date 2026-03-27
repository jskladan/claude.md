# Jira Plugin

Jira ticket management using the `jtk` CLI.

## Prerequisites

- `jtk` CLI installed and configured
- Run `jtk init` to set up authentication if not already done

## Commands

### `/jira:list`
List and search Jira tickets with filtering options.

```
/jira:list --mine                              # My open tickets
/jira:list --project PROJ --sprint current     # Current sprint
/jira:list --jql "status = 'In Progress'"      # Custom JQL
```

### `/jira:create`
Create new Jira tickets.

```
/jira:create PROJ "Summary here"                    # Simple task
/jira:create PROJ "Bug title" --type Bug -d "desc"  # Bug with description
/jira:create PROJ "Subtask" --parent PROJ-100       # Under an epic
```

## jtk CLI Reference

This plugin wraps the `jtk` CLI. For full CLI documentation:
```
jtk --help
jtk issues --help
```
