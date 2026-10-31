# Example plugin marketplace

Shared Claude Code and Codex plugin marketplace for murmur agents.

Murmur workspaces reference plugins from this repo via their `plugins` list
(`clone_url` + `ref` + `name`); at VM prepare each plugin is installed with the
backend CLI, so every agent in the workspace gets it.

## Plugins

### `linear`

The [Linear MCP server](https://linear.app/docs/mcp) (streamable HTTP,
`https://mcp.linear.app/mcp`) — issues, projects, comments.

Auth: agents are headless, so interactive OAuth is not usable. The plugin's
`.mcp.json` declares Claude's `Authorization: Bearer ${LINEAR_APPLICATION_TOKEN}`
header and Codex's `bearer_token_env_var: LINEAR_APPLICATION_TOKEN` together.
Both reference the same environment variable; no token is stored in this repo.
Deliver that token through a workspace runtime secret mount so it is present
in the agent process environment.

## Adding to a workspace

```
plugins:
  - clone_url: https://github.com/prassoai/example-plugin-market-place
    ref: <pinned-sha-or-branch>
    name: linear
```

## Layout

```
.claude-plugin/marketplace.json   # marketplace "prasso", lists plugins
linear/
  .claude-plugin/plugin.json      # plugin manifest
  .mcp.json                       # Linear MCP server declaration
```
