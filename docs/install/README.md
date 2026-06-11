# Install Waggle

Waggle is local graph memory for coding agents.

Use it to give Claude, Cursor, Codex, Copilot, and other MCP agents persistent repo memory.

No cloud account. No API key. Local by default.

## Install methods

- [VS Code](./vscode.md)
- [Smithery](./smithery.md)
- [Claude Code](./claude-code.md)
- [Claude Desktop](./claude-desktop.md)
- [Codex](./codex.md)
- [Cursor](./cursor.md)
- [Antigravity](./antigravity.md)
- [Generic MCP clients](./generic-mcp.md)
- [Troubleshooting](./troubleshooting.md)
- [Windows setup & troubleshooting](./troubleshooting.md#windows-specific-troubleshooting)

## Client support matrix

Not sure which guide to follow? This matrix shows what each install path configures. Every path runs Waggle locally over stdio.

| Client | Install path | One-line command | MCP config location |
|--------|--------------|------------------|---------------------|
| [VS Code](./vscode.md) | Marketplace extension (one-click) or manual | `Waggle: Enable for this Workspace` | `.vscode/mcp.json` (`servers` root) |
| [Smithery](./smithery.md) | `smithery.yaml` bundle + `pipx` | `pipx install waggle-mcp` | root `smithery.yaml` (stdio) |
| [Claude Code](./claude-code.md) | `claude mcp add` (CLI) | `claude mcp add --transport stdio waggle -- waggle-mcp serve --transport stdio` | managed by `claude mcp` (e.g. project `.mcp.json`) |
| [Claude Desktop](./claude-desktop.md) | `setup --yes` | `waggle-mcp setup --yes --clients claude-desktop` | `claude_desktop_config.json` |
| [Codex](./codex.md) | `setup --yes` (writes an `AGENTS.md` block) | `waggle-mcp setup --yes` | `~/.codex/config.toml` (`[mcp_servers.waggle]`) |
| [Cursor](./cursor.md) | `setup --yes` | `waggle-mcp setup --yes --clients cursor` | `~/.cursor/mcp.json` |
| [Antigravity](./antigravity.md) | `setup --yes` | `waggle-mcp setup --yes --clients antigravity` | generic stdio JSON |
| [Generic MCP clients](./generic-mcp.md) | Manual JSON | `pipx install waggle-mcp` | client's own `mcpServers` JSON |

If a client doesn't pick up the server, see [Troubleshooting](./troubleshooting.md).

## One-line install

```bash
pipx install waggle-mcp
waggle-mcp doctor
```

## Universal stdio config

```json
{
  "mcpServers": {
    "waggle": {
      "command": "waggle-mcp",
      "args": ["serve", "--transport", "stdio"]
    }
  }
}
```

## Verify

```bash
waggle-mcp doctor
waggle-mcp serve --transport stdio
```

## Final checklist

- `waggle-mcp` is on your `PATH`
- `waggle-mcp doctor` reports a writable database path
- Your client config points to `waggle-mcp serve --transport stdio`
- `WAGGLE_DB_PATH` and `WAGGLE_DEFAULT_TENANT_ID` are set if you want non-default storage or tenancy
- The client shows Waggle tools after reload or restart
