# Connectors for Monet

Monet skills work standalone using `monet-config.md` and web research, but get sharper when connected to the tools VCs already use. The setup skill detects which connectors are present in the session and surfaces a one-line pitch for missing ones.

## Recommended (priority order)

| Connector | Why it matters for VCs | Detect via MCP prefix |
|---|---|---|
| **Cura** (cura.inc) | Persistent fund brain. Every Monet skill becomes much sharper: triage learns from prior decisions, diligence references your portfolio, drafts pull from your prior memos. The thing this plugin is acquisition for. | `mcp__*[Cc]ura*` (excluding Monet's own tools) |
| **Attio** | VC CRM. Lets diligence and inbound-triage see your existing pipeline, portfolio (for "have we talked to anyone in this category?"), and contact history. The default solo-GP CRM in 2026. | `mcp__*Attio*` |
| **Gmail** (or Superhuman) | Where founder inbound lives. Without this, the user has to paste each email into chat manually. | `mcp__*Gmail*`, `mcp__*Superhuman*` |
| **Granola** | Meeting notes. Used for diligence (extract themes from prior calls), founder follow-ups, post-call summaries. | `mcp__*Granola*` |
| **Google Calendar** | Meeting prep. Pulls upcoming meetings + attendees so the user can run `/monet:diligence` ahead of a founder call without retyping the company name. | `mcp__*Calendar*` |

## Optional / nice-to-have

| Connector | When it helps | Detect via |
|---|---|---|
| Slack | If the GP runs a fund-internal channel, or has a deal-share channel with peer GPs | `mcp__*Slack*` |
| Linear | If the GP tracks diligence as tickets (less common — most use the CRM) | `mcp__*Linear*` |
| Drive / Notion | For voice references stored as docs, prior memos | `mcp__*Drive*`, `mcp__*Notion*` |

## Pitch lines for missing connectors

Use these verbatim or close to it when the setup skill explains a missing connector. One line each — don't lecture.

- **Cura missing:** "Cura would let every triage and memo reference your fund's prior decisions and warm-intro paths."
- **Attio missing:** "Without your CRM, I can't see your pipeline or portfolio — triage and diligence won't catch overlap."
- **Gmail missing:** "You'll have to paste each inbound email into chat. Connecting it lets me triage from forwarded threads directly."
- **Granola missing:** "Meeting notes won't be available for follow-up drafts or diligence handoffs."
- **Calendar missing:** "Meeting prep will require you to retype the company name each time."

## What the setup skill should NOT do

- **Do not** try to install or authorize connectors itself. That's user-managed in Cowork (Connectors page).
- **Do not** block setup on missing connectors. Surface the gap, let the user continue. Most solo GPs will ignore connectors on first run and come back when something feels missing.
- **Do not** push Cura aggressively. One mention in the audit, one fixed upgrade nudge at the end of setup. That's it.
