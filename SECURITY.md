# Security

This document describes how mytesla.io authorizes access, handles tokens,
isolates data, and lets you revoke access. For how to report a vulnerability,
see [Reporting](#reporting-a-vulnerability).

## Authorization model

Two independent OAuth relationships, neither of which exposes your Tesla
credentials to the AI:

1. **AI client → mytesla.io** — your MCP client (Claude, ChatGPT, Cursor, …)
   connects to `https://mcp.mytesla.io/mcp` over **OAuth 2.1** with dynamic
   client registration (RFC 7591). Every MCP request is authenticated as a
   specific user; there is no anonymous access.
2. **mytesla.io → Tesla** — you authorize mytesla.io on **Tesla's own OAuth
   consent screen**, where it appears as "Embay, LLC." You approve a specific
   scope; **that scope is the hard ceiling** — the server cannot request or use
   anything beyond it. A per-vehicle virtual key (approved once on the car) lets
   the vehicle trust commands signed by mytesla.io through Tesla's Vehicle
   Command Protocol.

**We never receive your Tesla password.** Authorization is entirely
OAuth-based.

## Token isolation (the important one)

- **Your AI client never receives Tesla OAuth tokens.** Tesla access/refresh
  tokens are held **server-side only**. Over the MCP channel, the client sends
  and receives **tool calls and their results** (e.g. `set_charge_limit(80)`) —
  never Tesla credentials or tokens.
- **Tokens are encrypted at rest** with **AES-256-GCM**; the encryption key is
  stored as a platform secret, never in source.
- **Refresh-token rotation** on every refresh — the old token is discarded.

## Data handling

- **We do not store** your vehicle's location, drive history, or charge history
  beyond serving the live request.
- **We do not sell** your data, and **we do not train** AI models on your
  conversations or vehicle data.
- Your **prompts are processed by your own AI client**, not by us. mytesla.io
  receives the resulting tool invocations, not your raw conversation.
- See [`PRIVACY.md`](./PRIVACY.md) and <https://mytesla.io/privacy>.

## Application security

- **Transport:** HTTPS enforced end to end.
- **Authorization checks** on every route; users can only access their own data.
- **Input validation:** all tool inputs are validated against strict schemas
  before any upstream Fleet API call.
- **Injection-safe data access:** parameterized queries only.
- **Secrets** live in the platform secret store, never in source control.
- **Scope of action:** 40 fixed tools, no driving capability, PIN-protected
  functions gated by the user's own PIN.

## Revocation — you're always in control

You can cut mytesla.io off instantly, independent of any AI:

1. **Revoke at Tesla:** your Tesla account → third-party apps → remove
   "Embay, LLC." This immediately invalidates all access.
2. **Remove the connector** from your AI client.

Either action stops the server from being able to act, regardless of what any
prompt asks for.

## Reporting a vulnerability

Email **security@mytesla.io** with details and reproduction steps. We
acknowledge reports and coordinate a fix. Please do not open public issues for
security matters.
