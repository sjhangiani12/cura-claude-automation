# Monet Plugin Build Plan

**Monet — Claude Automation by [Cura](https://cura.inc).** A Claude plugin for **Cowork** (and Code): VC-specific workflows installed once, invoked from the `/` skill picker. Works standalone; gets sharper when Cura MCP is connected.

> Brand: **Monet** is the plugin/product. **Cura** is the parent brand at cura.inc and the persistent fund-brain MCP. References to "Cura" in this doc as the strategic frame / SaaS / MCP are the parent brand. References to slash commands and the plugin name use "Monet."

---

## Spec corrections (2026-04-28)

The original draft of this plan made a few wrong assumptions about the plugin spec. Corrections below; the rest of the document still applies but should be read with these in mind:

- **No "lobby" skill.** Typing `/monet` in Cowork natively filters the `/` skill picker to skills shipped by this plugin. We don't build a help skill — Cowork does it for free. The "Six Components" section below drops to five.
- **`commands/` is NOT legacy.** Both `commands/` (flat `.md` files) and `skills/<name>/SKILL.md` (subdirectories with optional supporting files) are first-class. Several official Anthropic plugins (`product-management`, `pdf-viewer`) use both. Use `skills/` when a skill needs supporting files; `commands/` for single-file skills.
- **Invocation is the skill name, optionally namespaced.** `/monet:setup` and `/setup` both work. The `description` field in SKILL.md frontmatter is the trigger — written as natural-language use cases, not as event handlers. It does double duty: skill-picker copy AND auto-trigger signal.
- **Skills can be both manually invoked AND auto-triggered.** Earlier framing of "auto-trigger only" was wrong.

---

## Strategic Frame

**Cura vs. Claude.** Claude is the agent — brilliant on-demand, scheduled, and conversational. Cura is the persistent fund brain — always-on, event-driven, cross-run stateful. The plugin is the wedge: free Claude skills that solo GPs install, see value from immediately, and graduate to full Cura when they want continuous monitoring, persistent fund-state, and event-driven intelligence.

**The bet.** Every slash command is a daily reminder of Cura's existence inside the GP's primary work surface. Distribution flywheel disguised as a free plugin.

---

## v1 Scope (Tightened)

**Ships in 2-3 weeks. One orchestrator + foundation, not three.**

```
cura/
├── .claude-plugin/
│   ├── plugin.json
│   └── marketplace.json
├── skills/
│   ├── setup/SKILL.md            ← /monet:setup — config generation
│   ├── triage-inbound-deals/SKILL.md   ← /monet:triage-inbound-deals — score and reply to inbound pitches
│   └── diligence/SKILL.md        ← /monet:diligence — full company workup
├── README.md
├── LICENSE
└── .gitignore
```

**Why tighter:** `/monet:diligence` alone has 7 internal stages — that's real engineering. Three orchestrators in v1 means we discover the pattern is wrong across three skills instead of one. Better to ship one excellent skill, watch 5-10 real users, then extend.

**v1.1 (after real-user validation):** expose internal components as standalone skills, add `/monet:inbound` and `/monet:lp-update`.

**Components built in v1 but not exposed:**
- founder research
- market sizing
- competitor discovery
- competitive analysis
- risk assessment
- memo synthesis

These are stages of `/monet:diligence`, callable as their own skills in v1.1+. Cost is the same; surface area is smaller.

---

## The Five Components of v1

A working v1 plugin needs:

1. **Plugin manifest** — declares the namespace and identity
2. **Config schema** — `monet-config.md`, the fund-specific layer every skill reads
3. **Onboarding skill (`/monet:setup`)** — creates the config (auto-fills from Cura MCP if connected)
4. **Workflow skill** — at least one orchestrator (`/monet:diligence` or `/monet:triage-inbound-deals`) proving the pattern end-to-end
5. **Shared conventions** — config discovery, MCP detection, output handling, voice consistency, fixed-string upgrade nudges

(Cowork natively provides the "lobby" by filtering the `/` picker on the plugin name — no help skill needed.)

---

## 1. Plugin Manifest

`.claude-plugin/plugin.json` — declares plugin identity. Skills auto-discover from `skills/` directory; no need to enumerate.

Includes: name, version, description, author, homepage, repository, license, keywords.

---

## 2. Config Schema (`monet-config.md`)

Human-editable markdown. Lives in working directory. Read by every skill at runtime.

**Sections:**
- **Thesis** — what the fund invests in and why
- **Sectors** — priority order; anti-sectors separately
- **Stage & check size** — pre-seed/seed, $250K-$500K, lead/co-lead, etc.
- **Founder pattern-match** — traits the fund backs vs passes on
- **Voice** — style guide + reference materials (see Voice Ingestion below)
- **Network sources** — top warm intro sources
- **Pass criteria** — explicit anti-thesis

**Design principles:**
- Markdown over JSON (human-editable, easy to share, easy to version-control)
- Schema versioned in a frontmatter block so we can evolve without breaking old configs
- Required fields kept minimal; everything else optional with sensible defaults
- Cura MCP can write to it when connected (auto-updating fund context)

### Voice Ingestion (decided)

Voice is what makes outputs feel like the user's fund, not generic. We support both modes, default to inline:

**Inline (default).** During `/monet:setup`, user pastes 2-3 prior memos or LP updates directly. Stored in `monet-config.md` under a `## Voice References` section with delimiters.

**File paths (alternative).** User can instead point at file paths or a folder of prior memos. Config stores the paths; skills read those files at runtime.

**Skills that produce drafts** (memo synthesis, future LP draft) read whichever is populated. If both, prefer file paths (likely more current).

---

## 3. Onboarding Skill (`/monet:setup`)

Generates `monet-config.md` through a question flow.

**Flow (~5 min standalone):**
1. Thesis (paragraph or paste from website)
2. Sectors and anti-sectors
3. Stage and check size
4. Founder pattern-match (back instantly / pass instantly examples)
5. Voice — inline paste OR file paths
6. Network sources

**Cura-connected variant:** detects Cura MCP, pre-fills from existing fund data, asks for confirmation rather than answers. ~30 seconds.

**Re-run behavior:** edits existing config rather than overwriting. Backs up the previous version to `monet-config.md.bak`.

---

## 4. Diligence Skill (`/monet:diligence [company]`)

Full company workup. Reference implementation that proves the orchestrator pattern.

**Stages (run sequentially, each builds on prior context):**
1. **Company profile** — basic facts, traction, funding history
2. **Founder research** — backgrounds, prior companies, mutual network
3. **Market sizing** — TAM/SAM/SOM with sources
4. **Competitor discovery** — deep search, not just obvious names
5. **Competitive analysis** — positioning, differentiation, moats
6. **Risk assessment** — market, team, execution, timing
7. **Memo synthesis** — all of the above into structured memo, in fund's voice

**Outputs:**
- `monet-outputs/[company]-memo-[date].md` — the memo
- Chat summary including a **"What I researched and what surprised me"** paragraph (the trust-builder — user sees what the orchestrator actually did, not just the artifact)

**Standalone vs. Cura-connected:**
- Standalone: web research + voice from config + thesis from config
- Cura-connected: + your prior memos as voice reference, + your portfolio as comparison set, + your network for warm paths to references

**Fixed-string upgrade nudge at end of every standalone run:**
> "Cura would let this memo reference your fund's prior diligence on similar companies and surface warm intros to customer references. → cura.inc"

(Same string every time. Doesn't try to assess "was this run degraded enough." Always true. Educates the user about what Cura adds.)

---

## 5. Shared Conventions

**Config discovery.** Every skill checks for `monet-config.md`. If missing → suggest `/monet:setup`. If present but stale (>90 days), gentle reminder.

**Cura MCP detection.** Every skill checks if Cura MCP tools are available. If yes → augment with fund-specific data. If no → run standalone.

**Output conventions.**
- Memos and drafts → file in `monet-outputs/` + chat summary
- Every orchestrator chat output ends with "What I researched and what surprised me" paragraph
- Quick research → chat only
- Triage results → table in chat

**Voice consistency.** All draft-producing skills read voice references from config (inline or file paths) before generating output.

**Upgrade nudges (fixed strings, not dynamic judgments).** Each skill has a single hardcoded nudge tied to a specific Cura capability. Examples:
- `/monet:diligence`: "Cura would let this memo reference your fund's prior diligence on similar companies."
- `/monet:setup`: "Cura would auto-populate this from your existing fund data — 30 seconds instead of 5 minutes."
- `/monet:triage-inbound-deals`: "Cura would triage your inbox continuously and surface only the matches — instead of waiting for you to paste them in."

Each is true regardless of run quality. No meta-judgment required.

---

## Packaging & Distribution

- **Repo:** `sjhangiani12/cura-claude-automation` on GitHub (public from day one)
- **Channel:** GitHub repo + Claude plugin marketplace via `marketplace.json`
- **Install (one-line):** `/plugin marketplace add sjhangiani12/cura-claude-automation && /plugin install monet@cura-claude-automation`
- **Pricing:** Free (acquisition layer for Cura)
- **Updates:** Semver tags + GitHub Releases with changelogs
- **Support:** GitHub Issues + cura.inc/support

---

## Build Order

Updated v0.5.2: post solo-GP workflow research and skill-naming convention lock.

| # | Skill | Status |
|---|---|---|
| 1 | `setup` | ✅ shipped (v0.4.1) |
| 2 | `triage-inbound-deals` | ✅ shipped (renamed from `inbound-triage` at v0.5.2) — needs Phase 4-5 testing |
| 3 | `summarize-pending-work-this-week` | next |
| 4 | `write-investment-memo-for-deal` | after #3 |
| 5 | `run-full-diligence-on-company` | after #4 |
| 6 | `draft-warm-intro-for-portco` | |
| 7 | `write-quarterly-lp-letter` | |
| 8 | `prep-for-first-founder-call` | |
| 9 | `gather-references-on-founder` | |
| 10+ | (additional skills from full catalog below as demand surfaces) | |

**No new skill begins until the previous one passes Phase 5** (3 consecutive good runs in real-user testing).

---

## Full Skill Catalog (~22 workflows)

Mapped 1:1 from manual workflows a solo GP does today. Naming convention: `verb-object`, descriptive enough that the picker self-documents. Plurals for stream/firehose ops (`triage-inbound-deals`); singular for the-one-thing ops (`write-investment-memo-for-deal`).

### Sourcing & screening
- `triage-inbound-deals` — score cold emails / intros / pings; verdict + draft reply
- `source-new-deals-by-thesis` — proactively hunt founders matching your thesis
- `share-deal-with-peer-gps` — draft a "thought you'd like this one" email

### Diligence
- `prep-for-first-founder-call` — context + sharp questions before a 30-min intro
- `run-full-diligence-on-company` — multi-stage workup
- `gather-references-on-founder` — find refs, draft outreach, synthesize signal
- `analyze-market-for-deal` — TAM/SAM/SOM, comps, trends
- `find-competitors-for-deal` — competitor search + positioning

### Decision & docs
- `write-investment-memo-for-deal` — investment memo in your voice
- `draft-pass-email-to-founder` — graceful, specific decline
- `review-term-sheet-for-redflags` — term-sheet read, red flags, side-letters

### Portfolio
- `prep-for-portfolio-1on1-call` — talking points + recent context for a portco 1:1
- `draft-warm-intro-for-portco` — match a portco's intro request to your network, draft email
- `prep-for-board-meeting` — deck review, pointed questions
- `parse-founder-update-into-kpis` — convert a founder update email into structured KPIs + flags

### LP communications
- `write-quarterly-lp-letter` — quarterly LP letter in your voice
- `prep-for-lp-1on1-call` — talking points before a 1:1 with an LP
- `draft-capital-call-notice` — capital call note + sub-doc reminders
- `draft-annual-fund-report` — fund annual report assembly

### Operations
- `summarize-pending-work-this-week` — Monday brief: overdue replies, quiet portcos, owed intros, untouched LPs
- `review-active-deal-pipeline` — pipeline hygiene + stale-deal triage

---

## Locked Decisions

- **Plugin name:** `monet` (kebab-case; claims the namespace). Renamed from `cura` at v0.5.0 to distinguish the plugin from the parent brand.
- **Slash command syntax:** `/monet:skill-name` (colon-namespacing per plugin spec)
- **Distribution:** Free, public, GitHub + marketplace
- **v1 scope:** Manifest + config + `/monet:setup` + at least one workflow skill. Cowork's native `/`-picker filtering replaces the lobby. One orchestrator at a time, not three.
- **Config format:** Markdown in working directory
- **Voice ingestion:** Both inline paste (default) and file paths (alternative). Inline at setup, file paths as override.
- **Upgrade nudges:** Fixed strings tied to specific capabilities. No dynamic "was this degraded" judgments.
- **Orchestrator outputs:** Always include "what I researched and what surprised me" summary alongside the artifact.
- **Cura dependency:** Soft (skills work standalone; Cura makes them sharper).
- **`/monet:triage-inbound-deals` architecture:** On-demand only. User pastes/forwards an inbound (cold email, intro, syndicate ping); the skill scores it against config and drafts a reply. Continuous inbox monitoring is a Cura-substrate feature, not a plugin feature.

---

## Real Plugin Spec (from Anthropic docs)

**Required structure:**
```
cura/
├── .claude-plugin/
│   ├── plugin.json          # Manifest
│   └── marketplace.json     # For one-line install
├── skills/                  # Skills with supporting files (subdirectories)
│   ├── setup/SKILL.md
│   ├── triage-inbound-deals/SKILL.md
│   └── run-full-diligence-on-company/SKILL.md
├── commands/                # Optional: flat .md skills without supporting files
├── .mcp.json                # Optional: MCP server definitions
└── README.md
```

Both `skills/` and `commands/` are valid. Use `skills/` when a skill has supporting files (references, scripts); use `commands/` for single-file skills.

**Manifest (`.claude-plugin/plugin.json`):**
```json
{
  "name": "monet",
  "version": "0.5.0",
  "description": "Claude Automation by Cura — VC workflows for solo GPs and small funds",
  "author": { "name": "Cura", "email": "team@cura.inc", "url": "https://cura.inc" },
  "homepage": "https://cura.inc",
  "repository": "https://github.com/sjhangiani12/cura-claude-automation",
  "license": "MIT",
  "keywords": ["vc", "venture-capital", "fund-ops", "diligence"]
}
```

**Skill format (`skills/<name>/SKILL.md`):**
```markdown
---
name: Skill Name
description: When Claude should activate this skill
version: 1.0.0
---

Skill instructions and prompt content...
```

**Invocation:** Type `/` in Cowork to open the skill picker. Type `/monet` to filter to this plugin's skills. Invoke directly with `/monet:setup`, `/monet:triage-inbound-deals`, or just `/setup`, `/triage-inbound-deals` (namespaced form is safer when skill names collide across plugins).

---

## Resolved Open Questions

- ~~Exact plugin manifest format~~ → Confirmed via Anthropic docs
- ~~File paths for config and outputs~~ → `monet-config.md` and `monet-outputs/` in working directory
- ~~How aggressive Cura MCP auto-fill in onboarding~~ → Pre-fill everything, ask for confirmation
- ~~Whether to ship a `/cura` (no suffix) help command~~ → Not needed. Cowork natively filters the `/` picker on the plugin name.
- ~~Memo voice ingestion mechanism~~ → Inline paste (default) + file paths (alternative)
- ~~Upgrade nudge design~~ → Fixed strings per skill, tied to specific capabilities

## Remaining Open Questions (for build time)

- Exact format of voice references inside `monet-config.md` (delimiters, max length)
- Whether `monet-outputs/` should be gitignored by default (probably yes — fund-confidential)
- How skills should display Cura MCP connection status inline when augmenting their output
