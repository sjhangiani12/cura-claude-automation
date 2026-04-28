# Changelog

All notable changes to the Cura plugin are documented here. Format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/); versioning follows [SemVer](https://semver.org/).

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
