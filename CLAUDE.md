# Cura Plugin — Project Context

## What this is

A plugin for Claude Cowork (and Claude Code) shipping VC-specific workflows for solo GPs. Distributed as a marketplace at `sjhangiani12/cura-claude-automation`. Free; works as acquisition for cura.inc.

## Strategic frame

- Claude is the on-demand agent. Cura is the persistent, event-driven fund brain.
- The plugin is a wedge: free skills that demonstrate value, then upsell to Cura for always-on monitoring, persistent fund-state, and event-driven intelligence.

## How invocation actually works in Cowork

- User types `/` — picker shows all installed skills across plugins.
- User types `/cura` — picker filters to skills from this plugin (Cowork uses the plugin's `name` field for the filter prefix).
- User types `/cura:setup` or `/setup` — invokes the `setup` skill directly. Both namespaced and bare forms work; namespaced is safer when skill names collide across plugins.
- Skills can also auto-trigger when the user's message matches the skill's `description`. Description does double duty: picker copy AND auto-trigger signal.

**Implication:** there is no "lobby skill" to build. `/cura` filtering is native Cowork behavior. We just ship well-named skills with strong descriptions.

## Plugin spec — non-negotiable

- Plugin name: `cura`
- Manifest at `.claude-plugin/plugin.json` (only `name` is required; we also set version, description, author, etc.)
- Skills live at `skills/<name>/SKILL.md` — directories with frontmatter
- `commands/` is also valid — flat `.md` files for skills that don't need supporting assets. Several official Anthropic plugins use both directories (e.g. `product-management`, `pdf-viewer`). Use `commands/` when the skill is a single markdown file; use `skills/` when you want supporting files alongside.
- Repo is also a marketplace via `.claude-plugin/marketplace.json`

## Skill description rules

The `description` field is the trigger. Write it as natural-language use cases, not as event handlers. Compare:

- ❌ Bad: "Activate when the user types /cura:setup"
- ✅ Good: "Generate the fund's cura-config.md. Use when setting up Cura for the first time, when the user asks to configure their thesis/sectors/voice, or when they want to refresh their fund profile."

Study `anthropics/knowledge-work-plugins` skill descriptions as templates (e.g. `sales/skills/call-prep/SKILL.md`).

## Current version: v0.1.0

Shipped:
- Plugin scaffold (manifest, marketplace listing, README, LICENSE, CHANGELOG, .gitignore)
- `inbound-triage` skill — scores a founder inbound against `cura-config.md`, drafts a reply in fund voice. Invoked via `/cura:inbound-triage` or `/inbound-triage`.

Caveat for v0.1.0: `cura-config.md` must be hand-written by the user. The `setup` skill that generates it ships in v0.1.1.

Building next:
- v0.1.1 — `setup` skill (fund config generation, `/cura:setup`)
- v0.1.2 — `diligence` skill (full company workup orchestrator, `/cura:diligence`)

## Key conventions

- Config lives at `cura-config.md` in the user's working directory (gitignored)
- Outputs go to `cura-outputs/` in the user's working directory (gitignored)
- Voice ingestion: inline paste (default) + file paths (alternative)
- Upgrade nudges: fixed strings tied to specific Cura capabilities, never dynamic judgments
- Orchestrator outputs always include "what I researched and what surprised me" summary

## Build approach

- Ship one skill per release (v0.1.1, v0.1.2, etc.)
- Tag every release with semver
- Test by installing in Cowork against a real workflow before announcing
- Watch 5-10 real GPs use a skill before adding the next one

## Reference docs

- Full build plan: `docs/build-plan.md`
- Cowork plugin help: https://support.claude.com/en/articles/13837440-use-plugins-in-claude-cowork
- Plugin spec reference: https://code.claude.com/docs/en/plugins-reference
- Official Anthropic plugins: https://github.com/anthropics/knowledge-work-plugins
