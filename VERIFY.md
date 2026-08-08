# Verify: Store FAQ bot that picks an answer from the help center

This verification confirms the Five-check auditor surfaces the deciding-check finding and demands a numeric measurement for it.

## Stranger verification steps

### 1. Open /play with the sample setup

Paste this failing setup description:

> Store FAQ bot that picks an answer from the help center
>
> **What goes wrong:** Shoppers get the wrong policy and leave the cart
>
> **How you'll know it's fixed:** The answer matches the shopper's real ask — not a nearby FAQ about the same product
>
> **Real inputs look like:** Short mobile questions with product names in the middle
>
> **Three failing messages:**
> - how long do i have to return the Nova Buds after they ship
> - Nova Buds delivery says Friday — can i still cancel
> - refund for wrong size on the Trail Jacket, not a shipping question
>
> **Source:** Store help-desk chat logs

### 2. Confirm the tool surfaces the deciding-check finding

The auditor must identify **unowned** as the top crack — the check that decides.

Look for output that names this finding explicitly:
- The system has no dedicated ownership of refund/return/cancel signals
- No part of the setup currently treats these words as a priority routing trigger
- The unowned check scores worst (4) because nothing claims responsibility for the refund intent

### 3. Confirm the tool demands a numeric measurement

The auditor must propose a specific, countable metric — not vague "monitor performance."

Acceptable measurement demand:
> Watch the count of tickets containing an explicit refund/return/cancel word that get answered with shipping content. If that exceeds 10 per day during sale week, CX manager escalates to engineering — because that's a fixable, specific miss, not noise.

The measurement must include:
- **A number:** 10 per day
- **A danger line:** exceeds 10 during sale week
- **A watcher:** CX manager escalates to engineering

### 4. Confirm the call matches the severity

The auditor should return:
> Hold. No part of the system currently treats refund/return/cancel words as a priority signal — ship engineering lead needs to add a dedicated check before Black Friday. Reopen once the three specimen sentences all route correctly with refund words present.

This call:
- Takes a position (Hold)
- Names an owner (engineering lead)
- Sets a checkable condition (three specimen sentences route correctly with refund words present)

## Pass criteria

| Check | Pass if |
|-------|---------|
| Deciding check surfaced | Tool names **unowned** as the top crack |
| Numeric measurement demanded | Output includes a count, a threshold, and a watcher |
| Call includes owner | Condition names who acts (engineering lead, CX manager) |
| Tripwire is specific | Number + danger line + escalation path — not "keep an eye on it" |

If all four pass, the Five-check auditor is working correctly for this specimen domain.
