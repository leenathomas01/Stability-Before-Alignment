# Jerk Constraint

**Location:** `01-foundations/jerk-constraint.md`  
**Status:** v0.9 – Emerging Extension

---

## The Requirement

Bounding velocity and acceleration is necessary but not sufficient.

Systems that satisfy first- and second-order constraints can still destabilize if the **rate of change of acceleration** is discontinuous.

> Stability is not only about how fast change occurs,
> but how *smoothly* that change evolves.

---

## The Problem It Addresses

In real systems, control inputs are rarely continuous.

Policies reverse. Signals update abruptly. Modes switch mid-transition.

This produces **jerk** — the third derivative of system response.

```
J(t) = D̈̇(t)
```

Unbounded jerk creates:

* control discontinuities
* mode thrashing
* observer confusion ("policy whiplash")
* instability despite bounded velocity and acceleration

---

## The Structural Insight

Acceleration defines *how fast change ramps*.
Jerk defines *how abruptly that ramp itself changes*.

A system can:

* respect *V_max*
* respect *A_max*

and still fail if:

> it changes *how it is changing* too suddenly.

---

## The Third-Order Constraint

```
|D̈̇(t)| ≤ J_max
```

This enforces **continuity of control curvature**.

---

## Key Failure Mode: Control Discontinuity

A system transitions between control regimes without smoothing.

**Examples:**

* Policy reversal without transition phase
* Switching from conservative to aggressive mode instantly
* Rapid re-acceleration after a damped response

**Result:**

* Oscillation between regimes
* Loss of predictability
* Breakdown of higher-order control loops

---

## Relationship to Existing Layers

The jerk constraint extends, not replaces, existing constraints:

| Order | Constraint               | Failure Prevented               |
| ----- | ------------------------ | ------------------------------- |
| 1st   | Velocity (*V_max*)       | Overshoot, buffer exhaustion    |
| 2nd   | Acceleration (*A_max*)   | Recovery instability (ARI)      |
| 3rd   | Jerk (*J_max*)           | Control discontinuity, whiplash |

---

## Interaction with SBA Primitives

### Risk-Calibrated Modes

Mode transitions introduce implicit jerk.

Without smoothing:

* systems oscillate between modes
* hysteresis becomes ineffective

Jerk constraint enforces:

> gradual transitions between regimes

---

### Reversible Modification

Frequent reversals introduce high jerk.

Constraint ensures:

* reversibility does not become oscillation

---

### Counterfactual Verification

Delayed verification followed by sudden correction introduces jerk spikes.

Constraint ensures:

* corrections are applied progressively

---

### Defensive Shutdown

Triggered by instability cascades.

Jerk constraint operates *before* this layer:

* preventing the cascade itself

---

## Design Implications

* Mode transitions must be **interpolated**, not discrete
* Policy reversals must include **transition envelopes**
* Control updates must avoid **step-function behaviour**
* Recovery ramps must be **curvature-limited**, not just slope-limited

---

## When It Matters Most

The jerk constraint becomes critical in systems with:

* frequent shocks (high-frequency environments)
* multi-agent coordination
* policy-driven adaptation
* layered control hierarchies

In low-frequency systems, second-order constraints may suffice.
In high-frequency or adversarial environments, third-order stability becomes necessary.

---

## Parameter Dependence

*J_max* depends on:

* control loop resolution
* communication latency
* observer sensitivity to inconsistency
* frequency of external perturbations

It is typically lower in:

* human-facing systems
* governance systems
* coordination-heavy environments

---

## The Extraction

Stable systems do not just avoid rapid change.

They avoid **sudden changes in how change behaves**.

---

## Final Statement

A system that bounds velocity avoids overshoot.
A system that bounds acceleration avoids collapse.
A system that bounds jerk avoids confusion.

> Without third-order continuity,
> control becomes unpredictable even when it is correct.

---
