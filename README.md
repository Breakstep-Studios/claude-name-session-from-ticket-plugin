# Name Session From Ticket Plugin for Claude Code

A Claude Code plugin that renames the current session to match the ClickUp ticket for the current git branch, so sessions, branches and tickets are easy to associate.

## Installation

```
/plugin marketplace add Breakstep-Studios/claude-plugins
/plugin install name-session-from-ticket@breakstep-studios
```

## Prerequisites

- The Claude desktop app (Code tab), which provides the session rename tool.
- A ClickUp MCP server connected in Claude Code with a `clickup_get_task` tool.

## Branch Naming Convention

The skill expects branches that include the ClickUp custom task ID, e.g.:

```
#CU-868mn2umg-feat-Fix-the-CD-client-deploy-service-account
```

## Usage

```
/name-session-from-ticket
/name-session-from-ticket 868mn2umg
```

The session is renamed to `#CU-<id> <Ticket name>`, e.g. `#CU-868mn2umg Fix the CD client deploy service account`. Pass a ticket ID to use it instead of the branch.
