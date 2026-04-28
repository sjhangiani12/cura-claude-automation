# Per-section synthesis directives

When the user picks "Draft from my tools" or "Mix" mode in `/monet:setup`, work through each profile section in this order. For each section: try the highest-priority connected source first, then fall back. Always show the user what you derived AND its source — never present synthesized content as if they typed it.

## Order of synthesis

Run sections in this order — earlier ones often inform later ones.

1. Sectors (informs founder pattern recognition)
2. Stage & check (independent)
3. Network (informs voice if pulling from emails)
4. Voice (uses sent emails + memos)
5. Thesis (often best derived from Drive docs / Cura)
6. Founder pattern (hardest — usually still ask)

## Section 1: Sectors

**Priority order of sources:**

1. **Cura MCP** — query for fund metadata or portfolio. Group portfolio companies by industry/category tag. Top 3 by count = priority sectors. Anti-sectors: ask user, since Cura won't have this explicitly.
2. **Attio MCP** — list portfolio + active pipeline. Group by `industry` or `category` field (whatever Attio's schema calls it). Top 3 by count = priority sectors. For anti-sectors, ask: "I don't see consumer social / crypto / hardware in your portfolio — should those be anti-sectors, or just absent?"
3. **Fallback (manual question):** "Sectors you're actively investing in? Hard nos?"

**Presentation template:**

> **Sectors** (drafted from your [Cura/Attio] portfolio of N companies):
> Priority: [sector 1] (N companies), [sector 2] (N), [sector 3] (N)
> Anti: [tentative — confirm with user]

## Section 2: Stage and check

**Priority order of sources:**

1. **Cura MCP** — historical investments. Compute median check size and most-common round type (pre-seed, seed, A). Lead/follow position from round structure if available.
2. **Attio MCP** — investments table. Same logic: median check, most-common round.
3. **Fallback (manual question):** "Stage, check size, lead/co-lead/follow?"

**Presentation template:**

> **Stage & check** (from your N most recent investments):
> Stage: [pre-seed / seed / A] (N of last N rounds)
> Check size: $XK–$YK (median: $ZK)
> Position: [lead / co-lead / follow] — should I keep this default, or update?

## Section 3: Network

**Priority order of sources:**

1. **Attio MCP** — query contacts ordered by interaction count or deal involvement. Filter to people NOT internal to the fund (no fund-domain emails). Top 5 = network sources.
2. **Gmail / Superhuman MCP** — search sent + received messages from the last 12 months. Count unique external addresses by frequency. Filter out vendors, tools, and obvious noise (LinkedIn, Stripe, etc.). Top 5 = network candidates.
3. **Fallback (manual question):** "Top 3-5 people whose intros carry weight for you?"

**Presentation template:**

> **Network** (drafted from your [Attio contact frequency / Gmail thread count]):
> 1. [Name] — [N threads / N deal involvements]
> 2. [Name] — [...]
> 3. [Name] — [...]
> Want to add anyone, or remove anyone whose intros DON'T carry weight?

## Section 4: Voice

**Priority order of sources:**

1. **Gmail or Superhuman MCP** — search the user's Sent folder for replies to external founders over the last 90 days. Heuristics for "founder reply": sent message that's a reply (Re: prefix or thread depth), to a person not in the user's organization, with reply length 2-15 sentences (not a one-liner, not a long memo). Pull the 5-10 most recent matches. Use these verbatim as voice samples.
2. **Drive or Notion MCP** — search for files matching keywords: "memo," "investment memo," "deal memo," "diligence." Pull top 2-3 most recently updated. Extract 1-2 paragraphs from each as voice samples.
3. **Granola MCP** — pull recent meeting transcripts where the user is the dominant speaker. Extract their statements verbatim.
4. **Fallback (manual question):** "Paste 2-3 prior reply emails or memo excerpts."

**Best result:** combine all available sources for max coverage. Voice is one of the highest-value sections to synthesize because GPs notoriously can't articulate their voice — but their sent folder shows it perfectly.

**Presentation template:**

> **Voice** (drafted from your sent emails + N prior memos):
> I pulled 8 of your recent founder replies and 2 memos as voice samples. They show your style — short, specific, kind on no's. Want to:
> [Use these as-is] [See them and pick which to keep] [Replace with ones I paste]

If user picks "See them and pick": render each sample with a 1-line attribution ("From: reply to founder X, March 2026") and let them keep/discard.

**Privacy note:** When storing voice samples in monet-config.md, redact the founder's name and company from the sample. Replace with `[founder]` and `[company]`. The voice is what matters; the specifics are not.

## Section 5: Thesis

Usually hard to synthesize — most funds keep their thesis in their head or on their website, not in their CRM.

**Priority order of sources:**

1. **Cura MCP** — if a fund metadata field has the thesis, use it directly.
2. **Drive / Notion MCP** — search for files: "thesis," "fund overview," "memo template," "investment thesis." Pull top result; extract the thesis section (usually first 1-2 paragraphs of the doc).
3. **Web** — if the user mentioned their fund name during setup OR if the fund domain can be inferred from their email, search for the fund's website and pull the thesis from the about page. Use cautiously — confirm the source URL with the user.
4. **Fallback (manual question):** "What's your fund's thesis? Paste from your website, or 1-2 sentences."

**Presentation template:**

> **Thesis** (drafted from [your Drive doc 'Fund Memo Template' / your fund's website at example.vc]):
> "[verbatim 1-2 sentences from source]"
> Use this, edit, or replace?

## Section 6: Founder pattern

**Hardest section to synthesize.** Founder pattern is what makes triage useful, but it's tacit — GPs know it when they see it but rarely write it down. Be honest about the limits.

**Priority order of sources:**

1. **Cura MCP** — if Cura tracks past yes/no decisions, query for last 50 founders backed and 50 passed. Look for common traits: prior company outcomes, technical/non-technical, repeat founder vs. first-time, university clusters, etc. Generate 3-5 candidate "back instantly" and "pass instantly" traits. **Mark these as low-confidence pattern guesses — always ask the user to confirm.**
2. **Attio MCP** — same logic if Attio tracks decisions and has founder profile fields.
3. **Fallback (manual question — recommended in almost all cases):** "Founders you'd back instantly (traits, archetypes), and founders you'd pass on instantly. Be specific."

**Presentation template (when synthesizing):**

> **Founder pattern** (tentatively derived from your last N decisions in [Cura/Attio]):
> Back-instantly traits I noticed:
> - Repeat founders with technical depth (8 of 12 yes-decisions)
> - Sub-30 founders building dev tools (6 of 12)
> Pass-instantly traits:
> - "AI for X" with no model differentiation (4 of 8 no-decisions cited this)
>
> This is a pattern guess — what would YOU say is the actual pattern? (My guess might be missing the gut signal.)

Always defer to the user on this one. Synthesis is a starting point, not the answer.

## Section 7 (optional): Pass criteria

For v0.4.0, do not auto-derive pass criteria. Just ask: "Any explicit hard nos beyond the anti-sectors? (e.g. 'no founders without technical co-founder', 'no companies pre-revenue', etc.)" Skip is fine.

In future versions, Cura MCP could surface this from past pass decisions ("you passed on 12 companies in the last 6 months citing 'no technical co-founder' as the reason — should that be a pass criterion?").

## Heuristics for "good enough" synthesis

- **Confidence threshold:** if you can derive a section from at least N=5 data points, present it. If less than 5, fall back to asking.
- **Anti-data:** absence of evidence isn't evidence of absence. If the user has 8 portfolio companies in AI infra and zero in consumer social, that means consumer social is *probably* an anti-sector — but ASK before saving it as one. They might just not have invested in consumer social yet for unrelated reasons.
- **Time decay:** for any source, prefer the last 12 months over older data. A fund's pattern can shift dramatically year-over-year.
- **Honesty over polish:** if a section is weak, say so. "I tried to derive your founder pattern from past decisions but the signal was noisy — let's just have you tell me." Better than presenting a wrong synthesis confidently.

## What synthesis should NOT do

- Never call MCP tools the user didn't authorize the plugin to use. If a connector is present but the user said "skip," do not query it.
- Never store raw queried data in `monet-config.md` (e.g. don't paste 8 emails verbatim). Store *derived* signals (voice samples, sector list, network names) — not the raw source data.
- Never present synthesized content as the user's words. Always attribute the source.
- Never block on a connector that returns an error. If Attio is connected but the query fails, fall back to the manual question for that section. Note the error briefly: "Attio query failed; let me just ask you directly."
