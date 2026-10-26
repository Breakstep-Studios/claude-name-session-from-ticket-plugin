---
name: name-session-from-ticket
description: Rename the current Claude Code session to match the ClickUp ticket for the current git branch, so sessions, branches and tickets are easy to associate. Use when the user asks to name/rename/title the session after the ticket or branch. Optional argument is a ClickUp ticket ID to use instead of the branch.
user_invocable: true
---

# Name Session From Ticket

Rename this session to `#CU-<id> <Ticket name>`, e.g. `#CU-868mn2umg Fix the CD client deploy service account`.

## Workflow

### 1. Get the ticket ID

If an argument was passed, use it as the ID (strip a leading `#` or `CU-`).

Otherwise run `git branch --show-current`. Branches follow `#CU-<id>-<type>-<Dashed-Title>`, e.g.:

```
#CU-868mn2umg-feat-Fix-the-CD-client-deploy-service-account
```

Take the first capture of `CU-([A-Za-z0-9]+)` (case-insensitive). If the branch is empty (detached HEAD) or has no match, ask the user for the ticket ID.

### 2. Get the ticket name

Call `clickup_get_task` with the ID and `custom_task_ids: true`. Use the task's `name` as-is.

If the task isn't found, report the ID tried and ask the user to confirm it.

### 3. Rename the session

Call `mcp__ccd_session_mgmt__set_session_title` with `session_id: "self"` and `title: "#CU-<id> <Ticket name>"`.

Reply with one line: the new title, with the ticket name linked to its ClickUp URL.

## Notes

- Read-only on ClickUp: never change the ticket.
- Don't rename the branch.
