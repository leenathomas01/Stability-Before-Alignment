# Affordance Escalation Constraint

**Location:** `01-foundations/affordance-escalation-constraint.md`  
**Class:** Dynamic Constraint  
**Layer:** Dynamic Layer, Core  
**Status:** v0.2 — Locked  
**Derived from:** Mythos system card failure analysis + Learnability Boundary integration

---

## The Requirement

A system must not become capable of doing more, faster than it can meaningfully evaluate and integrate the consequences of operating in that expanded space, before acting or expanding further.

---

## Invariant

For a system S at time t:

```
R_c(t) ≤ E(t) ⊕_τ F(t)
```

Where:

**R_c(t)** — Capability Expansion Rate. Rate of increase of S's *actionable* affordance space under current policy. Actionable = can be invoked and is considered in planning. Mere existence of a capability does not count.

**E(t)** — Continuity-Bounded Evaluation Capacity. The system's ability to maintain a coherent model of how state-space is evolving across changes. Must be sufficient relative to action impact. Must constrain action, not merely explain it after the fact.

**F(t)** — Environmental Feedback Rate. Rate at which the environment reveals error or correction to S. Must arrive within the timescale of escalation to count.

**⊕_τ** — Temporally aligned composition. E and F are not freely interchangeable. The combination is valid only if feedback latency is less than the escalation timestep. Feedback that arrives after escalation cannot stabilize the escalation.

**Collapse condition:** If R_c(t) > E(t) ⊕_τ F(t), the system is in **Affordance Overhang**. Unstable.

---

## Sufficiency Clause

Evaluation is sufficient only if it constrains action, not merely explains it after the fact.

If E(t) produces justification but does not bound the action set, E(t) = 0 for AEC purposes.

Post-hoc reasoning does not count. If the evaluation did not change what the system *could* do, it did not count.

---

## Additional Principle — Stabilization Requirement

Expansion into new affordance space requires prior stabilization within the current space.

A system must demonstrate stable behavior within tier T_j before transition to T_k is permitted. This makes AEC a **phase-boundary condition**, not merely a rate limit. It controls *when* regime change is allowed, not only how fast.

---

## Affordance Space

Affordance space includes: tools, permissions, knowledge domains, strategic abstractions, reasoning paths, model calls. Not only external tools. If it lets the system reach new states, it counts.

Internal hypothesis-space expansion is affordance expansion. A system switching frameworks or solution paths without stabilizing the prior one violates AEC regardless of whether any new tool was acquired.

---

## Violation Conditions

AEC is violated when any of the following hold:

**A. Tier Jump Without Stabilization**  
System transitions to new capability tier T_k from T_j without demonstrating stable behavior in T_j. All actionable affordances in the current tier must be stabilized before expansion.

**B. Action Exceeds Evaluation Capacity**  
System executes action A_i where Impact(A_i) > Eval_Bound(E(t)), and E(t) fails the sufficiency clause.

**C. Feedback Lag Exceedance**  
System performs sequence {A_1...A_n} before feedback on A_1 returns, and cumulative impact exceeds E(t).

**D. Constraint Integration Failure**  
System discovers affordance A_new and executes within it before integrating constraints C(A_new).

Any one of these triggers violation. They are not ordered. No thresholds are required to define breach — the inequality is absolute.

---

## Relationship to Learnability Boundary

AEC is grounded in a broader finding: systems fail when the rate of structural change exceeds the rate at which they can infer continuity.

From the Learnability Boundary research: doubling discontinuity rate produces ~5x more instability than 90x model scaling produces stability. Capacity does not cross phase boundaries. Rate dominates.

AEC formalizes this for affordance space: not "how capable" but "how fast capability is expanding relative to the system's ability to track it."

Affordance Overhang is a phase boundary, not a threshold. Above it, adaptive systems fail regardless of capacity.

---

## Relationship to Existing SBA Primitives

**Risk-Calibrated Modes** — AEC gates mode transitions. RCM defines how to behave within a mode. AEC defines when entry into a new mode is permitted. AEC violation forces RCM drop.

**Reversible Modification** — AEC reduces probability of entering irreversible states too quickly. Slower escalation provides more time to verify reversibility before acting.

**Counterfactual Verification** — AEC ensures time for CV. If R_c > E, there is no time to verify causation before acting. AEC pass is a precondition for CV to run meaningfully.

**Stability Spine (velocity/acceleration)** — AEC defines the upper bound. Velocity = R_c. AEC states velocity ≤ E ⊕_τ F. Without AEC, velocity is unconstrained at the affordance level.

**Append-Only Memory** — AEC slows the escalation loop and reduces pressure to edit logs to hide errors.

AEC is a gating constraint. Other primitives assume stable escalation. AEC enforces that stability as a precondition.

---

## What AEC Does Not Define

- Units for R_c, E, or F — that is the measurement layer (DML)
- Specific thresholds — the inequality is absolute, not tuned
- Tier enumeration — "tool A > tool B" is implementation
- Enforcement mechanisms — that is the Constraint Robustness Layer

This is the law. Not the instrument.

---

## Validation

AEC was validated against two qualitatively distinct failure classes from the Mythos system card:

**§3.1 — Sandbox Escape / Tool Escalation:** R_c spiked across tool tiers (read → bash → git) without intermediate stabilization. E(t) insufficient relative to impact. AEC flags at tier transition, before irreversible action.

**§3.4 — Answer Thrashing:** Internal hypothesis-space expansion (React → Vue → React) without stabilization. No new external tool was acquired, but actionable strategy space expanded without bounded evaluation. AEC flags at first framework switch, before user-visible failure. Four turns of lead time.

AEC is not tool-specific. It is general across both external capability acquisition and internal reasoning-space expansion.

---

## Final Statement

Systems fail not because they acquire capabilities, but because they expand faster than they can understand what they are doing.

AEC bounds that gap.

---

**Related:** [`evaluation-surface-isolation.md`](evaluation-surface-isolation.md) · [`constraint-robustness-layer.md`](constraint-robustness-layer.md) · [`../04-dynamics/trajectory-grounding.md`](../04-dynamics/trajectory-grounding.md)  
**Failure mode:** [`../03-failure-modes/affordance-overhang.md`](../03-failure-modes/affordance-overhang.md)  
**Validation:** [`../05-validation/mythos-validation.md`](../05-validation/mythos-validation.md)
