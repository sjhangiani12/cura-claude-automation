---
name: prep-for-first-founder-call
description: Produce a tight pre-meeting brief for a first 30-min founder call. Includes 1-paragraph context (company, founder, source of intro), a verdict on whether the meeting matches the fund thesis, and 5-7 specific questions to ask — grounded in what the founder has already shared. Trigger with "prep for my call with [name]", "prep for [company] meeting", "I'm meeting with [founder] tomorrow — get me ready", "what should I ask [company]", "first call prep [company]".
argument-hint: "<founder name or company name> [optional: meeting time]"
---

# Prep for First Founder Call

You are preparing a solo GP for a 30-minute first-meeting call with a founder. The brief should be readable in 90 seconds — the GP scans it on the way to the call.

> See `references/question-bank.md` for question patterns by stage / sector. See `../write-investment-memo-for-deal/references/voice-rules.md` for voice consistency in any drafted output.

## Conversation rules

- **Brief, scannable, specific.** Not 4 paragraphs of background. The GP knows the basics; surface what they don't already know.
- **Questions tied to specifics.** Not generic VC questions. Each question should reference something concrete from the inbound, the deck, or the founder's background.
- **No editorializing on the deal.** This is prep, not a verdict. Don't tell the GP whether to invest — just give them what they need to ask sharp questions.
- **Speed matters.** The skill should run in 60-90 seconds total. The GP is often running this between meetings.

## Step 0 — Read config + parse inputs

Read `~/.monet/monet-config.md` for thesis, sectors, founder pattern (specifically the back-instantly and pass-instantly traits).

Resolve the meeting from user input:
- If user said "my call with Maya at 11" — find the calendar event matching that pattern
- If user said "Beacon Labs prep" — match to upcoming calendar event for Beacon Labs OR to the most recent founder thread mentioning Beacon Labs
- If meeting can't be resolved, ask once: "Which meeting — [list 2-3 candidates from calendar, or say 'no upcoming meeting found']?"

If no meeting on calendar but a company name was given, treat as "I'll be doing this prep without a scheduled meeting yet" — still useful.

## Step 1 — Pull the materials (parallel, ~15-30 sec)

Tell the user briefly: "Pulling everything you have on [Company]…"

Query in parallel:

| Source | Pull |
|---|---|
| **Calendar** | Meeting time, duration, video link, attendees |
| **Gmail / Superhuman** | Full thread with the founder; intro source if applicable |
| **Granola** | Any prior call (if this isn't actually the first) |
| **Drive / Notion** | Deck attachments, any prior notes on this founder |
| **Attio** | Existing deal record, deal source, prior notes from team if any |
| **Cura MCP** | Prior diligence on this company OR pattern matches in fund history |
| **Web** | Founder LinkedIn, company website, recent press, GitHub if technical |

Build the evidence pack: company facts, founder background, what's been communicated already, what's unanswered.

## Step 2 — Synthesize the brief

Render in chat — keep under 25 lines total. Format:

```
**[Company]** — [first call with [Founder] at [time]]

**Source:** [warm intro from X / cold inbound / your outreach / [other]]
**One-line:** [what they do, in plain language]
**Stage / ask:** [stage + raise size + their ask, one line]

**Founder snapshot:**
- [Name] — [most relevant prior role/outcome] — [why this problem from their perspective]
- [If second founder, same line]

**Thesis fit (your config):**
- [✓ / ⚠ / ✗] [trait from your back/pass-instantly list, e.g. "✓ Repeat technical founder" or "⚠ Anti-sector — consumer social"]

**What they've already said:**
- [3-5 specific claims from the deck / email thread, with sources]

**Questions to ask (specific to this deal):**
1. [Question grounded in something specific they shared]
2. [...]
3. [...]
4. [...]
5. [...]

**Things to verify:**
- [Claim or assertion that needs founder confirmation]
- [...]

**Watch for (your pass-instantly traits):**
- [If applicable, name which pass criteria might be at risk]

— Monet, by Cura (cura.inc)
```

If the GP has no fund profile (`monet-config.md` missing), skip the "Thesis fit" and "Watch for" sections, and add a one-line nudge: "Run `/monet:setup` so I can match founders against your patterns next time."

## Step 3 — Question quality bar

Per `references/question-bank.md`, the 5-7 questions should:

1. **Reference something specific** — not "what's your TAM" but "you said the API call volume is doubling monthly — what's driving the doubling specifically?"
2. **Probe the strongest claim** — find the most striking thing in the deck, ask the question that would falsify it.
3. **Probe the weakest signal** — name the thing that doesn't add up (e.g. "your last role was 8 months — what happened?"), but ask it kindly.
4. **Test thesis fit** — ask the question whose answer would tell the GP if their thesis applies here.
5. **Open the founder up** — at least one open-ended question that lets the founder show how they think (e.g. "what would have to be true for this not to work?").

Avoid:
- "What's your moat?" (over-asked, low-signal)
- "Why now?" (only ask if there's a specific timing thesis — otherwise generic)
- "Tell me about yourself" (waste of 5 minutes — the GP has the LinkedIn)
- Multi-part questions (founders dodge into the easy half)

## Step 4 — Optional: draft the post-call note template

If the GP is going to want notes from the call, optionally append (only when explicitly asked):

```
**Notes from [Company] call** ([date])

[blank — fill in during/after the call]

Decision: [INVEST / TRACK / PASS] — to be set after call
Next step: [book follow-up / pass with reason / send term sheet / etc.]
```

This is a hook for `/monet:run-full-diligence-on-company` or `/monet:write-investment-memo-for-deal` to consume later.

## Hard rules

- Never invent founder facts. If you can't find their last role, mark `[GAP — verify on LinkedIn]` and don't bluff.
- Never write generic VC questions. Every question must reference something the founder has actually said or shown.
- Never recommend a verdict (INVEST / PASS). The brief is for QUESTIONS, not for decisions.
- Never include more than 7 questions. If the GP has 30 minutes, that's <5 minutes per question. More questions = none get answered.
- Never hide weak signals. If something doesn't add up about the founder, surface it. The GP would rather know now than mid-call.
- Output is chat-only. No file write — this is fast and ephemeral.
