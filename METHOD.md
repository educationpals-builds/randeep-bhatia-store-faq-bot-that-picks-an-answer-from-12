# The Five-Check Method

This auditor walks five checks to determine whether a failing setup is ready to ship. The checks follow the **PRISM** framework:

---

## P — Partition the Space

Does the system divide the input space into distinct, non-overlapping regions? A setup that lumps "refund" questions with "shipping" questions because both mention a product name has failed to partition. Each region should map to exactly one handler.

**What to measure:** Count how many input categories exist and whether any two categories share a routing trigger.

---

## R — Run in Parallel

Can multiple checks fire at once without collision? If the system can only evaluate one signal at a time, it will latch onto the first match and ignore later, more relevant signals. A shopper asking about a refund for the Nova Buds shouldn't get routed to shipping just because "Nova Buds" matched first.

**What to measure:** Number of signals evaluated per input; whether priority ordering exists when multiple signals match.

---

## I — Individuate the Pattern

Does each check have its own distinct pattern, or do patterns blur together? "Refund," "return," and "cancel" are different words that should all trigger the same refund-handling path — but they must be recognized as a coherent pattern, not confused with "delivery" or "shipping."

**What to measure:** Precision and recall for each pattern category against labeled test inputs.

---

## S — Stitch the Spectra

When multiple signals are present, does the system combine them correctly? A question like "refund for wrong size on the Trail Jacket, not a shipping question" contains both product and refund signals. The system must stitch these together and prioritize the refund intent.

**What to measure:** Accuracy on multi-signal inputs; whether the system has explicit combination rules.

---

## M — Map What Each Head Sees

Can you trace exactly what each component of the system detected? If you can't see that the FAQ bot latched onto "Nova Buds" and ignored "return," you can't fix the routing. Every head (classifier, matcher, router) should expose what it saw.

**What to measure:** Whether each component logs its match; whether you can reconstruct the decision path for any input.

---

## The Anti-Pattern: Collapse to Monochrome

When a system fails PRISM, it typically **collapses to monochrome** — treating all inputs as variations of one category. The Store FAQ bot that answers every Nova Buds question with shipping info has collapsed: it sees only the product name and ignores the action word (refund, cancel, return).

Signs of collapse:
- One trigger dominates all routing
- Action words are ignored in favor of entity names
- Multi-intent questions always resolve to the same handler
- No priority signal exists for high-stakes categories (refunds, cancellations)

The fix is to restore color: partition the space, individuate the patterns, and ensure the system can see and stitch multiple signals.

---

## Using the Checks

Rate each check 1–5:
- **5** = fully implemented, measurable, passing
- **4** = implemented but not measured
- **3** = partially implemented
- **2** = acknowledged but not built
- **1** = absent or broken

The lowest-scoring check is usually the deciding factor. Fix that one first.
