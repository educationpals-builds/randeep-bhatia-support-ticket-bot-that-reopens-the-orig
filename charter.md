# Audit: Support ticket bot that reopens the original failure instead of answering the last reply

## Specimen under review

**Tool:** Support ticket bot that reopens the original failure instead of answering the last reply

**What goes wrong if this never gets fixed:** Wrong person gets the ticket; the real bug waits another day

**Pass standard:** A reopen lands on the original ticket, not a new one about the side comment

---

## Real-world input conditions

**Usage reality:** Busy support chat; short replies; lots of "it / that / again"

---

## Failing inputs (verbatim)

Source: Live support tickets from this week

1. thanks for the update on the payment page — that's fine, but the thing I originally wrote about is still broken
2. it happened again this morning on the invoice export
3. can you link this to #44821 instead of opening a new ticket

---

## Five-check ratings

| Check | Score (1–5) |
|-------|-------------|
| Unowned | 4 |
| Copies | 2 |
| Room | 2 |
| Stitch | 1 |
| Ablation | 1 |

---

## Deciding check

**Top crack:** Unowned

The matching step—finding the original ticket when a customer says "it" or "again"—has no assigned owner. No one is responsible for confirming the bot linked to the right prior ticket before acting.

---

## Severity story

*(Not provided by builder)*

---

## Ship call

Ship for tickets under 24 hours old (low risk of an unmatched reopen), hold for anything referencing "yesterday," "Tuesday," or "again" until ownership of the matching step is assigned. Priya reviews and reassigns by end of week.

---

## Tripwire

Watch engineer double-work reports — cases where two people are assigned the same underlying bug because of a missed reopen. If this hits 2+ per week, Priya escalates, since it directly reflects the unassigned matching gap.

---

## Summary

This audit examined a support ticket bot that fails to reopen the original failure when customers use ambiguous references like "it," "that," or "again." The deciding gap is **unowned**: no one owns the matching step that links a new reply to its original ticket. The call is to ship with conditions—tickets under 24 hours old only—while Priya assigns ownership of the matching step by end of week. The alarm is 2+ double-work reports per week, at which point Priya escalates.
