# mytesla.io — Tesla MCP Server (public spec & security docs)

**mytesla.io** is a hosted [Model Context Protocol](https://modelcontextprotocol.io)
server that lets an AI assistant (Claude, ChatGPT, Cursor, VS Code, or any MCP
client) read your Tesla's status and send it commands through Tesla's **official
Fleet API** — in plain English.

This repository is the **public specification, tool manifest, and security
documentation** for that server. The production worker is closed-source, so this
repo exists to make the connector **auditable and transparent**: what it
exposes, how authorization works, what data flows where, and what it does and
does not store. Nothing here contains secrets or credentials.

> **Not affiliated with Tesla, Inc.** mytesla.io is an independent service
> operated by **Embay, LLC**, built on Tesla's official Fleet API and Vehicle
> Command Protocol. It is not endorsed by or affiliated with Tesla, Inc.

## At a glance

| | |
|---|---|
| **Endpoint** | `https://mcp.mytesla.io/mcp` |
| **Transport** | Streamable HTTP |
| **Authorization** | OAuth 2.1 (dynamic client registration, RFC 7591) |
| **Tools** | 40 fixed tools (see [`TOOLS.md`](./TOOLS.md)) — no "drive" tool |
| **Upstream** | Tesla Fleet API + Vehicle Command Protocol (official, signed) |
| **Operator** | Embay, LLC |
| **Security contact** | security@mytesla.io |

## How to connect

- **Claude (Desktop / web):** Settings → Connectors → Add custom connector →
  paste `https://mcp.mytesla.io/mcp`
- **ChatGPT** (paid plan, web, Developer Mode): Settings → Connectors → Advanced
  settings → Developer mode → add the URL
- **Cursor / VS Code:** add an MCP server pointing at the URL
- **Claude Code (CLI):** `claude mcp add --transport http mytesla https://mcp.mytesla.io/mcp`

On first connect you complete an OAuth flow. Tesla authorization happens
separately on **Tesla's own consent screen** — mytesla.io never sees your Tesla
password.

## What's in this repo

- [`TOOLS.md`](./TOOLS.md) — the full 40-tool manifest with read-only vs.
  state-changing annotations.
- [`SECURITY.md`](./SECURITY.md) — authorization, token handling, encryption,
  data isolation, revocation, and how to report a vulnerability.
- [`ARCHITECTURE.md`](./ARCHITECTURE.md) — the request/data-flow diagram and
  trust boundaries (where your prompts go, where Tesla tokens live).
- [`PRIVACY.md`](./PRIVACY.md) — what we collect, keep, and never do.

## Key trust properties

- **Your AI client never receives Tesla OAuth tokens.** Tokens are held
  server-side, encrypted at rest; the MCP client only sends tool calls.
- **The Tesla-approved OAuth scope is the hard ceiling.** The server exposes 40
  fixed tools and can't request anything beyond what you approved on Tesla's
  screen.
- **No "drive" tool.** The server controls climate, charging, access, and a few
  security toggles — nothing that moves the car.
- **Revocable anytime** from your Tesla account's third-party-apps settings.

## Links

- Website: <https://mytesla.io>
- Security page: <https://mytesla.io/security>
- Privacy policy: <https://mytesla.io/privacy>
- Server card: <https://mytesla.io/.well-known/mcp/server-card.json>
- Status: <https://mcp.mytesla.io/status>
