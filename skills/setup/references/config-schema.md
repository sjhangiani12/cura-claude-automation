# monet-config.md template

The setup skill writes this file to `~/.monet/monet-config.md` — a user-level location that persists across all Cowork conversations and working directories. Other Monet skills read it from the same path. Keep it readable — the GP should be able to edit it by hand.

**Why `~/.monet/` and not the working directory:** A VC runs setup once but invokes Monet skills from many different Cowork conversations. Storing the config under `~/.monet/` means `/monet:inbound-triage` and `/monet:diligence` work in any conversation without the user having to remember which folder their fund profile lives in.

```markdown
---
schema_version: 1
created: YYYY-MM-DD
updated: YYYY-MM-DD
---

# Monet Fund Profile

## Thesis

[The user's answer to Q1. Paragraph form. Verbatim if they pasted from their website.]

## Sectors

**Priority:**
- [sector]
- [sector]

**Anti:**
- [sector]

## Stage & Check

- **Stage:** [pre-seed / seed / Series A / etc.]
- **Check size:** [range, e.g. $250K–$500K]
- **Position:** [lead / co-lead / follow / mixed]

## Founder Pattern

**Back instantly:**
- [trait or archetype]
- [trait or archetype]

**Pass instantly:**
- [trait or archetype]
- [trait or archetype]

## Voice References

The setup skill stores 2-3 prior reply emails or memo excerpts here, between delimiters. Skills that draft replies or memos read this section and match the style.

<!-- voice-start -->
[verbatim sample 1]
<!-- voice-end -->

<!-- voice-start -->
[verbatim sample 2]
<!-- voice-end -->

## Network

People whose intros carry weight (used when scoring inbound that comes through a warm path):

- **[Name]** — [why; one line]
- **[Name]** — [why; one line]

## Pass Criteria

Hard no's. Anything that trips one of these = automatic PASS, regardless of other signal.

- [criterion]
- [criterion]
```

## Field handling rules (for the setup skill)

- If the user skipped a question, write `_(not specified — re-run /monet:setup to add)_` in that section. Do not invent or pad.
- Voice references go between `<!-- voice-start -->` and `<!-- voice-end -->` delimiters so the inbound-triage and (future) memo-drafting skills can extract them cleanly.
- Stage / check size / position should be parsed from the user's free-text answer into the three sub-bullets. If they only said "pre-seed, $500k checks", leave Position as "_(not specified)_".
- Pass Criteria can be empty for v0.2.0 — the setup skill doesn't ask about it explicitly. Future versions can derive it from the founder pattern Q4 ("pass instantly" list) or add an explicit question.

## Reading conventions (for other skills)

When another Monet skill reads `monet-config.md`:

1. Read the whole file.
2. Extract the relevant sections by H2 heading.
3. For voice: collect everything between `<!-- voice-start -->` and `<!-- voice-end -->` delimiters; concatenate as voice reference material.
4. Treat `_(not specified)_` fields as missing — surface to the user when relevant ("I don't have your founder pattern; my triage will be weaker until you add it via `/monet:setup`").

(Note: schema_version stays at 1; the rename from cura → monet does not bump it because the file format is unchanged.)
5. Check the `updated` date in frontmatter — if older than 90 days, mention it once at the end of the response.
