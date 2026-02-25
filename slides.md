---
theme: default
title: OpenClaw on DigitalOcean
info: Minimal knowledge sharing session by Set Kyar Wa Lar
class: text-center
drawings:
  persist: false
transition: slide-left
mdc: true
---

# OpenClaw on DigitalOcean
## Setting up agents

Set Kyar Wa Lar  
Fullstack Engineer

<!--
Setting up agents
-->

---

# What is OpenClaw?

- Self-hosted messaging gateway for AI coding agents
- Routes messages from channels (Telegram, Discord, WhatsApp, iMessage) to agents
- Agents can run tools (files, shell, browser) in your own environment
- You control config, integrations, and execution runtime

<!--
It's AI assistant that have access to your computer and you can ask it to do things for you.

Self hosted, so it store memory, can handle failovers, etc... (gemini, if failed, use claude)

Example usages...
You can ask it to manage social media, email, etc...

Anyone use openclaw before? Can you share your usage?
-->

---

# OpenClaw vs Claude Code

- OpenClaw is self-hosted; Claude Code is a hosted coding assistant workflow
- OpenClaw focuses on multi-channel routing + agent operations
- OpenClaw supports per-agent workspace, policy, and identity setup
- Best summary: OpenClaw gives more infra/control surface; Claude Code is simpler to start

<!--
Claude Code is like coding focus.

OpenClaw can create multiple personality. Like Health, Work, etc...
(They called it Workspaces)

Run it on your own infra. Local, private cloud etc..

infra/control surface
- workspace, policy, identity

CC operate under one single identity
-->

---

# Install on DigitalOcean

## Basic flow
1. Create a Ubuntu droplet
2. Install Node.js 22+
3. Install OpenClaw: `npm install -g openclaw@latest`
4. Run onboarding: `openclaw onboard --install-daemon`
5. Verify: `openclaw status` and `openclaw health`

## Why DO
- Fast VPS provisioning
- Predictable pricing
- Easy to isolate OpenClaw from personal machine

## Sign-up + guide
- Referral: https://m.do.co/c/47a95fdf065e
- Setup guide: https://github.com/setkyar/openclaw-hands-on/blob/main/setup-guide.md

---
layout: center
class: text-center
---

# Scan to Sign Up

<img src="https://api.qrserver.com/v1/create-qr-code/?size=320x320&data=https://m.do.co/c/47a95fdf065e" alt="DigitalOcean referral QR" style="margin:auto; border-radius: 12px;" />

https://m.do.co/c/47a95fdf065e

---

# Workspace, Memory, and Git Backup

- OpenClaw data lives in `~/.openclaw/` (config, credentials, sessions)
- Treat workspace as private memory for your agents
- Initialize a private git repo for backup/audit trail
- Use `.gitignore` to exclude secrets and sensitive files
- Push to a private remote only

---

# Skills

- Skills are folders with `SKILL.md` instructions
- Per-agent skills: `<workspace>/skills`
- Shared skills: `~/.openclaw/skills`
- Install from registry: `clawhub install <slug>`
- Treat third-party skills as untrusted until reviewed

- Docs: https://docs.openclaw.ai/tools/skills
- ClawHub: https://clawhub.ai/

---

# Multi-Agent

- Use separate agents for different roles and risk levels
- Each agent can have its own workspace, tools, and permissions
- Example: `openclaw agents add work`
- Keep personal/work/automation contexts isolated

- Docs: https://docs.openclaw.ai/concepts/multi-agent

---

# Security

- Assume prompt injection attempts will happen
- Enable sandboxing for untrusted channels/senders
- Restrict dangerous tools (`exec`, `process`, `browser`) where possible
- Never grant elevated/host access to unknown senders
- Keep secrets out of markdown files and rotate keys regularly

<!--
- We got concerns
-->

---
layout: center
class: text-center
---

# Thank you
## Any questions?

<!--
Explain shortcuts - https://github.com/setkyar/openclaw-hands-on/blob/main/cheatsheet.md
-->
