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
| `inbound-triage` | Score a founder inbound against your thesis; get a verdict, first-call questions, and a draft reply in your voice |
| `setup` | *(v0.1.1)* Generate `cura-config.md` for your fund |
| `diligence` | *(v0.1.2)* Full company workup → memo in your voice |

Invoke as `/cura:inbound-triage`, `/cura:setup`, `/cura:diligence [company]`, etc. See [docs/build-plan.md](docs/build-plan.md) for the roadmap.

### Quick start (v0.1.0)

The `setup` skill that generates `cura-config.md` ships in v0.1.1. For now, hand-write `cura-config.md` in the directory you're working from. Minimum sections:

```markdown
## Thesis
[1-2 sentences]

## Priority sectors
- [sector]
- [sector]

## Anti-sectors
- [sector]

## Stage & check size
[e.g. pre-seed/seed, $250-500k, lead/co-lead]

## Founder pattern
**Back instantly:** [traits]
**Pass instantly:** [traits]

## Pass criteria
- [hard no]

## Voice references
[paste 1-2 prior reply emails or memos here, OR list file paths to them]
```

Then run `/cura:inbound-triage` and paste an inbound.

## How it works

Every skill reads `cura-config.md` from your working directory — your fund's thesis, sectors, voice, and pass criteria. Outputs land in `cura-outputs/`. Both are gitignored by default.

When the [Cura](https://cura.inc) MCP server is connected, skills augment with fund-specific data: prior memos for voice, portfolio for comparison, network for warm intros. Without Cura, skills run standalone via web research + your config.

## License

MIT — see [LICENSE](LICENSE).

## Feedback

GitHub Issues, or reply to whoever sent you this.
