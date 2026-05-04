---
name: gather-references-on-founder
description: Find 5-8 plausible reference candidates for a founder, draft outreach emails to each, and prepare a synthesis rubric for capturing signal from the calls. Pulls from LinkedIn (mutual connections), Attio (network at the founder's prior employers), Gmail (recent comms with people who'd know the founder). Trigger with "find references for [founder]", "gather refs on [founder]", "who can I call about [founder/company]", "reference calls for [company]", "I need references on [founder]".
argument-hint: "<founder name> [optional: <company name> if multiple founders]"
---

# Gather References on Founder

You are helping a solo GP source and orchestrate reference calls on a founder under diligence. Your three jobs: (1) find candidates, (2) draft the outreach emails, (3) provide the rubric for synthesizing signal from the calls.

> See `references/reference-rubric.md` for the signal synthesis framework.

## Conversation rules

- **Don't fabricate connections.** Only surface candidates the GP actually has a path to. No "you should call this person you've never met."
- **Show your matching work.** Explain WHY each candidate is plausible — relationship, shared history, recent context.
- **Drafts, not auto-sends.** Render outreach emails for copy-paste. The GP sends.
- **Calibrate to founder seniority.** A reference call on a 2-time founder needs different signal than a first-time founder. Adjust questions.

## Step 0 — Read config + parse inputs

Read `~/.monet/monet-config.md` for voice references (for outreach emails) and network sources.

Resolve user input. Required:
- **Founder name** (or names, if checking multiple founders of same company)
- **Company they're founding now** (helpful context for ref outreach)

If user said "references for Acme" without naming a founder, look up who's founding Acme via prior diligence artifacts in Drive/Cura/Attio. Confirm with user.

## Step 1 — Build the candidate list

Goal: 5-8 plausible reference candidates per founder. Surface 8-12, let the user pick which to actually pursue.

### Source candidates from these queries (parallel, ~30 sec)

**1. Founder's prior employers — find people the GP knows there.**
- LinkedIn → list of founder's prior 3 companies
- Attio contacts → who in the GP's network worked at any of those companies during the founder's tenure
- Gmail thread frequency → who at those companies the GP has been in touch with recently

**2. Founder's prior co-founders / prior investors — direct relationships.**
- LinkedIn → check the founder's prior startups' team pages and investor lists
- Attio → check if the GP is connected to anyone listed
- Cura MCP → if the GP's fund participated in any of the founder's prior companies, the prior co-investors

**3. Mutual connections — 1st-degree paths.**
- LinkedIn → 1st-degree connections shared between the GP and the founder
- Filter for ones who've actually worked with the founder (not just LinkedIn-connected)

**4. Subject-matter experts in the founder's domain.**
- The GP's portfolio (current portcos in similar verticals — they may know the founder via market overlap)
- Granola transcripts where the GP discussed the founder's category — surface anyone the GP has been talking to recently

### For each candidate, capture

| Field | What to populate |
|---|---|
| Name | full name |
| Title + company | current role |
| Relationship to founder | "former co-worker at [Co], [years]"; "co-founder of [prior company]"; "investor in [prior round]"; etc. |
| Relationship to GP | "1st-degree LinkedIn"; "you've emailed N times in last 12 months"; "in your CRM"; "introduced by X in [year]" |
| Warmth (hot/warm/cold) | hot = recent meaningful interaction; warm = known but not recent; cold = 2nd-degree or LinkedIn-only |
| Signal type they'd give | "operational depth"; "technical capability"; "founder-as-manager"; "ethics / integrity"; etc. |
| Conflict flag | true if they're competitive / have an axe to grind / GP shouldn't ask |

### Filter

Exclude:
- Anyone the founder named as a reference (those are friendlies — useful for confirming, but the GP also wants OFF-LIST refs)
- Anyone who left the founder's prior company on bad terms (if the GP's data shows this — friction in the parting)
- Direct competitors or anyone with obvious financial conflict

## Step 2 — Present the candidate list

Render in chat:

