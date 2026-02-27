# OpenClaw on DigitalOcean — Hands-on Session

Slide deck and resources for a knowledge-sharing session on setting up [OpenClaw](https://openclaw.ai/) agents on DigitalOcean, presented by **Set Kyar Wa Lar**.

## What's Covered

- **What is OpenClaw** — Self-hosted messaging gateway for AI coding agents
- **OpenClaw vs Claude Code** — Differences in control, multi-channel routing, and identity setup
- **Install on DigitalOcean** — Step-by-step droplet setup and deployment
- **Workspace, Memory & Git Backup** — Managing agent data and audit trails
- **Skills** — Installing and managing agent capability packs
- **Multi-Agent** — Running isolated agents for different roles
- **Security** — Sandboxing, tool restrictions, and prompt injection awareness

## Resources

| File | Description |
|------|-------------|
| [slides.md](slides.md) | Slidev presentation deck |
| [setup-guide.md](setup-guide.md) | Step-by-step DigitalOcean setup guide |
| [cheatsheet.md](cheatsheet.md) | OpenClaw CLI command reference |
| [notes.md](notes.md) | Speaker notes and prompts |

## Getting Started

### Prerequisites

- [Node.js](https://nodejs.org/) 22+

### Install & Run

```bash
# Install dependencies
npm install

# Start the slide deck in dev mode
npm run dev
```

The slides will be available at [http://localhost:3030](http://localhost:3030).

### Build

```bash
# Build static slides for deployment
npm run build
```

### Export to PDF

```bash
npm run export
```

## Useful Links

- [OpenClaw Docs](https://docs.openclaw.ai/)
- [ClawHub (Skills)](https://clawhub.ai/)
- [DigitalOcean Referral](https://m.do.co/c/47a95fdf065e)

## Tech Stack

- [Slidev](https://sli.dev/) — Markdown-based presentation framework
- [Vite](https://vitejs.dev/) — Build tool

## License

ISC
