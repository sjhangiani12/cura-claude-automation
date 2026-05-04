# Per-stage diligence directives

Run stages in order. Each builds on the prior. Don't run later stages if earlier ones surface a deal-breaker.

## Stage 1 — Company profile

**Goal:** establish the basic facts.

**Pull from:**
- Founder's deck (Drive / email attachments) for claimed metrics
- Crunchbase / Pitchbook / company website for confirmed funding history
- Company website for product description, customers if listed
- LinkedIn for team size and recent hires
- Public press for recent announcements

**Extract:**
- Company name, founding year, headquarters, team size
- One-sentence product description (use the founder's framing)
- Stage and funding history (rounds, dates, leads, valuations if disclosed)
- Customer wedge (who buys, why now)
- Public traction metrics (users, ARR, growth rate) — separate verified from claimed

**Output format:**
```
## 1. Company profile

**Name:** [name]
**Founded:** [year]
**Stage:** [stage]
**Team:** [N] (from LinkedIn, [date])
**HQ:** [location]

**What they do:**
[1-2 sentences in plain language. Avoid the company's own marketing copy.]

**Funding history:**
| Round | Date | Lead | Amount | Valuation |
|---|---|---|---|---|
| [...] | [...] | [...] | [...] | [...] |
Sources: [Crunchbase URL, press release URL, founder claim]

**Traction (verified):**
- [metric, source, date]

**Traction (claimed but unverified):**
- [metric, marked `[GAP — verify with founder]`]
```

**Stop conditions:** if you can't even establish what the company does after 2 minutes of search, the deck is too thin or the company doesn't exist publicly. Surface this and ask the user for the deck or website link.

## Stage 2 — Founder backgrounds

**Goal:** understand who is building this and whether they match the GP's founder pattern.

**Pull from:**
- LinkedIn (each founder)
- Cura MCP (any history with this founder, prior deals reviewed)
- Attio contacts (mutual connections, prior interactions)
- Gmail (any prior threads with the founder)
- Web (founder's public writing, podcast appearances, GitHub)

**Extract per founder:**
- Full name, current role, age (rough — only if relevant)
- Career arc (last 3-4 roles, dates)
- Prior outcomes (companies they founded, exits, failures)
- Technical / operational depth (do they ship code? Run sales? Both?)
- Why this problem (their stated motivation, plus any independent signal)
- Mutual network (who in the GP's network knows them)

**Cross-reference against `monet-config.md`:**
- Which "back-instantly" traits do they hit?
- Which "pass-instantly" traits, if any?

**Output format:**
```
## 2. Founders

### [Founder name 1] — [role]

**Career:**
- [Most recent: title, company, dates]
- [Prior: title, company, dates]
- [...]

**Prior outcomes:**
- [Company X: founded [year], outcome [exit / shutdown / still going], notes]

**Why this problem:** [from their own framing — quote source]

**Pattern match (vs your back-instantly traits):**
- ✓ [trait they hit]
- ✓ [trait they hit]
- ✗ [trait they don't hit]
- ⚠ [pass-instantly trait they show — flag prominently]

**Mutual network in the GP's contacts:**
- [Name, relationship: e.g. "ex-coworker at Stripe 2018-2020"]
- [...]

[Repeat for each founder]
```

## Stage 3 — Market

**Goal:** size the opportunity and place this company in market trends.

**Pull from:**
- Cura / prior memos in fund history (have we sized this market before?)
- Public reports (Gartner, IDC, public S-1s of comps if any)
- Crunchbase comparable rounds in the category
- Web (recent press, trend articles, peer-fund posts on the category)

**Extract:**
- TAM / SAM / SOM with credible sources (skeptical of founder-deck numbers)
- Top 3 trends shaping the category (with dates and sources)
- Comparable rounds in the last 18 months (similar stage, similar wedge): name, lead, amount, valuation
- If any comps have exited or scaled meaningfully, note them

**Output format:**
```
## 3. Market

**TAM:** $[X]B by [year], per [source]
**SAM (this company's wedge):** $[X]B, per [source / triangulation]
**SOM (5-year capture):** $[X]M reasonable, $[X]M optimistic — assumptions: [list]

**Recent comparable rounds:**
| Company | Stage | Date | Lead | Amount | Valuation |
|---|---|---|---|---|---|
| [...] | [...] | [...] | [...] | [...] | [...] |

**Trend signals:**
- [trend, source, date]
- [trend, source, date]

**What would change the market in the next 24 months:**
- [factor + how it'd change the bet]
```

## Stage 4 — Competitive landscape

**Goal:** name the competitors honestly. Don't strawman.

**Pull from:**
- Founder's own competitor list in the deck (starting point, not endpoint)
- Crunchbase category page
- Web search for "[category] companies" / "[wedge] alternatives"
- G2 / Product Hunt for direct user-facing competitors
- The GP's network (Attio + Granola transcripts mentioning competitors)

**Extract per competitor:**
- Name, what they do, stage, last funding
- How they're positioned vs. this company
- Whether they share customers / are commonly considered together

**Don't:**
- Cite only competitors the founder named (the deck almost always misses the strongest ones)
- Frame all competitors as "weaker" — be honest about who's actually stronger

**Output format:**
```
## 4. Competitive landscape

### Direct competitors (same wedge, same buyer)
| Company | Stage | Funding | Positioning vs. [target] |
|---|---|---|---|
| [...] | [...] | [...] | [...] |

### Adjacent competitors (overlapping use case)
| Company | Stage | Funding | Overlap |
|---|---|---|---|
| [...] | [...] | [...] | [...] |

### Why this company can win (claimed):
- [claim from founder]
- [claim from founder]

### Why those claims might not hold:
- [counter from market evidence]
- [counter from market evidence]

### White space the founder claims:
[summary] — supported by [evidence] OR challenged by [evidence]
```

## Stage 5 — Risks

**Goal:** name the things that could kill this. Specifically address pass-criteria from config.

**Pull from:**
- Everything gathered in stages 1-4
- The GP's `pass criteria` from `monet-config.md`
- Cura prior pass decisions (what kills deals like this in this fund's history)

**Categories:**
1. **Market risk** — does the market exist at this size? Is the timing right?
2. **Team risk** — gaps in skills, missing co-founder, founder-market fit weak?
3. **Execution risk** — can this team build this thing? GTM strategy realistic?
4. **Competitive risk** — are bigger / better-funded players going to crush them?
5. **Timing risk** — too early? Too late? Cycle risk?
6. **Anti-thesis risk** — does the deal trip any of the GP's explicit `pass criteria`?

**Output format:**
```
## 5. Risks

### Top 3 (rank-ordered by severity)

**1. [Risk title]**
- What it is: [1-2 sentences]
- Why it matters: [tied to fund size, stage, GP's pattern]
- What would have to be true for this NOT to bite: [specific, testable]

**2. [Risk title]**
[same format]

**3. [Risk title]**
[same format]

### Pass-criteria check
| Pass criterion (from config) | Status |
|---|---|
| [criterion] | ✓ not tripped / ⚠ at risk / ✗ tripped |

### Other risks (lower severity, noted for the record)
- [...]
```

## Stage 6 — Reference signals (optional, runs only if connectors support)

**Goal:** identify 3-5 plausible reference candidates and surface enough signal to decide who to actually call.

**Pull from:**
- Attio contacts who worked at the founder's prior companies
- LinkedIn connections (if accessible) at the founder's prior employers
- Gmail thread frequency to identify mutual close ties

**Don't:**
- Actually contact references — that's `/monet:gather-references-on-founder`
- Render anyone the GP has already pinged about this deal (avoid double-tap)

**Output format:**
```
## 6. Reference candidates

[3-5 candidates per founder, with relationship to founder + relationship to GP]

| Candidate | Relationship to founder | Relationship to GP | Strength |
|---|---|---|---|
| [name] | Worked together at [Co], [years] | [direct / 1-degree / 2-degree] | [hot / warm / cold] |

→ Run `/monet:gather-references-on-founder [founder name]` to draft outreach.
```

## Stop early if deal-breakers surface

If during stages 1-3 you find a clear deal-breaker (e.g. founder is currently in litigation, company is in an explicitly anti-sector), surface it and ask:

> Found a likely deal-breaker: [issue]. Continue full diligence anyway, or stop here?

Save what you have either way. Don't silently waste the GP's time.
