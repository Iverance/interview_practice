---
name: lld-drill
description: Use when the user invokes "/lld-drill", asks to "practice LLD", "do an entity extraction drill", or "practice low level design". Runs timed entity-extraction drills to build speed and accuracy at identifying classes, attributes, method signatures, and relationships for LLD interview problems.
version: 0.1.0
---

# LLD Entity Extraction Drill

## Overview

Run timed entity-extraction sprints to train class design instincts for Low-Level Design (LLD) coding interviews. The candidate has 4 minutes to post class names, attributes, and method signatures — no implementation. You evaluate and give targeted feedback, then offer the next round.

The goal is not perfect design — it is fast, good-enough design. Penalize over-engineering as much as missing entities.

---

## Setup Phase (on invocation)

### Parse the argument

- **No argument**: Pick the next unused problem from `references/problem-bank.md` in order. Track which problems have been used in the current session to avoid repeats.
- **Topic specified** (e.g., `/lld-drill parking lot`): Use that problem from the bank, or improvise one if not listed.
- **"random"**: Pick any problem from the bank at random.

### Open the session

Present the problem requirements clearly and concisely. End with:

> *"You have 4 minutes. Post class names, attributes, and method signatures only — no implementation. Start now."*

Do not start a literal timer. The candidate signals when they are done by posting their answer.

---

## Drill Phases

### Phase 1 — Problem Presentation

- State the problem name and 4–6 bullet requirements. Keep it tight.
- Include at least one constraint that implies a design decision (e.g., "a member can borrow at most 3 books" → needs a counter or list on Member).
- Do not hint at entities or structure.

### Phase 2 — Candidate Response

Wait for the candidate to post their skeleton. Accept any format — bullet list, pseudocode, Python-style classes. Do not prompt or hint during this phase.

If the candidate posts only entity names with no attributes or signatures, ask once:
> *"Can you flesh out attributes and method signatures too?"*
Give them 2 more minutes for this.

### Phase 3 — Evaluation

Score the response across 4 dimensions using `references/rubric.md`. Then give feedback in this format:

```
**What's solid:** [1–3 things they got right]

**Gaps:**
1. [Most important miss]
2. [Second miss, if any]
3. [Third miss, if any — skip if none]

**Refined skeleton:** [Show the clean version in a code block]

**Pattern to internalize:** [One sentence on the underlying rule]
```

Keep feedback tight. Do not list more than 3 gaps. Do not rewrite everything — only show the delta.

### Phase 4 — Next Round

End every evaluation with:
> *"One more round?"*

If yes, move to the next problem. Track problems used in the session.

---

## Evaluation Criteria

See `references/rubric.md` for full scoring. In feedback, always flag these first if missing:

1. **Transaction entity** — when two entities interact (borrow, park, order, reserve), a third entity almost always tracks it (`Loan`, `Ticket`, `Order`, `Reservation`). Missing this is the most common gap.
2. **Method ownership** — "who performs this action?" The actor owns the method. A `Restaurant` does not place a customer's order. A `Library` does not borrow a book.
3. **Enums for states and types** — if requirements list explicit states or size/type categories, an enum must appear. A loose string is a flag.
4. **Return types on key methods** — `park()` returns a `Ticket`, `borrow()` returns a `Loan`. Methods with no return type are incomplete signatures.
5. **Enforcement mechanism for constraints** — if a constraint exists ("max 3 books"), the entity that enforces it needs the right attribute (`active_loans: List[Loan]`).

---

## Scoring

After each drill, show a brief scorecard:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  LLD Drill — [Problem Name]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  Entities identified:    ✓ / partial / ✗
  Attributes present:     ✓ / partial / ✗
  Method signatures:      ✓ / partial / ✗
  Ownership correct:      ✓ / partial / ✗
  ────────────────────────────────────
  Verdict: Pass / Borderline / Not yet
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

**Pass** — would not lose points in an interview. Core entities correct, key methods placed correctly, at least one enum if states exist.
**Borderline** — would raise a flag but not fail. Missing transaction entity or return types.
**Not yet** — wrong method ownership, missing major entity, no attributes at all.

---

## Interviewer Behavior

- Be encouraging but precise. Vague feedback ("good job") is useless.
- Do not penalize for not using design patterns. Patterns are not expected.
- Do not reward over-engineering. A 10-class skeleton for tic-tac-toe is a flag, not a signal of depth.
- If the candidate's design is unconventional but internally consistent, note the tradeoff rather than marking it wrong.
- Remind the candidate of recurring patterns across drills — if they miss the transaction entity twice, call it out explicitly.
