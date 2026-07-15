# Swarm MCP tools

The tools available once a client is connected to Swarm, grouped by the loop.

## Load context (start of a task)

- `get_context_for_injection` — load what other conversations already know: channel records and your private working context. Returns the channel's resolved `capture_mode` and the end-of-conversation `guidance`. **Call this first.**
- `list_channels` — list the channels you can reach. Use it to **discover** candidates, not to silently pick one; the active channel comes from an explicit binding or the user's choice.
- `list_recent_sessions` — your own recent private captured conversations.

## Fetch on demand

**Fetch on demand** — the ranking already narrowed the channel down to the relevant few, so do not respond to an injection payload by re-querying or filtering it yourself; call `fetch` with a record's id to go deeper on demand. When headline mode is active, injected records come back as a headline + one-line summary rather than the full body. Read headlines first, and fetch a record's full `What`/`Why` only when the task actually needs it. This is deliberate, not a degraded result.

- `fetch` — fetch the full `What`/`Why` text of a single record by id, as returned in a headline or by `search`. Call it per-record, on demand.
- `search` — search records by keyword, returning lightweight `{id, title, url}` matches. Pair with `fetch` to read a specific match in full.

## Working context (private)

- `capture_context` — capture a private working note inside a channel. Stays yours until shared or promoted.

## Checkpoint (end of a meaningful chunk)

- `share_session` — checkpoint a private conversation to its channel, exposing its summary and provenance to teammates (never raw content, no record created). Pass `trigger=agent_auto` only when the mode is Auto; otherwise `trigger=user_request` after the user agrees.

## Curate durable canon (explicit user intent)

- `promote_context_to_record` — promote a private conversation into a channel-visible intelligence record.
- `create_record` — create a channel-visible record directly, without a private conversation source.
- `create_relationship` — link two records in the same channel with a typed, directional relationship.
- `supersede_record` / `unsupersede_record` — mark one record as replacing another as current truth, or undo it.
- `record_history` — the redaction-safe audit trail for a record.

## Handoffs

- `create_handoff_bundle` — package context to hand from one actor to another within a channel.
- `inspect_handoff_bundle` — read a bundle: actors, narrative, open questions, ordered reading path.
- `acknowledge_handoff_bundle` — acknowledge a bundle as its recipient.

## Project setup

- `onboard_project` — create a channel and seed it with typed records distilled from a project. Run once per project; the `onboard-project` prompt walks the full flow.
- `set_channel_workspace` — assign a channel to one of your workspaces.
- `report_dispatch_progress` — post a short live progress note to a dispatch run.
