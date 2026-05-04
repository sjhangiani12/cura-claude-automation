# Changelog

All notable changes to the Monet plugin are documented here. Format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/); versioning follows [SemVer](https://semver.org/).

> Brand history: this plugin was named `cura` through v0.4.1. Renamed to `monet` at v0.5.0 to distinguish the plugin/product (Monet) from the parent company (Cura at cura.inc). All `/cura:*` commands and `~/.cura/` paths from earlier versions are now `/monet:*` and `~/.monet/`.

## [0.6.0] — 2026-05-04

Big drop: 7 new priority skills built. Plugin now covers the core solo-GP workflow loop end-to-end.

### Added
- **`summarize-pending-work-this-week`** — Monday-morning brief across 8 categories of pending work (cold inbounds, active deals, quiet portcos, untouched LPs, owed intros, this week's calendar, dropped commitments, stale pipeline). Pulls from Gmail/Calendar/Attio/Granola/Drive/Cura. Per-category query directives in `references/categories.md`.
- **`prep-for-first-founder-call`** — pre-meeting brief in 60-90 seconds: company snapshot, founder snapshot, thesis-fit indicators, 5-7 founder-specific questions. Question-quality patterns in `references/question-bank.md` (sector + stage specific).
- **`run-full-diligence-on-company`** — 6-stage workup (company profile, founders, market, competitive, risks, reference candidates). Produces structured findings at `~/.monet/outputs/[company]-diligence-[date].md`. Per-stage research directives in `references/diligence-stages.md`.
- **`gather-references-on-founder`** — finds 5-8 plausible reference candidates from the GP's network, drafts outreach emails per candidate, provides 5-question synthesis rubric for capturing signal during/after calls. Rubric in `references/reference-rubric.md`.
- **`write-investment-memo-for-deal`** — full memo from diligence artifacts. Default 2000-3000 words; `--short` flag for one-pager. Heavy emphasis on voice fidelity (see `references/voice-rules.md`). Memo template at `references/memo-template.md`.
- **`draft-warm-intro-for-portco`** — matches portco intro request to GP's network (Attio + Gmail + Cura), ranks by warmth × relevance, drafts forwardable email in GP voice with optional permission ping for stale/reach connections. Rules in `references/intro-rules.md`.
- **`write-quarterly-lp-letter`** — quarterly LP letter as creative writing in GP voice (not templatized). Pulls prior letters from Drive for voice gold, portfolio updates this quarter, fund operations. Format guide in `references/lp-letter-format.md`.

### Conventions established
- **Outputs to `~/.monet/outputs/`.** Memos, diligence findings, LP letters all save here — same user-level location as the config. Triage and prep skills are chat-only (ephemeral).
- **Voice rules shared.** All long-form skills (memo, LP letter, intro, pass email) reference `skills/write-investment-memo-for-deal/references/voice-rules.md` for voice cloning.
- **Skills compose.** `run-full-diligence` produces findings → `gather-references` adds signal → `write-investment-memo` synthesizes. Each can also run standalone.
- **Footer everywhere.** Every skill ends with `— Monet, by Cura (cura.inc)` and a Cura-MCP-aware upgrade nudge.
- **Imperative skill bodies, plain user-facing language.** Same rules as `setup` and `triage`.

### Notes
- This is the full priority-8 catalog. Future skills (`source-new-deals-by-thesis`, `prep-for-board-meeting`, `draft-capital-call-notice`, etc.) ship only after the priority 8 hit Phase 5 stability (3 consecutive good runs in real-user testing).
- All skills are buildable with currently-available connectors. Cura MCP integration is already wired in — when Cura ships, skills will get sharper without code changes.

## [0.5.2] — 2026-04-29

Skill naming convention locked. First rename: `inbound-triage` → `triage-inbound-deals`.

### Changed
- **Skill rename: `inbound-triage` → `triage-inbound-deals`.** Slash command is now `/monet:triage-inbound-deals`. Old `/monet:inbound-triage` no longer works.
- **Naming convention locked across the catalog.** Verb-object, descriptive enough that the picker self-documents. Plurals for stream ops; singular for the-one-thing ops. Future skills will follow this pattern: `summarize-pending-work-this-week`, `write-investment-memo-for-deal`, `run-full-diligence-on-company`, `draft-warm-intro-for-portco`, `write-quarterly-lp-letter`, `prep-for-first-founder-call`, `gather-references-on-founder`.
- `docs/build-plan.md` now contains the full ~22-skill catalog, organized by category, mapped 1:1 from manual VC workflows.
- README + CLAUDE.md updated to reflect the new skill name and roadmap.

### Notes
- The renamed skill's behavior is unchanged from v0.5.1 — same prompts, same output format, same fallback chain. This is purely a rename.
- Build process: no new skill begins until the previous one passes Phase 5 (3 consecutive good runs in real-user testing).

## [0.5.1] — 2026-04-28

Brand polish: lead with "Monet by Cura" everywhere user-facing.

### Changed
- Marketplace title and plugin description lead with "Monet by Cura" (was "Claude Automation by Cura"). Cura is visible at first read in the marketplace, README, and skill outputs — but the slash command stays `/monet:*` for typing speed.
- README title is now "Monet by Cura" with sub-tagline "Claude Automation for solo GPs and small funds."
- Every skill output ends with the footer `— Monet, by Cura (cura.inc)` on its own line. Quiet, constant brand presence.
- `CLAUDE.md` locks the brand convention so future skills don't drift: marketplace + README + first-action copy + footers all carry "by Cura"; slash commands stay short.

## [0.5.0] — 2026-04-28

Renamed: cura → monet.

### Changed
- **Plugin name: `cura` → `monet`.** Slash commands change: `/cura:setup` → `/monet:setup`, `/cura:inbound-triage` → `/monet:inbound-triage`. The plugin is now branded "Monet — Claude Automation by Cura."
- **Config path: `~/.cura/cura-config.md` → `~/.monet/monet-config.md`.** Setup skill auto-detects legacy configs at `~/.cura/cura-config.md` and `./cura-config.md` (very old working-dir location) and offers to migrate them. No manual data migration needed.
- All skill references, README, build plan, and project context updated to reflect the rename. References to "Cura" the parent brand at cura.inc are preserved (Cura MCP, cura.inc upgrade nudges, parent brand attribution).

### Added
- Roadmap section in `CLAUDE.md` reflecting the post-research priority order: `weekly-digest`, `memo-write`, `intro-triage`, `lp-letter`, `reference-orchestration`.
- 5-phase build process documented in `CLAUDE.md` (JTBD → Design → Build → Test → Tighten) so future skills are built thoughtfully, not stacked.
- Surprising-findings section in `CLAUDE.md` from solo-GP workflow research (CRM is a graveyard, voice fidelity is the killer feature, etc.).

### Migration for existing testers
- v0.4.x users with `~/.cura/cura-config.md`: re-run `/monet:setup`. The skill will detect your old config and offer to copy it to `~/.monet/monet-config.md`. Backup of the old file is automatic.
- Slash invocations: `/cura:setup` no longer works. Use `/monet:setup`.

## [0.4.1] — 2026-04-28

Setup synthesis: batch the queries, single review.

### Changed
- `setup` synthesis flow restructured from per-section interactive ("here's sector — confirm? — here's stage — confirm?") to **batch synthesis + unified review**: all sections drafted in parallel from connected tools, then the user sees the whole drafted profile at once and edits the sections that need changing. Faster, less conversational fatigue, easier to spot inconsistencies between sections.
- New review step has clear options: [Approve all], [Edit something] (loops through sections), [Show me my voice samples first], [Start over manually].
- Sections that couldn't be synthesized are surfaced with `_(needs your input)_` markers and the user is forced to address them before save (no silent `(not specified)` writes).

## [0.4.0] — 2026-04-28

Setup synthesizes the fund profile from connected tools.

### Added
- **Synthesis mode in `/cura:setup`.** When Gmail, Attio, Granola, Drive, or Cura is connected, setup now offers to draft the fund profile from those tools instead of asking 6 questions cold. The user confirms or corrects each derived section.
  - **Sectors** — derived from Attio or Cura portfolio (group by industry tag)
  - **Stage & check** — derived from median of last N investments
  - **Network** — derived from Attio contact frequency or Gmail thread count
  - **Voice** — derived from Gmail sent emails (last 90 days of founder replies) + Drive memos + Granola transcripts
  - **Thesis** — derived from Drive docs ("thesis", "fund memo") or fund website
  - **Founder pattern** — best-effort from past decisions in Cura/Attio; usually still asks the user
  - Each derivation is shown to the user with its source ("drafted from your Attio portfolio of 23 companies"). Full directives in `skills/setup/references/synthesis.md`.
- Three modes via `AskUserQuestion`: [Draft from my tools] [Manual questions] [Mix — draft what's possible, ask the rest].

### Changed
- `setup` SKILL.md restructured: Steps 0-2 unchanged (state check, frame, connector audit), new Step 3 picks mode, Step 4 branches to synthesis or manual, Steps 5-7 unchanged.
- Upgrade nudge now branches: "Cura would auto-populate this..." when Cura MCP is missing; "Profile drafted from your Cura fund brain" when present.

### Notes
- Synthesis works without Cura MCP — Attio + Gmail alone cover sectors, stage, network, and voice. Cura adds founder pattern derivation and full thesis lookup.
- The `created_via` source attribution in the saved config lets future setup re-runs offer "your portfolio's grown — re-derive sectors?"

## [0.3.0] — 2026-04-28

Config now persists across Cowork sessions.

### Changed
- **`cura-config.md` moved from working directory to `~/.cura/cura-config.md`.** This is a user-level location that persists across every Cowork conversation, working directory, and plugin update. Run `/cura:setup` once and all Cura skills work in every conversation without re-entering your fund profile.
- `setup` skill writes to and reads from `~/.cura/cura-config.md`. Backups (when "Refresh everything") go to `~/.cura/cura-config.md.bak`.
- `inbound-triage` reads `~/.cura/cura-config.md` first, falls back to `./cura-config.md` if found there (with a one-time nudge to migrate via `/cura:setup`).

### Migration for v0.2.0 testers
Re-run `/cura:setup` once. Old `./cura-config.md` files in working directories are detected and the user is prompted to migrate. Setup takes ~5 minutes.

## [0.2.0] — 2026-04-28

The actual onboarding ships.

### Added
- **`setup` skill** — guided 5-minute onboarding. Audits which connectors (Gmail, Calendar, Attio, Granola, Cura) are wired in the user's Cowork session, captures the fund profile via 6 questions, and writes `cura-config.md` to the working directory. Re-runnable; can update individual sections without restarting from scratch. Invoked via `/cura:setup` or `/setup`.
- `skills/setup/references/config-schema.md` — the canonical `cura-config.md` template, plus reading conventions for skills that consume it.
- `skills/setup/references/connectors.md` — connector recommendation table, MCP-prefix detection rules, and pitch lines for missing connectors.

### Changed
- `inbound-triage` now falls back gracefully when no `cura-config.md` exists: if the user pastes fund context inline alongside the inbound, the skill works off that for a single run.

## [0.1.0] — 2026-04-28

Initial scaffold + first prototype skill.

### Added
- Plugin manifest at `.claude-plugin/plugin.json`
- Marketplace listing at `.claude-plugin/marketplace.json` for one-line install
- `inbound-triage` skill — scores a founder inbound against the fund's thesis (read from `cura-config.md`) and drafts a reply in the GP's voice. Invoked via `/cura:inbound-triage` or `/inbound-triage`.
- README, LICENSE (MIT), `.gitignore`
- Build plan at `docs/build-plan.md`
- Project context at `CLAUDE.md`

### Notes
- No "lobby" skill — Cowork natively filters the `/` picker by plugin name when the user types `/cura`.
