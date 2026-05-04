# Monet Plugin — Project Context

## What this is

**Monet** is a Claude plugin (Cowork + Code) shipping VC-specific workflows for solo GPs. It's a product by **Cura** (cura.inc) — distributed as a marketplace at `sjhangiani12/cura-claude-automation`. Free; works as acquisition for the Cura SaaS platform.

> Brand: **"Monet by Cura"** is the canonical product name when shown to users. **Monet** is the slash-command name (`/monet:setup`). **Cura** is the parent brand at cura.inc and the persistent fund-brain MCP. Cura is visible in everything the user reads (marketplace title, README, first-action copy, every skill's output footer); the slash command stays short.

## Brand convention (lock this — don't drift)

- **Marketplace title and README:** "Monet by Cura"
- **Plugin description (manifest + marketplace):** lead with "Monet by Cura — …"
- **Setup's first message:** "Hi — I'm Monet, the Claude Automation plugin from Cura (cura.inc)."
- **Every skill's output footer:** end with `— Monet, by Cura (cura.inc)` on its own line. Quiet but constant. Below any upgrade nudge.
- **Slash commands:** stay `/monet:*` for typing speed.
- **Don't say "the Cura plugin"** anywhere — it's "Monet" or "Monet by Cura."

## Strategic frame

- Claude is the on-demand agent. Cura is the persistent, event-driven fund brain.
- Monet is the wedge: free skills that demonstrate value, then upsell to Cura SaaS for always-on monitoring, persistent fund-state, and event-driven intelligence.
- **Reframe of Monet's value prop (post-research):** "calendar reclamation," not "better decisions." Solo GPs are confident about their judgment and self-conscious about their throughput. Monet gives them back 15-25 hours a month.

## How invocation actually works in Cowork

- User types `/` — picker shows all installed skills across plugins.
- User types `/monet` — picker filters to skills from this plugin.
- User types `/monet:setup` or `/setup` — invokes the `setup` skill directly. Both namespaced and bare forms work; namespaced is safer when skill names collide across plugins.
- Skills can also auto-trigger when the user's message matches the skill's `description`. Description does double duty: picker copy AND auto-trigger signal.

## Plugin spec

- Plugin name: `monet`
- Manifest at `.claude-plugin/plugin.json` (only `name` is required; we also set version, description, author, etc.)
- Skills live at `skills/<name>/SKILL.md` — directories with frontmatter
- `commands/` is also valid — flat `.md` files for skills that don't need supporting assets. Several official Anthropic plugins use both (e.g. `product-management`, `pdf-viewer`).
- Repo is also a marketplace via `.claude-plugin/marketplace.json`. Marketplace name stays `cura-claude-automation` (the umbrella for Cura's plugins); plugin name is `monet`.

## Skill description rules

The `description` field is the trigger. Write it as natural-language use cases, not as event handlers. Compare:

- ❌ Bad: "Activate when the user types /monet:setup"
- ✅ Good: "Generate the fund's monet-config.md. Use when setting up Monet for the first time, when the user asks to configure their thesis/sectors/voice, or when they want to refresh their fund profile."

Study `anthropics/knowledge-work-plugins` skill descriptions as templates (e.g. `sales/skills/call-prep/SKILL.md`).

## Current version: v0.6.0

Shipped — all priority skills:
- `setup` — onboarding (synthesis or manual), writes `~/.monet/monet-config.md`
- `triage-inbound-deals` — verdict + draft reply for cold founder inbound
- `summarize-pending-work-this-week` — Monday brief across all categories of pending work
- `prep-for-first-founder-call` — pre-meeting brief with founder-specific questions
- `run-full-diligence-on-company` — multi-stage workup → structured findings file
- `gather-references-on-founder` — candidate references + outreach drafts + synthesis rubric
- `write-investment-memo-for-deal` — full memo from diligence artifacts in GP voice
- `draft-warm-intro-for-portco` — match portco intro request → forwardable email
- `write-quarterly-lp-letter` — quarterly LP letter in GP voice

Outputs (memos, diligence findings, LP letters) go to `~/.monet/outputs/`. Config stays at `~/.monet/monet-config.md`. Both persist across all Cowork conversations.

Skills compose naturally:
- `prep-for-first-founder-call` → first call → `triage-inbound-deals` (if cold) or `run-full-diligence-on-company` (if pursuing)
- `run-full-diligence-on-company` → produces findings → `gather-references-on-founder` adds reference signal → `write-investment-memo-for-deal` synthesizes the memo

References (per-skill detail) live at `skills/<name>/references/`. The shared voice-rules are at `skills/write-investment-memo-for-deal/references/voice-rules.md` — referenced by other long-form skills.

## Naming convention (locked)

- **Verb-object** skill names that map 1:1 to a manual VC workflow.
- Be specific. `summarize-pending-work-this-week` not `weekly-digest`. `write-investment-memo-for-deal` not `memo-write`.
- Plurals for stream/firehose ops (`triage-inbound-deals`); singular for the-one-thing ops (`write-investment-memo-for-deal`).
- The picker is the discoverability layer — names should be self-documenting so a GP can scan `/monet` and immediately know which skill matches their situation.

## What's next

All 8 priority skills are shipped. Next phase is **Phase 4-5 testing** — running each skill against real cases, capturing flaws, tightening prompts. The build process:

1. User runs the skill against 2+ real cases
2. Pastes outputs to chat
3. We identify what's wrong (voice, generic content, missing edge cases, hallucinations)
4. Tighten prompts
5. Repeat until 3 consecutive good runs per skill

Per-skill testing priority (matches creation priority):
1. `triage-inbound-deals` — quickest to test, smallest scope
2. `summarize-pending-work-this-week` — needs full Cowork session with connectors
3. `prep-for-first-founder-call` — easy to test if user has an upcoming founder meeting
4. `run-full-diligence-on-company` — slow per-run, but high signal
5. `write-investment-memo-for-deal` — pairs with diligence
6. `gather-references-on-founder` — only meaningful with real network connections
7. `draft-warm-intro-for-portco` — needs portco intro request to test
8. `write-quarterly-lp-letter` — quarterly cadence, lower urgency

Future skills (see `docs/build-plan.md` full catalog) ship only after the priority 8 are stable:
- `source-new-deals-by-thesis` — proactive sourcing (lower priority — nobody really asks for AI to do this yet)
- `share-deal-with-peer-gps` — deal-share emails
- `analyze-market-for-deal`, `find-competitors-for-deal` — currently bundled into diligence; can split out
- `prep-for-portfolio-1on1-call`, `prep-for-board-meeting`, `parse-founder-update-into-kpis` — portfolio support
- `prep-for-lp-1on1-call`, `draft-capital-call-notice`, `draft-annual-fund-report` — LP comms
- `draft-pass-email-to-founder` — currently bundled into triage; can split
- `review-active-deal-pipeline`, `review-term-sheet-for-redflags` — operations

## Build process — five phases per skill

To prevent stacking unverified versions on top of each other:

1. **Job-to-be-done** — workflow research, JTBD doc at `docs/skills/<name>.md`
2. **Design** — propose flow in chat; user signs off; no code yet
3. **Build** — write SKILL.md + references; tag a version
4. **Test** — user runs with 2+ real cases; we capture flaws
5. **Tighten** — iterate prompts. Move to next skill only after 3 consecutive good runs.

## Patterns learned from official Anthropic plugins

The `productivity` plugin (in `anthropics/knowledge-work-plugins`) is the canonical reference for state-bearing Cowork skills. Key conventions:

- **Working-directory file persistence is for project-scoped state** (productivity's `TASKS.md`). For user-scoped state like a fund profile, use `~/.dotdir/`.
- **Connector detection via MCP prefix.** Skills check whether `mcp__*Gmail*` etc. exist in the session and degrade gracefully when missing.
- **`AskUserQuestion` for structured Q&A.** Always include Skip and free-text. Never fabricate when user skips.
- **Progressive disclosure.** Lean SKILL.md (<3k words), detailed schemas/templates in `references/`.
- **Imperative tone in skill bodies.** "Parse the config," not "you should parse the config." Skill bodies are instructions FOR Claude.
- **Plain language in user-facing turns.** Never expose file paths, schemas, MCP terminology to the user unless they ask.
- **`${CLAUDE_PLUGIN_ROOT}`** for shipped template paths. Never hardcode.

## Surprising findings from research

Five things to keep in mind when designing skills (from `docs/research/solo-gp-workflows.md`):

1. **The "no" email is strategically critical.** Solo GPs get judged by their no-quality.
2. **GPs want 80% drafts in their voice, not full autonomy.** Voice fidelity is the killer feature.
3. **The CRM is a graveyard.** Don't require Attio hygiene. Lean on Gmail + Granola + Drive.
4. **LP letters are creative writing, not templates.** Each GP's letter is brand. Voice clone, don't templatize.
5. **The bottleneck is calendar, not cognition.** Pitch is "give back hours," not "smarter decisions."

## Reference docs

- Full build plan: `docs/build-plan.md`
- Solo GP workflow research: `docs/research/solo-gp-workflows.md` (TODO: commit)
- Per-skill JTBD docs: `docs/skills/<skill>.md` (TODO: created in Phase 1 for each skill)
- Cowork plugin help: https://support.claude.com/en/articles/13837440-use-plugins-in-claude-cowork
- Plugin spec reference: https://code.claude.com/docs/en/plugins-reference
- Official Anthropic plugins: https://github.com/anthropics/knowledge-work-plugins
