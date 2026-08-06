# Support ticket bot that reopens the original failure instead of answering the last reply

Your ticket bot tags the wrong issue when a customer says "it broke again". The bot opens a new ticket instead of finding the old one.

## The problem

When customers reply with short messages like "it happened again" or "can you link this to #44821 instead of opening a new ticket," the bot misses the reopen signal and creates a fresh ticket. Wrong person gets the ticket; the real bug waits another day.

## Verdict

**Ship with conditions.**

Ship for tickets under 24 hours old (low risk of an unmatched reopen), hold for anything referencing "yesterday," "Tuesday," or "again" until ownership of the matching step is assigned. Priya reviews and reassigns by end of week.

## Tripwire

Watch engineer double-work reports — cases where two people are assigned the same underlying bug because of a missed reopen. If this hits 2+ per week, Priya escalates, since it directly reflects the unassigned matching gap.

## What "fixed" looks like

A reopen lands on the original ticket, not a new one about the side comment.

## One-paste rebuild

Run the five-check audit on your own ticket-reopen setup:

```
I have a support ticket bot that's supposed to reopen original failures
instead of answering the last reply. It's failing on short messages
with pronouns like "it" and "that" and words like "again."

Walk me through the five checks. For each one, tell me what you'd
measure and what finding you'd expect. Then give me a call
(ship / ship-with-conditions / hold) and a tripwire I can watch.
```

See [charter.md](charter.md) for the full audit of this setup, including the three failing messages, the check scores, and the deciding gap.

See [METHOD.md](METHOD.md) for the five-check framework this audit applies.

See [VERIFY.md](VERIFY.md) to confirm the tool surfaces the right findings for your own setup.

<!-- educationpals-build-verified -->
