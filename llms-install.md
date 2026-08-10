# Installing Verbative Memory (guide for AI agents)

Verbative Memory is a local **MCP server** — a fully on-device memory for AI coding
agents. Installing it means adding it to the client's MCP config; there is no build
step. Pick ONE of the methods below and write the config, then restart the client.

## Recommended — any MCP client (npx)

Add this to the client's MCP settings JSON (e.g. `cline_mcp_settings.json`,
`mcp.json`, or the client's equivalent):

```json
{
  "mcpServers": {
    "verbative-memory": {
      "command": "npx",
      "args": ["-y", "verbative-memory"]
    }
  }
}
```

## Claude Code CLI

```bash
claude mcp add verbative-memory -- npx -y verbative-memory
```

## Python / pip alternative

```bash
pip install verbative-memory
```

Then point the client at the installed console script:

```json
{
  "mcpServers": {
    "verbative-memory": {
      "command": "verbative-memory",
      "args": []
    }
  }
}
```

## First run & requirements

- **Node 18+** (for the npx method) or **Python 3.10+** (for pip).
- On first launch it downloads the on-device engine + models (~4 GB, one time).
  After that it runs **fully offline** — no network calls, nothing uploaded.
- The memory engine needs a **Verbative account** (free 14-day trial) — sign in at
  https://verbative.de. Listing, pinning, and exporting existing memories keep
  working even if the trial lapses.
- Platform: macOS (Apple Silicon) or Windows 10/11 (x64).

## Verify it works

Ask the agent to call the `search` or `list` tool, or `remember` a fact and then
`recall` it. Tools exposed: `remember`, `search`, `recall`, `list`, `pin`,
`forget`, `edit_core`, and more.

## Docs

https://verbative.de/memory
