# Changelog

All notable changes to the Cura plugin are documented here. Format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/); versioning follows [SemVer](https://semver.org/).

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
