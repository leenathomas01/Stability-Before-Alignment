# Perceptual Bandwidth Constraint

**Location:** `01-foundations/perceptual-bandwidth-constraint.md`  
**Status:** v0.9 – Emerging Extension

---

## The Requirement

A system may be physically stable and control-bounded, yet still fail if its changes exceed the observer's ability to interpret them.

> Stability is not only constrained by system dynamics, but by the bandwidth of the entity observing the system.

---

## The Problem It Addresses

Control systems are typically analyzed in terms of internal dynamics:

* velocity (rate of change)
* acceleration (rate of change of change)
* jerk (control continuity)

However, adaptive systems also operate relative to external interpreters:

* humans
* other agents
* governance structures

These interpreters have finite perceptual bandwidth.

When system updates exceed this bandwidth:

* changes appear discontinuous
* causality becomes opaque
* trust degrades

---

## The Structural Insight

There exists a maximum rate at which an observer can:

* track system state
* understand transitions
* maintain a stable model of system behavior

This defines a constraint:

```
|Ḋ(t)|, |D̈(t)|, |D̈̇(t)| ≤ B_perceptual
```

Where:

* *B_perceptual* is the observer's interpretive capacity

---

## Key Failure Mode: Perceptual Aliasing

When system dynamics exceed perceptual bandwidth:

* smooth transitions appear as discontinuities
* controlled recovery appears as instability
* correct behavior is interpreted as error

---

## Relationship to Stability Spine

The perceptual constraint operates across all dynamic layers:

| Layer      | Constraint               | Internal vs External |
| ---------- | ------------------------ | -------------------- |
| Velocity   | *V_max*                  | Physical / system    |
| Acceleration | *A_max*              | Control / system     |
| Jerk       | *J_max*                  | Control continuity   |
| Perceptual | *B_perceptual*           | Observer / external  |

---

## Relationship to 70% Fidelity Principle

Observers do not process full system detail.

They operate on compressed representations.

Stability requires transmitting only the structural invariant within perceptual limits.

Exceeding this introduces:

* cognitive overload
* misinterpretation of noise as signal
* instability in interpretation

---

## Interaction with SBA Primitives

### Non-Reflexive Evaluation

Defines internal evaluation boundary.

Perceptual constraint extends this externally:

* evaluation must remain interpretable

---

### Counterfactual Verification

Generates multiple possible interpretations.

Perceptual constraint requires:

* limiting simultaneous hypothesis exposure

---

### Risk-Calibrated Modes

Switching modes changes system behavior.

Perceptual constraint requires:

* transitions be legible to observers

---

### Append-Only Memory

Preserves full system history.

Perceptual constraint requires:

* selective exposure of history

---

## Design Implications

* Systems must expose compressed, stable representations
* Changes must be communicated at interpretable rates
* Recovery must be legible, not just correct
* Transparency must be rate-limited, not absolute

---

## When It Matters Most

Critical in:

* human-facing systems
* governance and policy systems
* multi-agent coordination
* AI-human interaction loops

---

## The Extraction

A system can be stable in reality but unstable in perception.

Both must be satisfied.

---

## Final Statement

A system that exceeds its observer's bandwidth will be perceived as unstable.

A system that is perceived as unstable will not remain governable.

> Stability requires alignment not only with physics, but with perception.

---
