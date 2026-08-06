# Support ticket bot that reopens the original failure instead of answering the last reply

## What this auditor does

A conversational auditor that walks five checks on any ticket-routing bot that struggles to match reopens to original tickets. A stranger describes their failing setup, pastes real failing messages, and receives a scored audit with findings, a call, and a tripwire.

---

## The problem being audited

**Specimen:** Support ticket bot that reopens the original failure instead of answering the last reply

**What goes wrong if this never gets fixed:** Wrong person gets the ticket; the real bug waits another day

**How you know it's fixed:** A reopen lands on the original ticket, not a new one about the side comment

**Real input conditions:** Busy support chat; short replies; lots of "it / that / again"

---

## Worked example: failing messages from this build

Source: Live support tickets from this week

```
thanks for the update on the payment page — that's fine, but the thing I originally wrote about is still broken
```

```
it happened again this morning on the invoice export
```

```
can you link this to #44821 instead of opening a new ticket
```

---

## The five checks

Walk each check in order. For every finding, name the measurement that would confirm it.

### 1. Unowned
**Rating:** 4 (critical gap)

Does the matching step have a clear owner? Who is responsible when a reopen fails to link?

*Measurement:* Name the person or role assigned to review unmatched reopens. If no one is assigned, this check fails.

### 2. Copies
**Rating:** 2

Are there duplicate tickets being created for the same underlying issue? How many times per week does the bot open a new ticket when it should have matched an existing one?

*Measurement:* Count of duplicate tickets created in the last 7 days where the customer explicitly referenced an existing issue.

### 3. Room
**Rating:** 2

Does the bot have enough context window or history access to find the original ticket? Can it see tickets older than 24 hours?

*Measurement:* Maximum ticket age (in hours) the bot can search when matching. Note any cutoffs.

### 4. Stitch
**Rating:** 1

When the customer references a prior conversation ("the thing I originally wrote about"), can the bot connect that reference to a specific ticket ID?

*Measurement:* Percentage of pronoun/reference phrases ("it," "that," "again") that successfully resolve to a prior ticket.

### 5. Ablation
**Rating:** 1

If you removed the matching logic entirely, would anyone notice? Is the matching step actually being used, or is it bypassed?

*Measurement:* Count of tickets processed through the matching step vs. tickets that skip it entirely.

---

## Top crack

**Deciding check:** unowned

The matching step has no assigned owner. When a reopen fails to link, no one is responsible for catching it.

---

## Ship call

Ship for tickets under 24 hours old (low risk of an unmatched reopen), hold for anything referencing "yesterday," "Tuesday," or "again" until ownership of the matching step is assigned. Priya reviews and reassigns by end of week.

---

## Tripwire

Watch engineer double-work reports — cases where two people are assigned the same underlying bug because of a missed reopen. If this hits 2+ per week, Priya escalates, since it directly reflects the unassigned matching gap.

---

## How a stranger uses this auditor

1. Describe your ticket-routing bot and what it's supposed to do when a customer reopens an issue
2. Paste 3+ real messages where it failed to match
3. Walk the five checks above, rating each 1–5
4. Identify your top crack (the check that decides)
5. Make a ship/hold call with conditions and owners
6. Set a tripwire: what number you'll watch, what level means trouble, and who watches it

The auditor applies the same discipline used on this build to your failing setup.