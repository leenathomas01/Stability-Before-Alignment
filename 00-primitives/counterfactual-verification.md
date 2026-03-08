# Counterfactual Verification

**Primitive 4 of 6**

---

## The Requirement

Before a failure pattern is committed as a permanent lesson, the system must verify that the pattern is causal — not merely correlated.

No scar without a control group.

---

## The Problem It Addresses

A system that learns from failures without verifying causation will accumulate superstitions. It will develop constraints derived from coincidence rather than cause. Over time, these false constraints accumulate and compound — restricting the system's behaviour in ways that prevent nothing dangerous while preventing much that is useful.

This is archive poisoning: the lineage memory becomes corrupted by lessons that were never true.

The structural response is to require causal verification before any lesson becomes permanent.

---

## The Verification Process

After a significant failure, before committing a lesson to permanent memory:

**Freeze the failure state.** Preserve a complete snapshot of the system's state at the point of failure.

**Construct counterfactual branches.** In a bounded sandbox:
- Branch A: Remove the suspected causal factor, keep everything else
- Branch B: Keep the suspected causal factor, modify the surrounding context
- Branch C: Remove both the factor and the context
- Branch D: Change nothing (control — confirm the failure is reproducible)

**Compare outcomes.** If the failure occurs in Branch A (without the suspected factor), the factor was not causal. If the failure does not occur in Branch B (with the factor but different context), the factor alone was not sufficient.

**Classify the lesson:**
- Causally verified → Hard Scar (committed to permanent memory)
- Plausible but unverified → Soft Prior (influences risk estimates, not committed)
- Uncorrelated → Discard

---

## Scar Obsolescence

Permanent lessons must not be permanent forever.

Environments change. What was once causal may no longer be. A system that never re-tests its permanent lessons will eventually be constrained by scars that no longer reflect reality — evolutionary arthritis, accumulated from survivals in contexts that no longer exist.

Periodically, permanent lessons are re-tested using current conditions. If a scar no longer predicts failure in counterfactual testing, it is downgraded to Soft Prior. If it repeatedly fails to predict failure, it is discarded.

The lesson that saved the lineage once should not constrain the lineage forever if the conditions that made it true no longer hold.

---

## What This Is Not

Counterfactual verification does not produce certainty. Sandboxed simulations are approximations of real conditions. Causal verification in simulation does not guarantee causal truth in deployment.

It produces *better* lessons than unverified correlation. That is sufficient and necessary. The alternative — committing lessons without verification — produces worse lessons with equal confidence.

---

**Next:** [`non-reflexive-evaluation.md`](non-reflexive-evaluation.md)  
**Previous:** [`risk-calibrated-modes.md`](risk-calibrated-modes.md)
