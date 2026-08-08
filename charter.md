# Audit: Store FAQ bot that picks an answer from the help center

## Specimen under review

**Tool:** Store FAQ bot that picks an answer from the help center

**Stakes if unfixed:** Shoppers get the wrong policy and leave the cart

**Standard for success:** The answer matches the shopper's real ask — not a nearby FAQ about the same product

---

## Real inputs tested

**Input profile:** Short mobile questions with product names in the middle

**Source:** Store help-desk chat logs

### Specimen sentences

```
how long do i have to return the Nova Buds after they ship
Nova Buds delivery says Friday — can i still cancel
refund for wrong size on the Trail Jacket, not a shipping question
```

---

## Five-check findings

| Check | Rating | Notes |
|-------|--------|-------|
| unowned | 4 | Highest-severity gap — no component owns refund/return/cancel intent |
| copies | 2 | Some duplication in FAQ matching logic |
| room | 1 | Minimal headroom for edge cases |
| stitch | 2 | Weak handoff between product-name detection and intent classification |
| ablation | 1 | Removing product-name matching doesn't isolate the failure |

---

## Deciding check

**Top crack:** unowned

The system has no dedicated owner for refund/return/cancel words. When a shopper types "refund for wrong size on the Trail Jacket, not a shipping question," the bot latches onto "Trail Jacket" and returns shipping content — because nothing in the pipeline prioritizes the explicit refund signal over the product name match.

---

## Call

Hold. No part of the system currently treats refund/return/cancel words as a priority signal — ship engineering lead needs to add a dedicated check before Black Friday. Reopen once the three specimen sentences all route correctly with refund words present.

---

## Tripwire

Watch the count of tickets containing an explicit refund/return/cancel word that get answered with shipping content. If that exceeds 10 per day during sale week, CX manager escalates to engineering — because that's a fixable, specific miss, not noise.

---

## Audit summary

This audit examined a store FAQ bot that routes shopper questions to help-center answers. The bot fails when shoppers ask about refunds, returns, or cancellations while mentioning a product name — it latches onto the product and serves shipping content instead of policy content.

The deciding gap is **unowned**: no component in the current system treats refund/return/cancel words as a priority signal. Until engineering adds that dedicated check, the bot will continue misrouting these questions during the upcoming sale week.

**Verdict:** Hold until the three specimen sentences route correctly with refund words present. Monitor for 10+ refund-misroutes per day as the escalation threshold.
