# Changelog

All notable changes to the Cura plugin are documented here. Format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/); versioning follows [SemVer](https://semver.org/).

## [0.1.0] — 2026-04-28

Initial scaffold + first prototype skill.

### Added
- Plugin manifest at `.claude-plugin/plugin.json`
- Marketplace listing at `.claude-plugin/marketplace.json` for one-line install
- `inbound-triage` skill — scores a founder inbound against the fund's thesis (read from `cura-config.md`) and drafts a reply in the GP's voice. Invoked via `/cura:inbound-triage` or just `/inbound-triage`.
- README, LICENSE (MIT), `.gitignore`
- Build plan at `docs/build-plan.md`
- Project context at `CLAUDE.md`

### Notes
- `setup` skill (creates `cura-config.md`) is planned for v0.1.1. Until then, users running `/cura:inbound-triage` need to hand-write `cura-config.md` in their working directory.
- `diligence` skill is planned for v0.1.2.
- No "lobby" skill — Cowork natively filters the `/` picker by plugin name when the user types `/cura`.