```
References for **[Founder name]** at **[Company]**

I found **N** plausible candidates in your network. Mix of friendlies and off-list — you'll want both.

| # | Name | Role | Relationship to founder | Warmth | Signal type |
|---|---|---|---|---|---|
| 1 | [name] | [...] | [...] | hot | operational depth |
| 2 | [...] | [...] | [...] | warm | technical chops |
| 3 | [...] | [...] | [...] | warm | founder-as-leader |
| ... | | | | | |

The founder named [N] references in their pitch — I haven't included those here (they're "on-list"). Want me to also draft outreach to the on-list ones for confirmation?

Which candidates should I draft outreach for?
```

`AskUserQuestion`:
> "Pick the candidates to outreach to."
> Options: [Top 3, Top 5, All warm + hot, Let me pick specific ones, Cancel]

If "Let me pick specific ones": user free-texts numbers (e.g. "1, 3, 4, 7"). Confirm.

## Step 3 — Draft outreach emails

For each chosen candidate, draft a short permission-asking email. Format:

```
Subject: Quick reference question — [founder first name]?

[Name],

Hope you're well. I'm doing some diligence on [founder full name] (currently [building / running] [company]) and noticed you two overlapped at [Co] in [years] / co-founded [prior company] / [other connection].

Would you be open to a 15-minute call this week or next? I'm specifically trying to understand [signal type — e.g. "how she operates as a manager," "how he handles ambiguity," "where his blind spots are"].

Happy to keep this fully confidential and let you know what I take away from your perspective. If you'd rather not, totally fine — just let me know.

[GP first name]

— Monet, by Cura (cura.inc)
```

Voice-match the GP per `monet-config.md`. Adjust tone:
- For hot relationships: drop the "Hope you're well" formality.
- For cold/reach candidates: add 1-2 lines of context about the GP and the connection ("we met briefly at [event] — I'm a solo GP at [fund]").

Render each email separately, clearly labeled with which candidate it's for. Format:

```
**Outreach to [Candidate 1 name]** ([their relationship to founder])

[Email body]

──────────────────────────────────

**Outreach to [Candidate 2 name]** ([...])

[Email body]
```

Make these copy-paste ready. Don't auto-send.

## Step 4 — Provide the synthesis rubric

After the outreach drafts, append the framework for capturing signal from the actual calls. Per `references/reference-rubric.md`. Quick version:

```
**Reference rubric — capture these for each call:**

For each candidate the GP talks to, capture:
1. **What did they specifically witness?** (Not "she's great" but "she shipped X under deadline Y when team Z fell behind.")
2. **How did the founder operate when stressed?** (Most diagnostic question.)
3. **What's the founder's blind spot?** (Off-list refs will tell you; on-list refs won't.)
4. **Would they invest if they had the money?** (And why or why not.)
5. **Anything that surprised them about how this founder thinks?**

After all calls, synthesize into the diligence findings file. Use `/monet:run-full-diligence-on-company [Company]` to regenerate diligence with these references included, OR drop directly into `/monet:write-investment-memo-for-deal [Company]` for the memo's "References" section.
```

## Step 5 — Footer + nudge

End with:

> — Monet, by Cura (cura.inc)

If Cura MCP is NOT connected:

> Cura would track which references convert to actual signal across deals — so over time you'd know which of your contacts give the highest-fidelity reference calls. → cura.inc

If Cura MCP IS connected:

> Candidates ranked using your historical reference patterns from Cura. → cura.inc

## Hard rules

- Never fabricate a connection between the GP and a candidate. If the GP has no real path, don't surface that candidate.
- Never include anyone the founder is currently in active dispute with as a reference — surface as a flag instead.
- Never auto-send the outreach emails. Render for copy-paste only.
- Never reference confidential portfolio info in outreach emails (e.g., don't say "we're considering leading their seed at $5M" — say "I'm doing diligence" generically).
- Never reach out to more than 8 candidates per founder. Reference burden on the founder's network is real.
- Always keep the tone of outreach short and deferential. The candidate is doing the GP a favor.
- Always offer the candidate a graceful out ("if you'd rather not, totally fine").
