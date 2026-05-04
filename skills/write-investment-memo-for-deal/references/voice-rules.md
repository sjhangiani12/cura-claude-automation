# Voice cloning for memos

Voice fidelity is the #1 quality bar. A memo that's 90% accurate but doesn't sound like the GP gets thrown away and re-typed. These rules apply to memo drafting AND to any other long-form skill (`write-quarterly-lp-letter`, `draft-warm-intro-for-portco`, etc.).

## Sources to learn voice from (priority order)

1. **Cura MCP** — if connected, query for the GP's prior investment memos. These are the gold standard.
2. **Drive / Notion** — search for files matching patterns: `*memo*`, `*investment memo*`, `*deal memo*`, `*[company]*memo*`. Pull last 3-5 most recent.
3. **`monet-config.md` voice references** — verbatim samples saved during `/monet:setup`. These are inline reply emails or memo excerpts the GP pasted.
4. **Gmail sent folder** — last 30-90 days of replies to founders. Filter for replies of 2-15 sentences (not one-liners, not full-length memos).

## What to extract from voice samples

Before drafting, scan the samples and note:

- **Sentence length** — short (under 12 words) / medium (12-25) / long (25+)? Mix?
- **Punctuation patterns** — em-dashes liberally? Semicolons? Mostly periods? Paragraph breaks frequent or rare?
- **Structural tics** — do they bullet? Lead with the decision? Open with a one-liner conclusion?
- **Adjective tendency** — are they spare or descriptive? "Strong founder" vs. "10x founder with rare technical taste."
- **Hedging** — do they hedge ("I think", "seems like") or assert ("This works", "She'll win")?
- **VC clichés** — do they use words like "compelling", "exciting", "unique opportunity", "huge market"? Or do they avoid that vocabulary?
- **Profanity / informality** — do they curse in memos? Use "lol" or other casual markers? Match exactly.
- **Opening/closing patterns** — how do they start memos? End them? Match.

## Apply during drafting

- Match sentence length distribution. If the GP writes 80% short sentences, don't generate paragraphs of 30-word constructions.
- Match punctuation cadence. If em-dashes feature in their voice, use them — sparingly and where the GP would.
- Match structural choices. If their memos start with the decision, lead with the decision.
- Match assertion level. If they don't hedge, don't generate hedging language.
- Match vocabulary. If they don't say "compelling," don't say it.

## Hard rules

- **Never insert "VC vocab" not present in the GP's voice samples.** Banned by default unless the GP uses them: *exciting, compelling, unique opportunity, massive TAM, hair on fire, ride the wave, durable moat, asymmetric upside, 10x outcome, generational company, category-defining*. Check generated text for these and replace.
- **Never inflate.** If the founder said "$50K MRR," don't render as "strong $50K MRR traction." Say "$50K MRR." Inflation reads as junior-analyst voice.
- **Never use the word "synergies"** under any circumstances.
- **Never start memos with "I'm excited to share..."** — even if the GP does this in informal contexts, it's wrong for decision memos.
- **Never end memos with "Happy to discuss" or "Let me know your thoughts!"** — that's a pitch deck closer, not a memo closer.
- **Match the GP's level of confidence.** If their voice samples are confident and direct, the memo is confident and direct. If they're more analytical and reserved, the memo is too.

## Voice signals that distinguish the GP from a generic VC LLM

The GP probably:
- Uses lowercase in casual contexts but not in memos (or maybe always — check samples)
- Has a few signature phrases or framings ("the question is...", "the bet is...", "what would have to be true...")
- Has personal references to their portfolio ("reminds me of [portco]", "we've seen this pattern before")
- Uses specific people's names rather than abstractions ("Maya is...", not "the founder is...")
- Has opinions about things adjacent to the deal (the market category, the trend, peer funds)

A generic VC LLM:
- Uses passive voice and abstractions
- Hedges constantly
- Generates lists where the GP would have written prose
- Includes platitudes as filler

When in doubt, lean toward what the GP would actually write — even if it's more opinionated, more specific, or shorter than what feels "complete."

## Test before saving

Re-read the draft against the voice samples. Ask: *would the GP have written this sentence?* For each paragraph, if the answer is "no, they'd phrase it differently," rewrite.

If you've made it through the whole memo and several paragraphs still feel off, ask the user: "I have a draft but voice fidelity feels off in [these sections]. Want me to retry, or should we just edit those manually?"
