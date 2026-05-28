# claude-config

Personal Claude Code configuration: settings, hooks, skills, and installed plugin manifests.

## Layout

| Path | Purpose |
| --- | --- |
| `settings.json` | Main Claude Code settings (theme, permissions, hooks, statusline, enabled plugins). |
| `hooks/` | Local hook scripts wired up in `settings.json` (currently the caveman-mode hooks and statusline). |
| `skills/` | User-level skills available to Claude Code. |
| `plugins/installed_plugins.json` | List of installed plugins. |
| `plugins/known_marketplaces.json` | Configured plugin marketplaces. |

## What is intentionally *not* tracked

Anything runtime, machine-specific, or sensitive is excluded via `.gitignore`:

- `.credentials.json` — Anthropic API credentials. **Never commit.**
- `sessions/`, `projects/`, `session-env/`, `shell-snapshots/`, `history.jsonl` — per-session state and transcripts.
- `tasks/`, `plans/`, `paste-cache/`, `file-history/`, `backups/`, `telemetry/`, `cache/`, `.last-cleanup`, `.caveman-active` — runtime caches and ephemeral state.
- `plugins/cache/`, `plugins/data/`, `plugins/marketplaces/` — plugin runtime data and nested git repos.

## Installing on a fresh machine

```bash
# Back up any existing config first.
mv ~/.claude ~/.claude.bak 2>/dev/null

git clone https://github.com/prdai-archive/claude-config.git ~/.claude
```

Then sign in to Claude Code normally — that re-creates `.credentials.json` and the runtime directories.

## Hooks

The hooks in `hooks/` are wired up in `settings.json`. They reference an absolute Node.js path from `mise`:

```
/home/prdai/.local/share/mise/installs/node/26.1.0/bin/node
```

On a new machine, edit `settings.json` to point at the local Node.js binary (or symlink it).

## Git config

This repo uses a local committer identity:

```bash
git config user.name  "claude"
git config user.email "claude"
```

Set per-repo, not globally.
