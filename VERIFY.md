# Verify: Support ticket bot that reopens the original failure instead of answering the last reply

## What this file checks

A stranger can run their own ticket-reopen setup through the auditor and confirm it surfaces the deciding check with a numeric measurement.

---

## Stranger verification steps

### 1. Open /play with your own failing setup

Describe a ticket bot (or similar routing tool) that should link follow-ups to original tickets but sometimes opens new ones instead.

Provide:
- What the tool is supposed to do
- Who gets hurt when it fails
- Three real messages where it misfires

### 2. Walk the five checks

The auditor will ask about each check in turn. Answer with your own setup's behavior.

### 3. Confirm the deciding-check finding

The tool must surface which check is the weakest link for your setup.

For the builder's specimen, the deciding check was **unowned** — the matching step had no assigned owner.

Your audit should name your own deciding check clearly.

### 4. Demand a numeric measurement

Every finding the auditor proposes must name the measurement that would confirm it.

Example from the builder's audit:
> Watch engineer double-work reports — cases where two people are assigned the same underlying bug because of a missed reopen. If this hits 2+ per week, Priya escalates.

Your audit must include:
- A number (e.g., "2+ per week")
- A danger line (what that number means)
- A watcher (who monitors it)

If the auditor returns a finding without a numeric threshold, the verification fails.

---

## Pass criteria

| Check | Pass |
|-------|------|
| Auditor walks all five checks for your setup | ☐ |
| Deciding check is named explicitly | ☐ |
| Each finding includes a measurement that would confirm it | ☐ |
| Final call includes owner on any condition | ☐ |
| Tripwire includes a number, danger line, and watcher | ☐ |

---

## Builder's worked example (reference)

**Specimen:** Support ticket bot that reopens the original failure instead of answering the last reply

**Deciding check:** unowned

**Tripwire:** Watch engineer double-work reports — cases where two people are assigned the same underlying bug because of a missed reopen. If this hits 2+ per week, Priya escalates, since it directly reflects the unassigned matching gap.

**Call:** Ship for tickets under 24 hours old (low risk of an unmatched reopen), hold for anything referencing "yesterday," "Tuesday," or "again" until ownership of the matching step is assigned. Priya reviews and reassigns by end of week.

Your audit should follow the same structure, grounded in your own setup's failures.