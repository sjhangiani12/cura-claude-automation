# Monet by [Cura](https://cura.inc)

**Claude Automation for solo GPs and small funds.** Available inside [Claude Cowork](https://claude.com/product/cowork) and Claude Code. Onboarding, inbound triage, diligence, and memo drafts — in your voice.

Free. Works standalone. Gets sharper when [Cura](https://cura.inc) MCP is connected.

> Monet is the plugin. [Cura](https://cura.inc) is the persistent fund brain it's built on top of.

## Install

In Cowork, open Customize → marketplace → add `sjhangiani12/cura-claude-automation`, install `monet`. Or via slash:

```
/plugin marketplace add sjhangiani12/cura-claude-automation
/plugin install monet@cura-claude-automation
```

Once installed, type `/monet` in Cowork to filter the picker to Monet skills, or invoke a skill directly with `/monet:skill-name` (or just `/skill-name`).

## Skills

| Skill | What it does |
|---|---|
| `setup` | Guided onboarding — drafts your fund profile from connected tools (Gmail, Attio, Granola, Drive, Cura), you review and edit. Saves to `~/.monet/monet-config.md`. |
| `triage-inbound-deals` | Score a founder inbound against your thesis; get a verdict, first-call questions, and a draft reply in your voice |
| `summarize-pending-work-this-week` | Monday brief: overdue replies, quiet portcos, owed intros, untouched LPs, this week's calendar |
| `prep-for-first-founder-call` | Context + sharp questions before a 30-min intro call |
| `run-full-diligence-on-company` | Multi-stage company workup: founders, market, competitors, risks. Produces structured findings. |
| `gather-references-on-founder` | Find references, draft outreach, provide synthesis rubric |
| `write-investment-memo-for-deal` | Investment memo in your voice from research artifacts |
| `draft-warm-intro-for-portco` | Match a portco's intro request to your network, draft the forwardable email |
| `write-quarterly-lp-letter` | Quarterly LP letter in your voice — pulls portfolio updates, prior letters for voice, fund activity |

Invoke as `/monet:setup`, `/monet:triage-inbound-deals`, etc. See [docs/build-plan.md](docs/build-plan.md) for the roadmap.

## Quick start

1. Install the plugin (above).
2. Type `/monet:setup`. It audits which tools you have connected and offers two modes:
   - **Draft from my tools** — synthesizes your fund profile from Gmail, Attio, Granola, Drive, or Cura. You review and edit. About 1-2 minutes if you have connectors.
   - **Manual questions** — 6 questions about thesis, sectors, stage, founder pattern, voice, network. About 5 minutes.
3. Profile saves to `~/.monet/monet-config.md` — works in every Cowork conversation, no matter what folder you're in.
4. Forward a founder inbound and run `/monet:triage-inbound-deals` to score it.

Re-run `/monet:setup` anytime to update individual sections.

### Recommended connectors

For best results, connect these in Cowork (Connectors page) before running setup:

- **[Cura](https://cura.inc)** — persistent fund brain, makes every Monet skill sharper
- **Attio** — your CRM, for pipeline + portfolio context
- **Gmail** (or Superhuman) — so triage works on forwarded emails
- **Granola** — meeting notes for diligence and follow-ups
- **Google Calendar** — meeting prep before founder calls

Setup runs fine without any of these; it'll just flag what's missing.

## How it works

Your fund profile lives at `~/.monet/monet-config.md` — a single file in your home directory that every Monet skill reads. Run `/monet:setup` once and every skill works in every Cowork conversation, no matter what folder you're in. Edit the file directly anytime, or re-run `/monet:setup` to update individual sections.

When the [Cura](https://cura.inc) MCP server is connected, skills augment with fund-specific data: prior memos for voice, portfolio for comparison, network for warm intros. Without Cura, skills run standalone via web research + your config.

## License

MIT — see [LICENSE](LICENSE).

## Feedback

GitHub Issues, or reply to whoever sent you this.
