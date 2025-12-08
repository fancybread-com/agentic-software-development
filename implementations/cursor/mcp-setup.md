# MCP Setup for Cursor

## Overview

Model Context Protocol (MCP) is the foundation for the Agentic Software Development methodology in Cursor. This guide explains how to configure and use MCP servers.

## What is MCP?

MCP (Model Context Protocol) enables AI models to interact with external tools and services. In the context of this methodology, MCP provides:

- **Atlassian Integration**: Read/write access to Jira and Confluence
- **GitHub Integration**: Repository, branch, and PR management
- **Plan Analysis**: Analyze and preview development plans

## MCP Server Configuration

### Configuration File Location

Cursor MCP configuration is stored in:

- **macOS/Linux**: `~/.cursor/mcp.json`
- **Windows**: `%USERPROFILE%\.cursor\mcp.json`

### Full Configuration Example

```json
{
  "mcpServers": {
    "atlassian": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-atlassian"],
      "env": {
        "ATLASSIAN_USER_EMAIL": "your-email@company.com",
        "ATLASSIAN_API_TOKEN": "your-atlassian-api-token"
      }
    },
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "ghp_your_github_token_here"
      }
    },
    "cursor-plans": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-cursor-plans"]
    }
  }
}
```

## Setting Up Each MCP Server

### 1. Atlassian MCP

#### Create Atlassian API Token

