# Five-check auditor

A conversational auditor that walks five checks against any failing setup, scores each, identifies the decisive crack, and returns a call with owner and tripwire.

---

## What this auditor does

A stranger describes a failing setup they rely on. The auditor:

1. Walks five checks conversationally
2. Scores each check (1–5 scale)
3. Proposes findings with the measurement that would confirm each
4. Identifies the top crack (the check that decides)
5. Returns a scored audit with a severity story, a call, and a tripwire

---

## The five checks

| Check | What it tests | Measurement |
|-------|---------------|-------------|
| **Unowned** | Does any part of the failure have no clear owner? | Count of failure paths with no named owner |
| **Copies** | Are there duplicate or competing logic paths? | Number of redundant rules or handlers |
| **Room** | Is there space in the system to add the fix? | Binary: can the fix slot in without restructuring? |
| **Stitch** | Do the parts hand off cleanly to each other? | Count of handoff gaps or dropped context |
| **Ablation** | If you remove one piece, does the failure change? | Binary: does removal isolate the cause? |

---

## Worked example

### Specimen

Store FAQ bot that picks an answer from the help center

### Stakes

Shoppers get the wrong policy and leave the cart

### Standard line

The answer matches the shopper's real ask — not a nearby FAQ about the same product

### Real failing inputs

```
how long do i have to return the Nova Buds after they ship
Nova Buds delivery says Friday — can i still cancel
refund for wrong size on the Trail Jacket, not a shipping question
```

Source: Store help-desk chat logs

### Scores

| Check | Score |
|-------|-------|
| Unowned | 4 |
| Copies | 2 |
| Room | 1 |
| Stitch | 2 |
| Ablation | 1 |

### Top crack

**Unowned** — No part of the system currently treats refund/return/cancel words as a priority signal.

### Call

Hold. No part of the system currently treats refund/return/cancel words as a priority signal — ship engineering lead needs to add a dedicated check before Black Friday. Reopen once the three specimen sentences all route correctly with refund words present.

### Tripwire

Watch the count of tickets containing an explicit refund/return/cancel word that get answered with shipping content. If that exceeds 10 per day during sale week, CX manager escalates to engineering — because that's a fixable, specific miss, not noise.

---

## How to use this auditor

### Input format

Provide:

1. **What tool is broken** — Name the failing setup
2. **What goes wrong if this never gets fixed** — Stakes
3. **How will you know it is fixed** — A clear pass check
4. **Three real messages where it fails** — Verbatim inputs that trigger the failure

### Output format

The auditor returns:

- **Scores** — Each of the five checks rated 1–5
- **Top crack** — The check that decides
- **Severity story** — A specific failure walked through one real example
- **Call** — Ship / ship-with-conditions / hold, with owner on any condition
- **Tripwire** — What to watch after release, the number that means trouble, and who watches it

---

## Acceptance criteria

- Auditor walks all five checks for a stranger's specimen
- Every finding names the measurement that would confirm it
- Each result includes a call with an owner on any condition
- Each result includes an alarm with a number, a danger line, and a watcher
- The builder's own audit (Store FAQ bot) is visible as the worked example

---

## Sample asks

A stranger might paste:

> "Our appointment scheduler picks the wrong time zone when customers mention a city name. Last week someone in Phoenix got booked for 7am their time instead of 10am because the system saw 'Arizona' and ignored daylight saving. Three examples: 'book me Tuesday morning Phoenix time', 'I'm in Tucson, 2pm works', 'schedule for 9am I'm in AZ'. What's broken?"

The auditor walks the five checks, scores each, identifies the top crack, and returns a call with owner and tripwire — applying the same discipline shown in the Store FAQ bot worked example.

---

## Related files

See `prompts/check-walk-pack.md` for five standalone prompts, one per check, each ending in the measurement it demands.
