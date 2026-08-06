# Five-Check Audit Prompts: Support Ticket Bot That Reopens the Original Failure

Use these five prompts to audit any ticket-routing bot that struggles to match follow-up messages to their original tickets. Each prompt walks one check and ends with the measurement it demands.

---

## Prompt 1: Unowned Check

You are auditing a support ticket bot that should reopen the original failure instead of answering the last reply.

**The problem:** When a customer says something like "it broke again" or references a prior issue, the bot opens a new ticket instead of finding and reopening the old one.

**Worked example (real failing input):**
> thanks for the update on the payment page — that's fine, but the thing I originally wrote about is still broken

In this case, the customer acknowledges a side topic ("payment page") but explicitly asks about "the thing I originally wrote about." A correct bot links this to the original ticket. A broken bot opens a new ticket about the payment page comment.

**Your task:** Examine the setup you're auditing. Who owns the step that matches a follow-up message to its original ticket? Is that ownership documented, or does the message fall through unassigned?

**Measurement demanded:** Name the person or system responsible for the matching step. If no one owns it, state "unowned" and count how many follow-up messages per week currently fall through without a match.

---

## Prompt 2: Copies Check

You are auditing a support ticket bot that should reopen the original failure instead of answering the last reply.

**The problem:** The bot may create duplicate tickets when a customer references a prior issue, leading to the same bug being worked by multiple people.

**Worked example (real failing input):**
> it happened again this morning on the invoice export

This message references a recurring issue ("again") on a specific feature ("invoice export"). If the bot opens a new ticket instead of linking to the existing invoice export bug, two engineers may end up working the same underlying problem.

**Your task:** Check whether the setup produces duplicate tickets for the same underlying issue. Look for cases where "again" or "still broken" triggers a new ticket instead of a reopen.

**Measurement demanded:** Count the number of duplicate ticket pairs created in the last week where both tickets trace to the same root bug. Report the exact number.

---

## Prompt 3: Room Check

You are auditing a support ticket bot that should reopen the original failure instead of answering the last reply.

**The problem:** The bot may not have enough context to distinguish a side comment from a reopen request.

**Worked example (real failing input):**
> thanks for the update on the payment page — that's fine, but the thing I originally wrote about is still broken

This message contains two topics: (1) a side comment about the payment page, and (2) a reopen request for the original issue. The bot needs room in its context window or logic to hold both and route correctly.

**Your task:** Examine whether the bot's prompt, context window, or matching logic has room to hold the full conversation history needed to distinguish side comments from reopen requests.

**Measurement demanded:** State the maximum conversation turns or tokens the bot can access when making a routing decision. If the limit is too short to hold typical reopen scenarios, report the gap in turns or tokens.

---

## Prompt 4: Stitch Check

You are auditing a support ticket bot that should reopen the original failure instead of answering the last reply.

**The problem:** The bot may fail to stitch together references across messages—"it," "that," "the thing I wrote about"—to the correct original ticket.

**Worked example (real failing input):**
> can you link this to #44821 instead of opening a new ticket

Here the customer explicitly names a ticket number (#44821) and asks for a link. If the bot still opens a new ticket, the stitch step is broken.

**Your task:** Test whether the bot can resolve explicit ticket references (like #44821) and implicit references (like "the thing I originally wrote about") to the correct original ticket.

**Measurement demanded:** Run three test messages with explicit or implicit references. Report how many of the three correctly stitch to the original ticket. Express as X/3.

---

## Prompt 5: Ablation Check

You are auditing a support ticket bot that should reopen the original failure instead of answering the last reply.

**The problem:** Removing or disabling the matching step may reveal whether it's actually doing useful work or just adding latency.

**Worked example (real failing inputs):**
> thanks for the update on the payment page — that's fine, but the thing I originally wrote about is still broken
> it happened again this morning on the invoice export
> can you link this to #44821 instead of opening a new ticket

**Your task:** Temporarily disable or bypass the matching/reopen logic. Run the same inputs through. Compare the outputs to when matching is enabled.

**Measurement demanded:** Report the difference in correct routing (reopen vs. new ticket) with matching enabled vs. disabled. If disabling matching produces the same or better results, the matching step is not contributing. Express as: "With matching: X/3 correct. Without matching: Y/3 correct."

---

## Sample Asks

Use these real failing inputs to test any ticket-routing bot:

1. thanks for the update on the payment page — that's fine, but the thing I originally wrote about is still broken
2. it happened again this morning on the invoice export
3. can you link this to #44821 instead of opening a new ticket

---

## How to Use This Pack

1. Pick the check most relevant to your failing setup
2. Paste the prompt into any chat model
3. Replace the worked example with your own failing inputs if needed
4. Collect the measurement the prompt demands
5. Repeat for all five checks to complete the audit

The measurements you collect become your audit scorecard. The check with the worst score is your top crack—fix that first.
