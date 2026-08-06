# The Five-Check Method

This audit framework applies five checks to any setup that's supposed to route, match, or classify incoming messages. Each check tests whether the system actually splits the work correctly—or collapses everything into one undifferentiated pile.

## PRISM

**P — Partition the Space**  
Does the setup divide the input space into distinct, non-overlapping regions? For a ticket bot handling reopens, this means: can it tell "this is a new issue" from "this is a follow-up to an existing ticket"? If every message lands in the same bucket, there's no partition.

**R — Run in Parallel**  
Do the checks run independently, or does one gate the others? A healthy setup evaluates multiple signals at once—recency, ticket reference, customer history—without waiting for a single classifier to finish first.

**I — Individuate the Pattern**  
Can the system recognize the specific pattern it's looking for, separate from noise? When a customer writes "it happened again," does the bot see "reopen signal" or just "vague pronoun"?

**S — Stitch the Spectra**  
After running checks, does the system combine findings into a coherent decision? If the recency check says "recent ticket exists" and the reference check says "customer mentioned #44821," those signals need to merge into one routing action—not fight each other.

**M — Map What Each Head Sees**  
Can you trace which part of the system saw which input and made which call? When a ticket lands on the wrong person, you need to know: did the matcher fire? Did it find the right ticket? Did the router override it?

---

## The Collapse-to-Monochrome Anti-Pattern

When a setup fails multiple checks, it often collapses into monochrome: every input gets the same treatment. The ticket bot opens a new ticket for everything. The classifier marks every message "general inquiry." The router sends all requests to the same queue.

This happens when:
- Partitions blur together (no clear boundary between "new" and "reopen")
- Parallel checks get serialized and one blocks the rest
- Pattern recognition fails on ambiguous inputs like "it" or "that"
- Stitching logic picks a default instead of combining signals
- No one can trace which component made the call

The audit scores each check 1–5. A score of 1 means the check is completely absent or broken. A score of 4–5 means it's working as intended. The deciding check—the one that most explains the failure—drives the ship/hold call.
