# MCP Setup

Model Context Protocol (MCP) connects your IDE or agent to version control and issue tracking services. This page uses **Cursor** as the primary example; other environments may use different settings locations.

**MCP combination:** GitHub for repositories and pull requests; Jira for issue tracking. ASDLC is optional.

---

## Configuration

**Cursor:** Settings → Features → Model Context Protocol
Or edit `~/.cursor/mcp.json` (macOS/Linux) or `%USERPROFILE%\.cursor\mcp.json` (Windows).
Other environments: see your IDE or agent's MCP documentation.

---

## GitHub + Jira

```json
{
  "mcpServers": {
    "github": {
      "url": "https://api.githubcopilot.com/mcp/",
      "headers": {
        "Authorization": "Bearer <YOUR_GITHUB_TOKEN>"
      }
    },
    "atlassian": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://mcp.atlassian.com/v1/mcp"]
    }
  }
}
```

**GitHub:** [github.com/settings/tokens](https://github.com/settings/tokens) — scopes: `repo`, `read:org`

**Jira:** On first use, your environment may prompt for Atlassian OAuth (e.g. Cursor). Test: *"Get Jira issues in my current sprint"*

---

## Troubleshooting

**MCP not connecting?** Restart your IDE or agent, verify URLs, check internet connection.

**GitHub auth fails?** Verify token has `repo` and `read:org` scopes.

**Atlassian OAuth fails?** Clear browser cookies, try incognito window.

---

[:octicons-arrow-left-24: Back to Getting Started](../getting-started.md)
