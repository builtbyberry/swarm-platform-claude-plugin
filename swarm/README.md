# Swarm — Claude Code plugin

Connects this project to Swarm, the shared context bus, and teaches the ritual: load context at the start of a task, checkpoint at the end.

## What is inside

- `.mcp.json` — connects the hosted Swarm MCP server at `https://swarmplatform.cloud/mcp/swarm` (browser OAuth on first use; no token to copy).
- `skills/swarm/` — the Swarm skill: how to use the tools well.
- `skills/` — the `/swarm:load`, `/swarm:checkpoint`, `/swarm:onboard`, `/swarm:curate`, and `/swarm:handoff` skills.
- `agents/swarm-dispatch` — a subagent that runs a Swarm dispatch end to end and returns a proposal for you to confirm.
- `hooks/` — reminders to load context at session start, preserve working context before compaction, and checkpoint when you finish.

## Install

From the directory that contains this `swarm/` folder:

```
claude plugin install ./swarm
```

Then restart Claude Code (or run `/reload-plugins`). On first use, Claude opens Swarm in your browser to authorize.

## After install

Run `/swarm:onboard` to bind this project to a channel — the plugin has no channel baked in unless you downloaded a channel-pinned copy, so onboarding (or hand-adding a `<!-- swarm-channel: <key> -->` line to `CLAUDE.md`) is what tells future sessions which one to use.

## Power mode (optional)

The hooks above are reminders — they ask the model to load context, which it usually does. For a deterministic load that runs even if the model forgets, install the `swarm` CLI, create a hook credential under Settings → Connected tools, and let a `SessionStart` hook run it:

```bash
npm install -g @builtbyberry/swarm-cli
swarm login   # paste your Swarm URL + the hook token
swarm install-hooks --client claude
```

The hook token lives in the same place it was created — revoke it any time under Settings → Connected tools.

## License

This plugin is licensed under Apache-2.0 (see `LICENSE`) — fork and adapt the connector freely. The hosted Swarm service it connects to is governed by its own terms; "Swarm" is a trademark and the licence grants no rights to it.
