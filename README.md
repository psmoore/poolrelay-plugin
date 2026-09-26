# Pool Relay plugin

The Pool Relay connector plus skills that teach an assistant to use it well, packaged for:
- **Claude:** Claude Code, the Claude desktop app, Cowork, and claude.ai through Anthropic's plugin directory.
- **ChatGPT, Codex and other Agent Plugins apps.**

## What's inside

| | |
|---|---|
| `.mcp.json` / `mcp.json` | The connector: `https://www.poolrelay.com/mcp` (OAuth; users sign in with their Pool Relay account). `.mcp.json` is Claude's format and `mcp.json` is the Agent Plugins format; same server. |
| `skills/add-a-facility/` | Putting a facility's schedule into Pool Relay lane by lane: sources, lane counts, lanes, placement, splitting, drafts and questions for staff. |
| `skills/publish-a-pool-calendar/` | Public calendars swimmers can read (lane view, week view, per-program tabs) and embedding them. |
| `.claude-plugin/plugin.json` | Claude plugin manifest |
| `.claude-plugin/marketplace.json` | Lets this folder, or a repo holding it, be added as a Claude plugin marketplace |
| `plugin.json` | Agent Plugins manifest (ChatGPT, Codex) |

## Where each rule lives

- **The must-follow rules live in the connector itself** (`SERVER_INSTRUCTIONS` in `server.ts`):
  - model only the water
  - give every pool real or standard lane counts
  - one event per lane set
  - stage changes in drafts

  They reach every chat that connects, with or without this plugin. Keep them short, because they're read on
  every turn.
- **The skills carry the longer procedures** and are loaded only when the job comes up. When a rule changes,
  change it in both places.

## Install

Claude Code:

```
claude plugin marketplace add psmoore/poolrelay-plugin
claude plugin install pool-relay@pool-relay
```

Then run `/mcp` and sign in to Pool Relay when prompted.

To validate a change: `claude plugin validate . --strict`.

Everyone else needs it published first:
- **Claude:** a public GitHub repo as a marketplace (`claude plugin marketplace add <org>/<repo>`), or Anthropic's
  plugin directory for claude.ai and Cowork.
- **ChatGPT and Codex:** the OpenAI plugin submission portal .

---

This repo is published from `plugin/` in the Pool Relay source; change it there and copy it here.