1. Go to [Atlassian Account Settings](https://id.atlassian.com/manage-profile/security/api-tokens)
2. Click "Create API token"
3. Give it a label (e.g., "Cursor MCP")
4. Copy the generated token

#### Configure Atlassian MCP

Add to your `mcp.json`:

```json
{
  "mcpServers": {
    "atlassian": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-atlassian"],
      "env": {
        "ATLASSIAN_USER_EMAIL": "your-email@company.com",
        "ATLASSIAN_API_TOKEN": "your-api-token-here"
      }
    }
  }
}
```

#### Verify Atlassian MCP

Test in Cursor by asking:
```
"Get Jira issue KAN-1"
```

If configured correctly, the AI should fetch the issue details.

### 2. GitHub MCP

#### Create GitHub Personal Access Token

1. Go to [GitHub Settings → Developer settings → Personal access tokens](https://github.com/settings/tokens)
2. Click "Generate new token (classic)"
3. Give it a descriptive name (e.g., "Cursor MCP")
4. Select scopes:
   - `repo` (full control of private repositories)
   - `read:org` (read org and team membership)
   - `read:user` (read user profile data)
5. Click "Generate token"
6. Copy the token (you won't be able to see it again)

#### Configure GitHub MCP

Add to your `mcp.json`:

```json
{
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "ghp_your_token_here"
      }
    }
  }
}
```

#### Verify GitHub MCP

Test in Cursor by asking:
```
"List branches in owner/repo"
```

Replace `owner/repo` with an actual repository you have access to.

### 3. Cursor Plans MCP

#### Configure Cursor Plans MCP

Add to your `mcp.json`:

```json
{
  "mcpServers": {
    "cursor-plans": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-cursor-plans"]
    }
  }
}
```

#### Verify Cursor Plans MCP

Test by creating a plan file and asking:
```
"Analyze plan .plans/test.plan.md"
```

## Verifying MCP Configuration

### Check MCP Status in Cursor

1. Open Cursor Settings (Cmd+, or Ctrl+,)
2. Navigate to "MCP" section
3. Verify all servers show as "Connected"
4. If any show errors, check the configuration

### Test MCP Functionality

Ask the AI to perform a test operation for each server:

**Atlassian MCP:**
```
"Get my Atlassian user info"
```

**GitHub MCP:**
```
"Get my GitHub user info"
```

**Cursor Plans MCP:**
```
"List available plan tools"
```

## Troubleshooting

### MCP Server Not Starting

**Symptoms**: Server shows as "Disconnected" or "Error" in settings

**Solutions**:

1. Check `mcp.json` syntax (valid JSON)
2. Verify `npx` is installed and accessible
3. Check internet connectivity
4. Restart Cursor

### Authentication Failures

**Symptoms**: "Unauthorized" or "Authentication failed" errors

**Atlassian MCP**:

1. Verify email matches your Atlassian account
2. Regenerate API token if expired
3. Check token has required permissions

**GitHub MCP**:

1. Verify token is valid and not expired
2. Check token has required scopes (`repo`, `read:org`)
3. Regenerate token if necessary

### Command Not Found

**Symptoms**: "npx: command not found"

**Solutions**:

1. Install Node.js (includes npm and npx)
2. Verify Node.js is in PATH
3. Restart terminal/Cursor after installation

### MCP Server Crashes

**Symptoms**: Server connects briefly then disconnects

**Solutions**:

1. Check Cursor logs for error messages
2. Try running MCP server manually to see errors:
   ```bash
   npx -y @modelcontextprotocol/server-atlassian
   ```
3. Update to latest MCP server versions
4. Report issue to MCP server maintainers

## Security Best Practices

### Protect Your Tokens

1. **Never commit tokens to version control**

   - Keep `mcp.json` out of git
   - Use environment variables where possible

2. **Use minimal required permissions**

   - GitHub: Only grant scopes you need
   - Atlassian: Use user-specific tokens, not admin tokens

3. **Rotate tokens regularly**

   - Set expiration dates on tokens
   - Regenerate tokens periodically
   - Revoke unused tokens

4. **Use separate tokens per purpose**

   - Don't share tokens between applications
   - Easier to track usage and revoke if compromised

### Environment Variables (Alternative)

Instead of hardcoding tokens in `mcp.json`, use environment variables:

```json
{
  "mcpServers": {
    "atlassian": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-atlassian"],
      "env": {
        "ATLASSIAN_USER_EMAIL": "${ATLASSIAN_EMAIL}",
        "ATLASSIAN_API_TOKEN": "${ATLASSIAN_TOKEN}"
      }
    }
  }
}
```

Then set in your shell profile:
```bash
export ATLASSIAN_EMAIL="your-email@company.com"
export ATLASSIAN_TOKEN="your-token"
```

## Advanced Configuration

### Custom MCP Server Paths

If you need to use a specific version or local MCP server:

```json
{
  "mcpServers": {
    "atlassian": {
      "command": "/path/to/custom/mcp-server",
      "args": ["--config", "/path/to/config.json"]
    }
  }
}
```

### Multiple Atlassian Instances

If you work with multiple Atlassian instances:

```json
{
  "mcpServers": {
    "atlassian-prod": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-atlassian"],
      "env": {
        "ATLASSIAN_CLOUD_ID": "prod-cloud-id",
        "ATLASSIAN_USER_EMAIL": "you@company.com",
        "ATLASSIAN_API_TOKEN": "token-prod"
      }
    },
    "atlassian-dev": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-atlassian"],
      "env": {
        "ATLASSIAN_CLOUD_ID": "dev-cloud-id",
        "ATLASSIAN_USER_EMAIL": "you@company.com",
        "ATLASSIAN_API_TOKEN": "token-dev"
      }
    }
  }
}
```

### Debugging MCP

Enable debug logging:

```json
{
  "mcpServers": {
    "atlassian": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-atlassian"],
      "env": {
        "DEBUG": "mcp:*",
        "ATLASSIAN_USER_EMAIL": "you@company.com",
        "ATLASSIAN_API_TOKEN": "your-token"
      }
    }
  }
}
```

Check Cursor logs for debug output.

## Updating MCP Servers

MCP servers are npm packages and can be updated:

```bash
# Clear npm cache to get latest versions
npx clear-npx-cache

# Or manually update specific packages
npm install -g @modelcontextprotocol/server-atlassian@latest
npm install -g @modelcontextprotocol/server-github@latest
npm install -g @modelcontextprotocol/server-cursor-plans@latest
```

Then restart Cursor to use updated versions.

## Resources

- [MCP Documentation](https://modelcontextprotocol.io)
- [Atlassian MCP Server](https://github.com/modelcontextprotocol/server-atlassian)
- [GitHub MCP Server](https://github.com/modelcontextprotocol/server-github)
- [Cursor Plans MCP Server](https://github.com/modelcontextprotocol/server-cursor-plans)

## Getting Help

If you encounter issues:

1. Check Cursor logs for error messages
2. Verify configuration in `mcp.json`
3. Test MCP servers manually via command line
4. Consult MCP server documentation
5. Ask in Cursor community forums
6. Open issue on relevant GitHub repository
