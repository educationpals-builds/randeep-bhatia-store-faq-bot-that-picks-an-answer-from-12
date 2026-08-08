# Five-check auditor

**Worked example:** Store FAQ bot that picks an answer from the help center

---

## The problem

Shoppers get the wrong policy and leave the cart.

When a shopper asks about refunds, the FAQ bot latches onto the product name and returns shipping times instead. The answer should match the shopper's real ask — not a nearby FAQ about the same product.

---

## Verdict

**Hold.** No part of the system currently treats refund/return/cancel words as a priority signal — ship engineering lead needs to add a dedicated check before Black Friday. Reopen once the three specimen sentences all route correctly with refund words present.

---

## Tripwire

Watch the count of tickets containing an explicit refund/return/cancel word that get answered with shipping content. If that exceeds 10 per day during sale week, CX manager escalates to engineering — because that's a fixable, specific miss, not noise.

---

## Deciding check

**unowned** — scored 4/5 severity. This is the crack that decides the call.

---

## One-paste rebuild block

```
Specimen: Store FAQ bot that picks an answer from the help center
Stakes: Shoppers get the wrong policy and leave the cart
Standard: The answer matches the shopper's real ask — not a nearby FAQ about the same product

Sample failing inputs (from Store help-desk chat logs):
- how long do i have to return the Nova Buds after they ship
- Nova Buds delivery says Friday — can i still cancel
- refund for wrong size on the Trail Jacket, not a shipping question

Check scores:
  unowned: 4
  copies: 2
  room: 1
  stitch: 2
  ablation: 1

Top crack: unowned
Call: Hold
Tripwire: 10 refund-misroutes/day → CX manager escalates to engineering
```

---

## What this tool does

A stranger describes the failing setup they rely on — what it is supposed to do, who gets hurt when it fails, and a few real failing inputs. The Five-check auditor walks five checks conversationally, proposes findings with the measurement that would confirm each, and returns a scored audit with a severity story, a call, and a tripwire.

The builder's own audit of the Store FAQ bot is embedded as the worked example, so a stranger gets the same discipline applied to their own failing setup.

---

## Files in this repo

| File | Purpose |
|------|---------|
| `charter.md` | Full audit grounded in the Store FAQ bot specimen |
| `METHOD.md` | The five-check framework with acronym spelled out |
| `VERIFY.md` | Stranger verification instructions |

<!-- educationpals-build-verified -->
