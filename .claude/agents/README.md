# Custom Agents

This directory contains project-level custom subagents for Claude Code.

## Available agents

| Agent | Purpose | Trigger |
|---|---|---|
| `email-assistant` | Gmail read/draft/reply/send | Mentions of email, reply, inbox, mail |

## How to use

Claude auto-invokes agents based on the `description` field. Or invoke explicitly:

> "Use the email-assistant agent to reply to John's email"

## Setup for email-assistant

The agent uses a `gmail` CLI. Install one of:

**Option 1 — gmail-cli (Node.js):**
```bash
npm install -g @gongrzhe/gmail-cli
gmail auth   # OAuth flow
```

**Option 2 — Gmail MCP server (recommended):**
Add to `~/.claude.json` MCP servers:
```json
{
  "mcpServers": {
    "gmail": {
      "command": "npx",
      "args": ["-y", "@gongrzhe/server-gmail-autoauth-mcp"]
    }
  }
}
```

Then run `claude mcp` to authenticate.

## Adding new agents

Create `<agent-name>.md` with YAML frontmatter:

```markdown
---
name: my-agent
description: When to use this agent (be specific, include trigger keywords)
tools: Read, Bash, Grep
model: sonnet
---

System prompt for the agent goes here.
```
