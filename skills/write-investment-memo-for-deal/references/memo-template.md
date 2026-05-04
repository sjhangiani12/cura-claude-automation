# Investment memo template

Default structure. Adapt to the GP's voice and prior-memo style. If the GP's prior memos use a different structure entirely (e.g. they always lead with founder, not thesis), override this template.

## Full memo (~2000-3000 words)

```markdown
# [Company Name] — Investment Memo

**Stage:** [pre-seed / seed / A]
**Round:** [round size, valuation if disclosed]
**Our check:** [proposed check size]
**Position:** [lead / co-lead / follow]
**Recommendation:** [INVEST / PASS / TRACK]
**Date:** [YYYY-MM-DD]

---

## 1. The decision in one paragraph

[2-4 sentences. State the recommendation, the single strongest reason for it, and the single biggest risk. The reader should be able to stop after this paragraph and know what you think.]

## 2. Why this fits our thesis

[Reference the fund thesis from monet-config.md by name. Be specific about WHY this maps — not "this is in our sector" but "this addresses [specific thesis hook] by [specific company action]." Cite the founder's own framing where it overlaps with the thesis.]

## 3. The company

[What they do, in 2-3 sentences. Target customer, wedge, current traction. Cite source: "per the deck dated April 12" or "from founder call April 14".]

**Traction (verified):**
- [metric: number, source]
- [metric: number, source]

**Traction (claimed but unverified):**
- [metric: number, mark as `[GAP — verify]`]

## 4. The founders

[For each founder: 2-3 sentences. Background, prior outcomes, why this problem. Reference the user's founder pattern from monet-config.md: which back-instantly traits do they hit? Which pass-instantly traits, if any?]

[If references called: synthesize signal here. Format: "Per [reference name, relationship to founder]: [verbatim or paraphrased signal]." Keep references confidential — never name an off-list reference without permission.]

## 5. Market

[TAM / SAM / SOM with sources. Cite Crunchbase, public reports, founder claims separately.]

[If a comparable round/exit exists in the GP's portfolio or peer fund's portfolio, mention it here. ("Peer fund X led [comparable] at $YM seed; exited at $ZM in 2024.")]

## 6. Competitive landscape

[3-5 named competitors. Per competitor: who they are, what they do, why this company is different / why not. Be honest — don't strawman competitors.]

[Note any "white space" claims the founder made — and whether they hold up.]

## 7. Risks

[List 3-5 risks, ranked by severity. For each: what is it, and what would have to be true for the risk to NOT bite. The GP scans this section before deciding.]

[Specifically address any pass-instantly traits from the GP's founder pattern that this founder shows. Don't bury them.]

## 8. Terms

[Round size, valuation, instrument (SAFE / priced / convertible), pro-rata, board observer, info rights. Anything unusual flagged.]

## 9. What I'd want to see before increasing conviction

[2-4 specific things. "Hit $50K MRR by July." "Land 2 more enterprise pilots in dev tools." "Hire a VP Eng before close." Concrete, time-bound, falsifiable.]

## 10. Decision rationale

[Final 2-3 paragraphs. Why this is a YES (or PASS, or TRACK). Tie back to the thesis. Acknowledge the strongest counter-argument. End with the action: "Sending term sheet" / "Passing — see draft email" / "Will revisit in 60 days."]

---

**Sources used:**
- [list of artifacts cited above with dates]

**Gaps remaining:**
- [list of `[GAP]` markers in the memo with what would close them]
```

## One-page version (~500-800 words)

For when the GP needs the gist, not the full workup. Skip sections 5, 6, 7 detail and compress.

```markdown
# [Company] — Memo (one-pager)

**Recommendation:** [INVEST / PASS / TRACK] | [check size] | [stage]

## What
[1-2 sentences: what they do, traction snapshot]

## Why we'd back them
[3-4 bullets: thesis fit, founder strength, market timing, competitive edge]

## Why we might not
[2-3 bullets: biggest risks]

## What we'd want before increasing conviction
[2-3 bullets: specific milestones]

## Decision
[2 sentences: final call + next step]

---
Sources: [list]
```

## Voice adaptation rules

- If the GP's prior memos use ALL CAPS section headers, match that.
- If they use em-dashes liberally (— like this), match.
- If they bullet-point heavily, match. If they write in flowing prose, do that.
- Default to the structure above ONLY if no prior memos exist to learn from.

## What NOT to do

- Don't include an "executive summary" as a separate section if the "decision in one paragraph" is already up top. Redundant.
- Don't put TAM/SAM/SOM before the founder section — that's a pitch deck order, not a decision memo order.
- Don't add a "Q&A" or "FAQ" section. If a question matters, it's in the memo. If not, it's noise.
- Don't include weasel words ("potentially," "could be," "may have"). The GP either thinks something or they don't.
