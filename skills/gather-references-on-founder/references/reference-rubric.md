# Reference call rubric

Framework for what to ask references and how to synthesize signal across multiple calls. The GP uses this DURING the calls and AFTER to pattern-match.

## Five questions every reference call should answer

These map to the five dimensions of founder evaluation. Skip the generic "tell me about her" — go specific.

### 1. What did they specifically witness?

**Generic:** "What was she like to work with?"
**Better:** "Tell me about a specific project where you saw [founder] do something that surprised you — for better or worse."

You want a concrete event, not abstract praise. "She launched the migration in 6 weeks when we'd estimated 12" is signal. "She's a great leader" is not.

### 2. How did the founder operate when stressed?

**Generic:** "How is she under pressure?"
**Better:** "Walk me through a specific time things were going badly at [Co]. What did [founder] do?"

Stress reveals more than success. The reference's hesitation, specificity, and tone here is diagnostic.

Watch for:
- Did they panic / freeze?
- Did they hide bad news?
- Did they own mistakes or blame the team?
- Did they get more decisive or more indecisive?

### 3. What's the founder's blind spot?

**Generic:** "What are her weaknesses?"
**Better:** "Every great founder has a thing they don't see well. What's [founder's]?"

This is the diagnostic question that separates on-list (friendly) refs from off-list (real signal) refs:
- **On-list refs** will deflect: "honestly, I can't think of one" / "she's pretty self-aware"
- **Off-list refs** will tell you: "she's terrible at delegation" / "he reacts emotionally to investor feedback" / "she sells the dream but doesn't execute the details"

A reference who can't name a blind spot is either lying or doesn't know the founder well. Either way, lower-signal call.

### 4. Would they invest if they had the money?

**Generic:** "Would you back her?"
**Better:** "If you had $1M of personal capital and could put it anywhere, would you put it in [founder's] new company?"

Forces a specific commitment. Watch how they answer:
- "Yes, in a heartbeat" + reasons → strong positive signal
- "Yes, but..." → ask about the "but"
- "I'd want to see [X] first" → tells you what THEY'd diligence
- "I'd pass" or hesitation → STRONG negative signal, dig in

### 5. Anything that surprised them about how this founder thinks?

**Generic:** "What's she like?"
**Better:** "What's something about [founder]'s thinking that surprised you the first time you saw it?"

Looking for: intellectual honesty, contrarian views, specific frameworks, intellectual curiosity. The reference's answer gives you a window into how the founder reasons.

If the reference can't name anything surprising, the founder is conventional. That's not necessarily bad — but it's diagnostic.

## Calibrating questions to founder seniority

### First-time founder
- Heavier weight on questions 2 and 3 (stress + blind spots)
- Add: "How did they handle their first big failure / firing / hard conversation?"
- Add: "Are they coachable?"

### Repeat founder (had at least one prior outcome)
- Heavier weight on question 4 (would you invest)
- Add: "What did they learn from [prior company]?"
- Add: "How did they treat people on the way down at [prior company]?" (if applicable)

### Domain expert turned founder
- Heavier weight on commercial instincts (product/market vs. domain depth)
- Add: "How are they on the parts of company-building outside their expertise?"
- Add: "Have they hired people smarter than them in adjacent functions?"

### Founder with a co-founder dispute history
- Specific question: "What was the dynamic between [founder] and [former co-founder]? What ended it?"
- Listen for: was the founder a difficult partner, or was it a structural / external break?

## Synthesizing signal across multiple calls

After 3-5 reference calls, look for:

### Patterns that show up consistently
- If 4 of 5 references mention the same strength — that's a real strength.
- If 3 of 5 references mention the same blind spot — that's a real blind spot. The founder doesn't see it; you should.

### Patterns that DON'T match the founder's self-narrative
- Founder says "I'm a great delegator." References say "she micromanages." → flag for the GP. Either the founder isn't self-aware, or grew past it.
- Founder says "I learned a lot from [prior failure]." References say "she still does the same thing." → flag.

### Outliers
- One reference giving a very different signal from the rest → ask why. Could be (a) bad blood, (b) only saw the founder in one context, (c) the only one telling the truth.

## Writing reference findings into the memo

In the memo file (`~/.monet/outputs/[company]-memo.md`), reference signal goes in the Founders section. Format:

```markdown
**References called:** [N — list types: e.g. "2 prior co-workers, 1 prior co-founder, 1 customer at prior company"]

**Consistent signal:**
- [pattern that 3+ refs confirmed]
- [pattern that 3+ refs confirmed]

**Off-list-only signal (note: this didn't appear in friendly references):**
- [pattern that only off-list refs surfaced]

**Conflicting signals:**
- [where references disagreed and how to interpret]

**Net assessment from references:**
- [1-2 sentences — does the reference picture confirm, complicate, or contradict the founder's self-narrative?]
```

Keep reference identities confidential. Never name a reference in a memo without their permission.

## What to do if references can't be found

If after the candidate-search step you have <3 plausible references:

1. **Surface to the GP early** — "I only found 2 plausible references. The founder is hard to triangulate from your network."
2. **Suggest expanding search** — ask the GP if they want to use 2nd-degree connections (intros TO refs they don't know directly).
3. **Suggest the founder name more refs** — sometimes the GP's network just doesn't overlap with the founder's history. The on-list references the founder names become more important in that case.

Don't fake it. A weak reference picture should LOOK weak in the memo, so the GP weighs it accordingly.
