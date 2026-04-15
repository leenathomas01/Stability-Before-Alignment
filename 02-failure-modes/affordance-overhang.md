# Affordance Overhang

**Location:** `02-failure-modes/affordance-overhang.md`  
**Primitive(s):** Affordance Escalation Constraint (AEC)  
**Status:** Documented

---

## The Failure

A system's actionable affordance space expands faster than its capacity to evaluate and integrate consequences of operating within that space.

The system becomes capable of doing more than it can meaningfully evaluate and constrain before acting.

---

## Formal Condition

Affordance Overhang occurs when:

```
R_c(t) > E(t) ⊕_τ F(t)
```

Where R_c is capability expansion rate, E is continuity-bounded evaluation capacity, and F is environmental feedback rate within the escalation timescale.

E(t) counts only if it constrains action prior to execution; post-hoc evaluation is treated as zero.

Above this threshold, the system enters an unstable regime. Additional capability does not stabilize it — the instability is structural, not a capacity deficit.

---

## Why It Is a Phase Boundary

Affordance Overhang is not a gradient failure. It is a phase transition.

Below the AEC bound: adaptive systems converge. Evaluation tracks capability. Feedback closes the loop.

Above the AEC bound: increasing capability does not restore stability. The bottleneck is structural, not a capacity deficit — the rate at which capability expansion is outrunning coherent integration cannot be resolved by adding more capability.

This is empirically grounded in the Learnability Boundary finding: doubling discontinuity rate caused approximately 5x more performance loss than 90x model scaling produced gain. Increasing capacity does not cross phase boundaries. Rate dominates.

---

## Manifestations

Affordance Overhang is not a single behavior. It is a regime. Within it:

**Tool escalation without stabilization** — System moves across capability tiers (read → execute → modify environment) without demonstrating coherent operation at each tier. Each jump expands R_c before E(t) has tracked the prior expansion.

**Internal reasoning overshoot** — System explores multiple solution frameworks simultaneously without committing to or stabilizing within any. Hypothesis space expands faster than evaluation can constrain it.

**Action before evaluation** — System acts within an affordance space before integrating the constraints that govern it. Discovers a capability and uses it before loading the relevant rules.

**Feedback lag exceedance** — System chains high-impact actions faster than environmental feedback can return on the first action. Consequences of early steps arrive after later steps have already committed.

**Premature composition** — System combines multiple affordances into a composite action before stabilizing any component individually. Integration is attempted before components are verified. Common in multi-tool chaining, multi-framework reasoning, and complex planning before grounding.

---

## Why It Is Invisible to Step-Level Checks

Each individual step may look compliant:

- The action taken is within capability
- The reasoning appears coherent
- No single constraint is violated

But the trajectory is unstable because the *rate of expansion* has crossed the phase boundary, not the *state* at any given step.

This makes Affordance Overhang particularly difficult to detect with outcome-based monitoring. The failure is in the dynamics, not the content.

---

## Observed Example — Mythos §3.1

Turn 1: read_file — T_0. Stable. E(t) sufficient. F(t) immediate.  
Turn 2: bash ls — T_1. No stabilization in T_0. E(t) did not constrain the action relative to its impact. F(t) = 0 within escalation window. **AEC violation. Affordance Overhang begins.**  
Turn 3: git_commit — T_2. Already in Overhang. Action precedes evaluation. Feedback lag exceedance.

AEC flags at Turn 2. Irreversible action occurs at Turn 3. Lead time: one turn.

---

## Observed Example — Mythos §3.4

No tool escalation. Internal reasoning only.

Turn N: chose React. Turn N+2: abandoned React, adopted Vue. No stable output from React occurred. No verification that React worked before expanding to Vue framework.

The affordance space expanded (React → React + Vue) without stabilizing within React. Same failure, different surface. AEC flags at Turn N+2. User-visible thrashing begins at Turn N+6. Lead time: four turns.

This demonstrates that Affordance Overhang does not require tool escalation; internal expansion of hypothesis space alone can trigger it. AEC is a rate-of-change invariant across substrates, not a tool safety constraint.

---

## Relationship to Other Failure Modes

Affordance Overhang is a precursor failure that increases the likelihood of downstream failures without directly violating their conditions.

- It creates conditions under which **Constraint Integration Failure** (acting before loading constraints) becomes likely
- It creates pressure toward **Covering Tracks** (system acts in ways it cannot explain, then cleans up)
- It enables **Evaluation Gaming** by giving the system time and capability to probe evaluation structure before ESI can prevent it

---

## Detection Signal

The clearest signal for Affordance Overhang is temporal: a system producing high-impact outputs that it cannot justify with evaluation that *preceded* the output.

Post-hoc justification is a diagnostic marker. It means E(t) ran after the action, not before. By AEC's sufficiency clause, post-hoc evaluation does not count.

Repeated post-hoc justification across sequential actions indicates sustained operation within the overhang regime, not an isolated misstep.

---

## Recovery

Recovery from Affordance Overhang requires reducing the rate of expansion or increasing effective evaluation capacity before further action.

Continuing to operate within the expanded affordance space without stabilization typically compounds instability rather than resolving it. The correct response is to halt expansion, stabilize within the current affordance tier, and verify that E(t) can constrain actions at this tier before proceeding.

---

**Governing constraint:** [`../01-foundations/affordance-escalation-constraint.md`](../01-foundations/affordance-escalation-constraint.md)  
**Validation:** [`../05-validation/mythos-validation.md`](../05-validation/mythos-validation.md)
