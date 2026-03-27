---
argument-hint: "<ticket-key>"
description: "Read a Jira ticket's details using jtk CLI"
---

## Name
jira:read

## Synopsis
```
/jira:read <ticket-key>
```

## Description
Fetch and display detailed information about a specific Jira ticket.

## Parameters
- `<ticket-key>`: Required. The Jira ticket key (e.g., PROJ-123)

## Implementation

### 1. Fetch Ticket
Run the following command, replacing `<KEY>` with the provided ticket key:

```bash
jtk issues get <KEY> -o json | jq -r '"# \(.key): \(.fields.summary)\n\n**Type:** \(.fields.issuetype.name)\n**Status:** \(.fields.status.name)\n**Priority:** \(.fields.priority.name)\n**Assignee:** \(.fields.assignee.displayName // "Unassigned")\n**Reporter:** \(.fields.reporter.displayName)\n**Created:** \(.fields.created)\n**Updated:** \(.fields.updated)\n\n## Description\n\(.fields.description // "No description")"'
```

### 2. Output Format
The command outputs formatted markdown with:
- Ticket key and summary as heading
- Metadata fields (type, status, priority, assignee, reporter, dates)
- Full description

## Examples

1. **Read a ticket**:
   ```
   /jira:read PROJ-123
   ```

2. **Read ticket from current branch** (if branch contains ticket key):
   ```
   /jira:read AIPCC-12974
   ```
