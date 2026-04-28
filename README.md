# Cura Plugin

VC workflows for solo GPs and small funds — diligence, setup, and on-demand fund ops, available inside [Claude Cowork](https://claude.com/product/cowork) (and Claude Code).

Free. Works standalone. Gets sharper when [Cura](https://cura.inc) MCP is connected.

## Install

In Cowork, open Customize → browse plugins → install `cura`. Or via marketplace:

```
/plugin marketplace add sjhangiani12/cura-claude-automation
/plugin install cura@cura-claude-automation
```

Once installed, type `/cura` in Cowork to filter the skill picker to Cura skills, or invoke a skill directly with `/cura:skill-name` (or just `/skill-name`).

## Skills

| Skill | What it does |
|---|---|
| `setup` | Guided 5-min onboarding — connector audit + fund profile, generates `cura-config.md` |
| `inbound-triage` | Score a founder inbound against your thesis; get a verdict, first-call questions, and a draft reply in your voice |
| `diligence` | *(v0.3.0)* Full company workup → memo in your voice |

Invoke as `/cura:setup`, `/cura:inbound-triage`, etc. See [docs/build-plan.md](docs/build-plan.md) for the roadmap.

## Quick start

1. Install the plugin (above).
2. Type `/cura:setup` — Cura walks you through ~6 questions about your fund (thesis, sectors, stage, founder pattern, voice, network) and audits which connectors you have wired up. Takes about 5 minutes. Writes `cura-config.md` to your working directory.
3. Forward a founder inbound and run `/cura:inbound-triage` to score it.

Re-run `/cura:setup` anytime to update individual sections without starting from scratch.

### Recommended connectors

For best results, connect these in Cowork (Connectors page) before running setup:

- **Cura** (cura.inc) — persistent fund brain, makes every other skill sharper
- **Attio** — your CRM, for pipeline + portfolio context
- **Gmail** (or Superhuman) — so triage works on forwarded emails
- **Granola** — meeting notes for diligence and follow-ups
- **Google Calendar** — meeting prep before founder calls

Setup runs fine without any of these; it'll just flag what's missing.

## How it works

Every skill reads `cura-config.md` from your working directory — your fund's thesis, sectors, voice, and pass criteria. Outputs land in `cura-outputs/`. Both are gitignored by default.

When the [Cura](https://cura.inc) MCP server is connected, skills augment with fund-specific data: prior memos for voice, portfolio for comparison, network for warm intros. Without Cura, skills run standalone via web research + your config.

## License

MIT — see [LICENSE](LICENSE).

## Feedback

GitHub Issues, or reply to whoever sent you this.
