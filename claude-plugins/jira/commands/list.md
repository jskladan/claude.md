---
argument-hint: "[options]"
description: "List Jira tickets using jtk CLI"
---

## Name
jira:list

## Synopsis
```
/jira:list [options]
```

## Description
List Jira tickets with flexible filtering. Uses `jtk` CLI for all operations.

## Parameters
All parameters are optional and can be combined:
- `--mine` or `--me`: Show only tickets assigned to current user
- `--project <KEY>`: Filter by project key (e.g., PROJ)
- `--sprint current`: Show tickets in current sprint
- `--jql "<query>"`: Custom JQL query for advanced filtering
- `--full`: Include descriptions in output
- `--max <N>`: Maximum results (default: 25)

## Implementation

### 1. Determine Query Type
Based on provided options, choose between:
- `jtk issues list` for project/sprint filtering
- `jtk issues search --jql` for JQL queries or assignee filtering

### 2. Build Command

#### For "my tickets":
```bash
jtk issues search --jql "assignee = '$ATLASSIAN_USER' AND resolution = Unresolved ORDER BY updated DESC" --max N -o json
```

**Note**: The `ATLASSIAN_USER` environment variable must be set (typically to your email address, e.g., `user@company.com`).

#### For project listing:
```bash
jtk issues list --project <KEY> [--sprint current] [--full] [--max N] -o json
```

#### For custom JQL:
```bash
jtk issues search --jql "<query>" [--full] [--max N] -o json
```

### 3. Output Format
Always use `-o json` for machine-readable output, then format into a markdown table.

#### Format JSON to table:
```bash
<json_output> | jq -r '.issues[] | "| \(.key) | \(.fields.issuetype.name) | \(.fields.status.name) | \(.fields.summary) |"'
```

Present results as a markdown table:
```
| Key | Type | Status | Summary |
|-----|------|--------|---------|
| PROJ-123 | Story | In Progress | Example ticket summary |
```

If `--full` is specified, include Description as a separate line below each row or as an additional column if brief.

## Examples

1. **My open tickets**:
   ```
   /jira:list --mine
   ```

2. **Current sprint in project**:
   ```
   /jira:list --project MYPROJ --sprint current
   ```

3. **Custom JQL**:
   ```
   /jira:list --jql "project = MYPROJ AND status = 'In Progress'"
   ```

4. **Detailed view of my tickets**:
   ```
   /jira:list --mine --full
   ```
