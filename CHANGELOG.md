# Changelog

All notable changes to this project will be documented in this file.

## [0.2.0] - 2026-04-06

### Added
- **Version check on startup.** The MCP server queries
  `https://api.github.com/repos/NYCU-Chung/claude-line-channel/releases/latest`
  on boot and prints a banner to stderr if the local version is out of date.
  The check has a 5 s timeout, is fire-and-forget (never blocks startup), and
  caches its result for 24 h in `$LINE_STATE_DIR/.version-check-cache.json`.
- `LINE_BIND_HOST` environment variable — override the webhook bind host
  (defaults to `127.0.0.1`; set to `0.0.0.0` only if you're not using a
  reverse proxy).
- `unknown-dms.log` — userIds of blocked DMs are now logged to a dedicated
  file (previously only group/room IDs were logged).
- `history.log` is now written by the channel itself, with newline-escaped
  user content to prevent log-injection/prompt-injection on restart.
- `history.log` is auto-rotated at 3 MB (trimmed to 2 MB, keeps most recent).
- `KNOWN_CHAT_IDS` is bootstrapped from `history.log` on startup so the
  `reply`/`send_image` anti-injection allowlist survives restarts.
- `bun.lock` is now committed (previously gitignored) for reproducible installs.

### Changed / Security
- **Fail-closed access control.** If `access.json` exists but is malformed,
  the server now refuses to start. If it becomes unreadable at runtime, all
  messages are dropped (`dmPolicy=disabled`) instead of the previous
  fail-open behavior that would have allowed every sender.
- **Bun HTTP server now binds to `127.0.0.1` by default** (previously `0.0.0.0`).
  This applies to both `server.ts` and `examples/line-router.ts`. Operators
  running behind a reverse proxy see no change; operators who relied on the
  old public bind must set `LINE_BIND_HOST=0.0.0.0`.
- **`dmPolicy: "disabled"` now acts as a kill switch** — it drops every
  message from every source (DMs *and* groups), matching its name. Previously
  it only affected DMs, letting groups still deliver.
- **`get_content` validates `message_id`** as a numeric string before
  interpolating into the LINE URL (prevents URL injection) and now streams
  the response body to disk instead of buffering the entire payload in
  memory. Downloads are capped at 100 MB. Images larger than 5 MB are
  saved to disk but not returned inline.
- **`send_image` now checks `KNOWN_CHAT_IDS`** symmetrically with `reply`,
  so Claude cannot be prompted to push images to arbitrary LINE users.
- **All outbound HTTP calls use `fetchWithTimeout`** (30 s default, 60 s
  for uploads, 5 s for the GitHub version check). Previously, a hung LINE
  API or gofile connection could stall the server indefinitely.
- **LINE/gofile API error bodies are no longer returned to Claude.** Full
  bodies are written to stderr for operator debugging; tool output only
  includes the HTTP status code, so token fragments and internal diagnostics
  don't leak into conversation context.
- **Reply tokens are stored *after* the gate drop check**, so blocked
  senders cannot force the bot to waste reply-quota state.
- **Quoted replies no longer compound prefixes.** Cached text is stored raw;
  the `In reply to:` prefix is added only when rendering a new notification.
- **Log injection via newlines is blocked.** Sender-controlled text written
  to `history.log` has `\n`, `\r`, and control characters replaced with
  visible Unicode glyphs.
- **`mentionPatterns` are pre-compiled** once per access-reload instead of
  recompiling every inbound message (ReDoS mitigation, less CPU).
- **`fetchBotUserId` now retries with exponential backoff** (5s, 10s, 30s,
  60s, 300s) so transient LINE API failures don't permanently disable
  structured `@mention` detection.
- **`KNOWN_CHAT_IDS` is bounded** to 1000 LRU entries to cap memory growth.
- **MCP server version is read from `package.json`** at runtime (was
  hardcoded to `1.0.0`).
- **State directory permissions are enforced on every boot** (`0700`),
  not just when it is first created.
- **`.env` parser only strips quotes when they form a matched pair** around
  the value.
- **`upload_file` validates `expire_minutes`** (1 .. 10080 min), checks the
  target is a regular file, caps file size at 100 MB, and uses `path.basename`
  so Windows paths also work.
- **`get_content` sanitizes Windows reserved filenames** (`CON`, `PRN`,
  `AUX`, `NUL`, `COM1-9`, `LPT1-9`) and control characters.
- **Graceful shutdown** now awaits `httpServer.stop()` so in-flight uploads
  are allowed to complete before exit.
- **Unknown group/DM log writes are deduplicated in-memory** so the same
  userId isn't appended on every message.
- **Nested quote replies use an invisible marker (U+2063)** so user text
  cannot trivially forge an `In reply to:` prefix.

### Removed
- Dead `duration` field on LINE message type (never read).

### Docs
- README security section expanded to document the new fail-closed
  behavior, `LINE_BIND_HOST`, download limits, and history.log escaping.
- ACCESS.md clarifies that `dmPolicy: "disabled"` is a full kill switch.
- README/ACCESS now direct operators to `unknown-dms.log` for user IDs
  (was previously conflated with `unknown-groups.log`).

## [0.1.0]

Initial release.
