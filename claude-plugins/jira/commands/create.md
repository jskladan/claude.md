---
argument-hint: "<project> <summary> [options]"
description: "Create a Jira ticket using jtk CLI"
---

## Name
jira:create

## Synopsis
```
/jira:create <project> "<summary>" [options]
```

## Description
Create a new Jira ticket. Uses `jtk` CLI for all operations.

## Parameters
Required:
- `<project>`: Project key (e.g., PROJ, MYTEAM)
- `<summary>`: Ticket summary/title (quote if contains spaces)

Optional:
- `--type <type>`: Issue type (Task, Bug, Story, Epic) - default: Task
- `--description "<text>"` or `-d`: Issue description
- `--assignee <user>`: Assign to user (email, account ID, or "me")
- `--parent <KEY>`: Parent issue key (for subtasks or epic children)
- `--field key=value`: Set custom fields (can be repeated)

## Implementation

### 1. Validate Required Parameters
Ensure project and summary are provided. If missing, prompt user.

### 2. Build Command
```bash
jtk issues create \
  --project <PROJECT> \
  --summary "<summary>" \
  [--type <type>] \
  [--description "<description>"] \
  [--assignee <assignee>] \
  [--parent <parent>] \
  [--field key=value] \
  -o json
```

### 3. Execute and Report
Run the command and parse the JSON output to extract the created issue key and URL.

Report back:
- Created issue key (e.g., PROJ-123)
- Direct link to the issue

## Examples

1. **Simple task**:
   ```
   /jira:create PROJ "Fix login button alignment"
   ```

2. **Bug with description**:
   ```
   /jira:create PROJ "Login fails with SSO" --type Bug -d "Users cannot log in when using SSO provider"
   ```

3. **Task under an epic, assigned to me**:
   ```
   /jira:create PROJ "Implement caching layer" --parent PROJ-100 --assignee me
   ```

4. **Story with priority**:
   ```
   /jira:create PROJ "User profile redesign" --type Story --field priority=High
   ```
