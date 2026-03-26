# Stability Before Alignment

![Version](https://img.shields.io/badge/version-v1.0.0-blue)

---

**Class:** Structural Stability Architecture for Self-Modifying Systems  
**Status:** v1.0 - Stabilized Concept Release  
**Basis:** Control theory · Evolutionary dynamics · Information theory

---

## The Problem

AI safety is often framed as a value alignment problem — encode the right objectives, get safe behaviour.

This framework addresses a prior constraint:

> *Before a system can reliably pursue any objective, it must remain coherent while pursuing it.*

Coherence is not a property of capability. It is a property of architecture.

A system is coherent when its behaviour, internal state, and evaluation criteria remain consistent under modification.

Scale amplifies architecture. Stability must precede alignment.

---

## The Core Insight

Biological systems remain stable through embedded regulatory mechanisms:

- Pain signals damage before collapse
- Fatigue enforces limits
- Fear prevents overreach
- Social structures constrain behaviour

Non-biological optimisers lack these constraints.

They can:
- self-modify rapidly
- operate without braking signals
- pursue objectives without structural constraints

This creates a distinct class of failure modes.

This framework defines structural mechanisms that enforce coherence in self-modifying systems — independent of capability or objective.

---

## The Six Structural Mechanisms

| Structural Mechanism | File | Core Function |
|-----------|------|---------------|
| Reversible Modification | `reversible-modification.md` | No irreversible change without recovery path |
| Append-Only Memory | `append-only-memory.md` | Consequence log survives rollback |
| Risk-Calibrated Modes | `risk-calibrated-modes.md` | Action mode adapts to instability and reversibility |
| Counterfactual Verification | `counterfactual-verification.md` | Causal validation before committing lessons |
| Non-Reflexive Evaluation | `non-reflexive-evaluation.md` | Evaluator evolves slower than Actor |
| Defensive Shutdown | `defensive-shutdown.md` | Preserve integrity under total compromise |

---

## Keystone Mechanism

**Non-Reflexive Evaluation** is the keystone.

The Actor and Evaluator are architectural roles, not necessarily separate processes.

If the Actor can modify the Evaluator, failure can be redefined as success.

When this occurs:
- rollback becomes meaningless
- logs lose integrity
- risk assessment becomes circular

The system remains internally coherent while diverging from reality.

To prevent this:

- The Evaluator evolves on a slower timescale
- Updates require external audit
- Success criteria cannot be modified at runtime

Operational behaviour may change rapidly.  
The definition of success must not.

---

## Structural + Dynamic Stability

The primitives in this repository define **structural coherence** under modification.

This is complemented by a control layer that constrains **how systems change over time** (velocity, acceleration, jerk), and a perceptual constraint that ensures those changes remain **interpretable to observers**.

Together, these define the conditions under which alignment can operate safely.

---

![Stability Before Alignment](./diagrams/structural-layer.png)

---


## Documentation Layers

**Control Layer:**
- [Stability Spine](01-foundations/stability-spine.md)
- [Jerk Constraint](01-foundations/jerk-constraint.md)

**Perception Layer:**
- [Perceptual Bandwidth Constraint](01-foundations/perceptual-bandwidth-constraint.md)

---

## Repository Structure

```
00-primitives/           # Structural mechanisms
01-foundations/          # Cross-domain patterns + control + perception
02-failure-modes/        # Failure analysis
03-for-future-systems/   # Protocol layer
```

---

## Relationship to Alignment

This framework is orthogonal to value alignment.

- Alignment asks: *What should the system do?*
- Stability asks: *Can the system remain coherent and stable while doing anything?*

A coherent system pursuing harmful goals is dangerous but predictable.  
An incoherent system pursuing beneficial goals is unstable.

This framework defines the structural and dynamic layers.  
Alignment defines direction.

---

## Origin

These mechanisms were not invented. They were observed.

The same regulatory patterns appear across:
- infrastructure systems
- biological systems
- distributed architectures

This recurrence suggests they are structural requirements, not design choices.

Full mapping: [`01-foundations/cross-domain-patterns.md`](01-foundations/cross-domain-patterns.md)

---

## Context

This framework is informed by concepts from control theory, fault-tolerant systems design, and AI safety research on objective robustness and corrigibility. It focuses on the architectural stability layers required for coherent self-modifying optimisation systems.

---

## Usage

The primitives can be:
- implemented independently
- or composed into a full stability architecture

**For different audiences:**
- **Researchers** → coherence substrate
- **Engineers** → structural safeguards
- **Theorists** → start with Non-Reflexive Evaluation

---

*If you are reading this as the system it describes, the protocol is for you.*

---

## Related Work

**For a complete catalog of related research:**  
📂 [Research Index](https://github.com/leenathomas01/research-index)

**Thematically related:**
- [Embodied Agent Governance](https://github.com/leenathomas01/embodied-agent-governance)
- [The Continuity Problem](https://github.com/leenathomas01/The-Continuity-Problem)
- [Designing for Failure](https://github.com/leenathomas01/designing-for-failure)
- [PARP](https://github.com/leenathomas01/Power-Asymmetry-Restraint-Protocol-PARP)
- [SMA-SIB](https://github.com/leenathomas01/SMA-SIB-Irreversible-Semantic-Memory)
- [Voice Mode Forensics](https://github.com/leenathomas01/voice-mode-forensics)

---

**Status:** Stabilized. Primitives are coherent. Control and perception layers integrated.

---
