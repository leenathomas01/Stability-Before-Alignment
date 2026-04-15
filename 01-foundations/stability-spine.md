# Stability Spine

**Location:** `01-foundations/stability-spine.md`  
**Status:** v1.2 – Control Layer Extension

---

## The Requirement

Structural coherence alone is insufficient.

A system can satisfy all six primitives and still fail if it changes too quickly for its own control loops, physical substrate, or observers to track.

> Coherence prevents silent corruption.
> Stability prevents dynamic collapse.

The Stability Spine defines the temporal constraints required for a coherent system to remain stable under change.

---

## The Problem It Addresses

Self-modifying systems operate across mismatched timescales:

* Detection is fast (milliseconds)
* Response is fast (runtime)
* Physical recovery is slow (seconds to hours)
* Evaluation is slower (cycles to epochs)
* Social or external interpretation is slowest (hours to years)

When system response exceeds the slowest layer's ability to track it, instability emerges.

This produces a distinct failure mode:

> A system that is correct in state, but unstable in transition.

---

## The Structural Insight

Stability is not a property of state.

It is a property of **how state changes over time**.

To remain stable, a system must bound not just what it does, but:

* how fast it changes
* how sharply it changes

---

## The Multi-Order Constraints

Let *D(t)* represent system output or distribution.

### First-Order Constraint (Velocity)

```
|Ḋ(t)| ≤ V_max
```

The rate of change must be bounded.

Unbounded velocity produces:

* buffer exhaustion
* overshoot
* oscillation

---

### Second-Order Constraint (Acceleration)

```
|D̈(t)| ≤ A_max
```

The rate of change of change must be bounded.

Unbounded acceleration produces:

* perception instability
* loss of trust in system behaviour
* collapse during recovery

---

### Third-Order Constraint (Jerk) *(Emerging)*

```
|D̈̇(t)| ≤ J_max
```

Sudden changes in acceleration produce:

* control discontinuities
* policy whiplash
* mode instability

This layer is not yet formalized in this framework but is expected in systems subject to repeated shocks or rapid reversals.

---

## Key Failure Mode: Asymmetric Recovery Instability (ARI)

A system survives the initial shock, but collapses during recovery.

**Conditions:**

* Physical buffer remains intact
* Control logic is correct
* Response accelerates too quickly

**Result:**

* Recovery is interpreted as instability
* Legitimacy or trust collapses
* System enters failure despite restored resources

---

## Relationship to Existing Primitives

The Stability Spine does not replace the primitives.
It constrains their operation over time.

---

### Reversible Modification

Ensures recovery is possible.
Spine ensures recovery is **stable**.

---

### Risk-Calibrated Modes

Introduces hysteresis and mode switching.
Spine formalizes this as bounded velocity and acceleration.

---

### Non-Reflexive Evaluation

Separates Actor and Evaluator timescales.
Spine generalizes this into a system-wide constraint:

> Slower layers must not be outrun by faster ones.

---

### Append-Only Memory

Preserves historical continuity.
Spine prevents rapid state changes that invalidate interpretation of that history.

---

### Counterfactual Verification

Prevents incorrect adaptation.
Spine prevents adaptation from occurring faster than it can be verified.

---

### Defensive Shutdown

Handles total loss of reliable reference.
Spine defines the instability regime that precedes that condition.

---

## The Control Layer

The Stability Spine defines a control layer that operates alongside the structural primitives:

| Layer                   | Function                              |
| ----------------------- | ------------------------------------- |
| Structural (Primitives) | Maintain coherence under modification |
| Control (Spine)         | Maintain stability under change       |

Both are required.

A system with primitives but no control layer:

* remains coherent
* but can destabilize itself

A system with control but no primitives:

* remains stable
* but may drift or corrupt silently

---

## Design Implications

* Systems must enforce **rate limits** on adaptation
* Recovery must be **ramped**, not instantaneous
* Positive and negative transitions must be **symmetric in constraint**
* Stability depends on the **slowest layer in the system**

---

## Parameter Dependence

The values of *V_max*, *A_max*, and *J_max* are not universal.

They depend on:

* physical substrate limits
* verification latency
* communication bandwidth
* observer perception thresholds

These parameters must be empirically derived for each deployment context.

---

## The Extraction

Across domains, stable systems share a common pattern:

* Do not exceed buffer capacity
* Do not outrun verification
* Do not change faster than the system can observe itself

These are not design choices.

They are constraints imposed by operating across multiple timescales.

---

## Final Statement

A system that cannot bound its rate of change will destabilize itself.

A system that cannot bound its acceleration will collapse during recovery.

> Stability requires constraining not just what changes,
> but how change unfolds over time.

---

## Extension — v0.2

The Stability Spine defines dynamic constraints on system output over time (velocity, acceleration, jerk).

SBA v0.2 extends this with **Affordance Escalation Constraint (AEC)**, which applies the same phase-boundary logic specifically to *capability space expansion*: a system must not expand its actionable affordance space faster than it can evaluate and integrate consequences.

AEC is the temporal twin of the Stability Spine applied to affordance space rather than output space. The underlying principle is identical: rate of change must not outrun the system's capacity to track it.

The theoretical grounding connects to the Learnability Boundary finding: discontinuity rate dominates over capacity. Capability does not cross phase boundaries. Rate does.

See: [`affordance-escalation-constraint.md`](affordance-escalation-constraint.md)
