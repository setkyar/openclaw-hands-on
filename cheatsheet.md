# OpenClaw Cheatsheet (English)

Verified on **February 24, 2026** against `openclaw` CLI **v2026.2.23** (`openclaw --help`).

## 1. Architecture (Quick View)

```text
You -> Channel -> Gateway -> Agent -> Skills/Tools
                         |            |
                         v            v
                      Sessions      Memory
```

- `Gateway` handles routing, auth, RPC, and orchestration.
- `Channels` connect Telegram/Discord/Slack/etc.
- `Agent` executes tasks with model + tools.
- `Skills` are capability packs; inspect with `openclaw skills ...`.
- `Memory` is searchable/indexed by the memory subsystem.

## 2. Install and Onboarding

```bash
# Install CLI (official installer)
curl -fsSL https://openclaw.ai/install.sh | bash

# Verify
openclaw --version

# Interactive onboarding (gateway/workspace/skills/channels)
openclaw onboard

# Common first-run option from course: install gateway service
openclaw onboard --install-daemon
```

## 3. Gateway Control (Correct Commands)

```bash
# Foreground gateway process
openclaw gateway run

# Service lifecycle
openclaw gateway start
openclaw gateway status
openclaw gateway restart
openclaw gateway stop

# Gateway health
openclaw gateway health
openclaw health
```

## 4. Configuration

```bash
# Interactive config wizard
openclaw config

# Read/write config values by path
openclaw config get <path>
openclaw config set <path> <value>
openclaw config unset <path>

# Model defaults
openclaw models list
openclaw models status
openclaw models set <model>
```

## 5. Channels

```bash
# List channels/accounts
openclaw channels list

# Add/update a channel account
openclaw channels add --channel telegram --token <bot_token>

# Channel login (for channels that support interactive linking)
openclaw channels login --channel whatsapp

# Probe channel health
openclaw channels status --probe

# Remove/disable a channel account
openclaw channels remove --channel telegram
```

## 6. Skills

```bash
# List available skills
openclaw skills list

# Readiness check (what is usable vs missing requirements)
openclaw skills check

# Inspect one skill
openclaw skills info <skill_name>

# Optional ecosystem command (if clawhub CLI is installed)
clawhub install <slug>
clawhub update --all
```

## 7. Multi-Agent

```bash
# List agents
openclaw agents list

# Add isolated agent profile
openclaw agents add work
```

## 8. Memory, Logs, Diagnostics

```bash
# Memory status/search/reindex
openclaw memory status
openclaw memory search "<query>"
openclaw memory index --force

# Logs
openclaw logs --limit 200
openclaw logs --follow

# Full system checks
openclaw status --all
openclaw doctor

# Security audit (from course)
openclaw security audit --deep
openclaw security audit --fix
```

## 9. Cron Jobs

```bash
# Add a recurring job
openclaw cron add --name daily-brief \
  --cron "0 7 * * 1-5" \
  --message "Send my daily briefing" \
  --channel telegram \
  --to <destination>

# List jobs
openclaw cron list

# Run now (debug)
openclaw cron run <job_id>

# Disable/enable/remove
openclaw cron disable <job_id>
openclaw cron enable <job_id>
openclaw cron rm <job_id>
```

## 10. Security and Sandbox Notes

```bash
# Security-first defaults to review in config:
# sandbox.mode: off | non-main | all
# sandbox.scope: session | agent | shared
# workspaceAccess: none | ro | rw

# Build sandbox image inside a cloned OpenClaw source repo
./scripts/sandbox-setup.sh
```

## 11. Common Fixes

```bash
# Port conflict check (default common port in examples: 18789)
lsof -i :18789

# If needed, run gateway on a different port
openclaw gateway run --port 18790 --force

# Deep channel and usage checks
openclaw status --deep --usage

# Repair common local issues
openclaw doctor --repair
```

## 12. Useful Links

- Docs: https://docs.openclaw.ai/cli
- Skills hub: https://clawhub.com/
- Community: https://discord.gg/openclaw
