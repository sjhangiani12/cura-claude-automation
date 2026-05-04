# Intro matching and email rules

## Ranking heuristics

Score each candidate on three dimensions, then combine:

### Warmth (0-3)

- **3 — Hot.** Active back-and-forth in last 90 days OR met in person in last 90 days OR they're in the GP's CLAUDE.md memory as a current contact.
- **2 — Warm.** Known well, comms in last 12 months, would respond to a forward without re-intro.
- **1 — Reach.** Real connection, but stale (last touch 1+ years). Needs a permission ping before forwarding.
- **0 — Cold.** Single interaction, low context, or a 2nd-degree contact via someone else. Generally don't draft intros at this level.

### Relevance (0-3)

- **3 — Bullseye.** This person specifically does the thing the portco wants (e.g. they're literally a Head of RevOps at a company in the portco's target ICP).
- **2 — Adjacent.** Similar function or similar context (e.g. they're VP Sales at a sector-adjacent company).
- **1 — Plausible.** Could plausibly help via their network even if they're not the direct match.
- **0 — Stretch.** Don't recommend.

### Conflict (0 or -3)

- **0 — No conflict.** They can engage with the portco without issue.
- **-3 — Conflict.** They're at a directly competing company, OR they're in active diligence on the portco from a competing fund, OR they're a portco founder being asked to advise a different portco (potentially fine, but flag).

### Combined score

`Warmth + Relevance + Conflict ≥ 4` → recommend. Lower → don't surface unless asked.

## Tier presentation

Show in this order:
1. Hot + Bullseye (most likely to convert)
2. Warm + Bullseye
3. Hot + Adjacent
4. Reach + Bullseye (worth the permission ping)

Don't show more than 5 candidates. The GP is making a quick decision.

## Email format rules

### Subject line

Pattern: `Intro: [portco founder first+last name] @ [portco] <> [candidate first name]`

Example: `Intro: Maya Chen @ Beacon Labs <> Carson`

Keep under 60 characters. Don't use em-dashes in the subject (mail clients render them weirdly).

### Body structure

1. **Greeting** — first name only.
2. **Frame the intro** — one sentence: "Want to make an intro to [name], who's [doing thing]."
3. **The portco hook** — one sentence on what the portco does + the most credible piece of traction or context.
4. **The ask** — one sentence on what the portco wants from the candidate.
5. **The "why you"** — one sentence on why the GP thought of THIS candidate specifically. This is the differentiator that turns generic intros into accepted ones.
6. **The double opt-in close** — "if you're up for it I'll connect you directly. [Portco founder] BCC'd."
7. **Signoff** — first name, GP's normal style.

### What NOT to put in an intro email

- Don't include the portco's pitch deck. The candidate gets curious by your description, not by a PDF.
- Don't include financials, ARR numbers, or sensitive metrics. Keep them as "early traction" or "recently launched" unless the GP explicitly says to include numbers.
- Don't oversell ("incredible founder", "rocket ship", "category-defining"). The candidate will ignore the email if it sounds like a pitch.
- Don't make multiple asks. One intro = one ask.
- Don't include long bios. The candidate will Google the founder if they're interested.

### Voice patterns

Match the GP's voice samples. But default tendencies for intro emails:

- Shorter than memos (4-6 sentences total in the body).
- More casual than memos.
- Specific reasons over generic praise.
- Lead with the action (the intro), not a wind-up.

Examples of intro openers a GP might use (study their voice samples for which fits):

- "Want to make an intro to..." (direct)
- "Quick one — meet [name]..." (casual, brief)
- "I'd love to connect you with..." (warmer)
- "Worth a fast intro — [name] is..." (energy + brevity)

## When to send a permission ping vs. skip it

**Always permission-ping if:**
- Last touch with the candidate was >180 days ago.
- The candidate is in a senior-time-pressed role (CEO of a public company, partner at a major fund) — they need control over their inbox.
- The portco's ask involves money flow (raise, customer pilot at >$100K ACV, M&A) — these get permission-pinged universally.

**Can skip permission ping if:**
- The candidate has explicitly told the GP "always intro people to me."
- The GP has made multiple intros to this candidate in the last 6 months without conflict.
- The candidate is a peer-fund GP / friend who's casual about intros.

When in doubt, default to permission-ping. The cost of asking is one extra email; the cost of an unwelcome forward is reputation.

## Tracking (when Cura MCP is connected)

If Cura MCP is connected, log each drafted intro:
- Portco asking
- Candidate
- Date drafted
- Outcome (after the GP sends, Cura observes whether the thread converts)

This is what makes Cura's intro-stack get smarter over time — patterns of which candidates accept, which decline, which lead to actual conversions for portcos. Plugin alone can't track this; that's the upgrade.
