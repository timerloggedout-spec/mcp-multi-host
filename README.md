> **Folded into `termux-monorepo`'s `mcp-hub/`.** This repo was a catalog +
> README only — no server code — kept in sync by hand as a second place.
> The host table and `catalog.json` now live at
> [`termux-monorepo/mcp-hub`](https://github.com/timerloggedout-spec/termux-monorepo/tree/master/mcp-hub)
> (see PR [#442](https://github.com/timerloggedout-spec/termux-monorepo/pull/442)).
> This repo is left in place, not deleted, pending a decision on archiving it.

# mcp-multi-host

Operational registry for the P0 MCP multi-host stack.

## Hosts

| ID | Repo | Transport | Status |
|----|------|-----------|--------|
| termux-mcp | [termux-mcp](https://github.com/timerloggedout-spec/termux-mcp) | Streamable HTTP (Vercel) | repo + GHA ready; deploy needs Vercel role/token |
| android-mcp | [android-mcp](https://github.com/timerloggedout-spec/android-mcp) | Streamable HTTP (Vercel) | same |
| github-remote | GitHub hosted | HTTP | `https://api.githubcopilot.com/mcp/` |
| gh-aw-mcpg | [gh-aw-mcpg_fork](https://github.com/timerloggedout-spec/gh-aw-mcpg_fork) | Gateway | fork present |

See `catalog.json` for machine-readable endpoints + client snippets.

## Deploy Vercel (operator)

Connector token lacks production deploy permission on team `team_jKHy7m9xZrvrGP5cAlIMPs3S`. Use either:

1. **GitHub Actions** (preferred) — set secrets on each MCP repo:
   - `VERCEL_TOKEN`
   - `VERCEL_ORG_ID` = `team_jKHy7m9xZrvrGP5cAlIMPs3S`
   - `VERCEL_PROJECT_ID` = from Vercel project settings after first `vercel link`
   - Then run workflow `Vercel Deploy` (workflow_dispatch or push to main)

2. **CLI**
   ```bash
   cd termux-mcp && vercel link --yes && vercel --prod
   cd android-mcp && vercel link --yes && vercel --prod
   ```

Expected URLs after deploy:
- `https://termux-mcp.vercel.app/mcp`
- `https://android-mcp.vercel.app/mcp`

## Client config (Cursor / MCP hosts)

```json
{
  "mcpServers": {
    "termux": { "url": "https://termux-mcp.vercel.app/mcp" },
    "android": { "url": "https://android-mcp.vercel.app/mcp" },
    "github": {
      "type": "http",
      "url": "https://api.githubcopilot.com/mcp/"
    }
  }
}
```

## Related forks

- gh-aw_fork, gh-aw-mcpg_fork
- gh-mcp_fork, gh_mcp_server_fork, agentix_fork

## License

MIT
