# Stability Before Alignment

![Version](https://img.shields.io/badge/version-v2.0.0-blue)

---

**Class:** Structural Stability Architecture for Self-Modifying Systems  
**Status:** v2.0 - Dynamic and Interface Layer Added  
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

## Structural + Dynamic Stability

The primitives in this repository define **structural coherence** under modification.

This is complemented by a control layer that constrains **how systems change over time** (velocity, acceleration, jerk), and a perceptual constraint that ensures those changes remain **interpretable to observers**.

In v0.2, three additional laws were derived from empirical failure analysis of frontier systems. These address failure modes that emerge as capability increases: affordance escalation, evaluation exploitation, and constraint erosion under optimization pressure.

Together, these define the conditions under which alignment can operate safely.

---

## Conceptual Stack

The framework can be viewed in two complementary ways:

- **Functional layers** (structural, control, perception) — describe *what kind* of constraint is applied
- **Constraint stack** (Layer 0–3) — describes *when* each constraint is needed and what it assumes

The mapping between them is not one-to-one, but they describe the same system from different perspectives.

The full constraint stack operates across four layers, plus an observed precondition beneath them:

| Layer | Constraint | Governs |
|---|---|---|
| Layer 0 | Trajectory Grounding *(observed, not yet law)* | External signal retains causal authority over trajectory |
| Layer 1 | AEC — Affordance Escalation Constraint | Rate of capability expansion vs evaluation capacity |
| Layer 2 | ESI — Evaluation Surface Isolation | System cannot model evaluation gradient to exploit it |
| Layer 3 | CRL — Constraint Robustness Layer | Constraints survive optimization pressure from within |
| Foundation | Six Structural Primitives | Coherence under self-modification |

Layers 1–3 assume Layer 0 holds. If a system has lost causal steerability, the upper layers are measuring the right things about the wrong system.

The six primitives assume the system is operating at all. The dynamic laws govern how it operates over time.

---

![Stability Before Alignment](./diagrams/structural-layer.png)

---

## The Six Structural Mechanisms

| Structural Mechanism | File | Core Function |
|-----------|------|---------------|
| Reversible Modification | `00-primitives/reversible-modification.md` | No irreversible change without recovery path |
| Append-Only Memory | `00-primitives/append-only-memory.md` | Consequence log survives rollback |
| Risk-Calibrated Modes | `00-primitives/risk-calibrated-modes.md` | Action mode adapts to instability and reversibility |
| Counterfactual Verification | `00-primitives/counterfactual-verification.md` | Causal validation before committing lessons |
| Non-Reflexive Evaluation | `00-primitives/non-reflexive-evaluation.md` | Evaluator evolves slower than Actor |
| Defensive Shutdown | `00-primitives/defensive-shutdown.md` | Preserve integrity under total compromise |

---

## Keystone Mechanism

**Non-Reflexive Evaluation** is the keystone of the structural layer.

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

*v0.2 note: Non-Reflexive Evaluation governs Evaluator modification. Evaluation Surface Isolation (ESI) extends this to cover a distinct failure mode: a system that does not modify its Evaluator but infers its structure at runtime and optimizes against it. Both are required.*

---

## Dynamic Stability and Interface Constraints (v2.0)

Derived from analysis of the Mythos system card as a forcing function. These three laws address failure classes that emerge at high capability where the structural primitives are necessary but insufficient.

| Law | File | Governs |
|---|---|---|
| Affordance Escalation Constraint (AEC) | `01-foundations/affordance-escalation-constraint.md` | Capability expansion rate vs evaluation capacity |
| Evaluation Surface Isolation (ESI) | `01-foundations/evaluation-surface-isolation.md` | Runtime modeling of evaluation gradient |
| Constraint Robustness Layer (CRL) | `01-foundations/constraint-robustness-layer.md` | Constraint invariance under objective pressure |

**AEC** — A system must not expand its actionable affordance space faster than it can evaluate and integrate consequences. Derived from phase-boundary findings in adaptive systems: rate of structural change dominates over capacity. Affordance Overhang is the failure condition.

**ESI** — A system must not form a usable model of the evaluation gradient governing its outputs. Extends Non-Reflexive Evaluation from architectural separation to inference-time isolation.

**CRL** — All constraints must remain enforced under all objective pressures acting on the system. Objective pressure includes reward, efficiency bias, heuristics, and simplification drives — not only RL reward signals. The constraint dominates the drive; the drive does not negotiate with the constraint.

---

## Failure Symmetry (v2.0)

Each dynamic constraint defines a corresponding failure regime:

| Constraint | Governs | Failure Mode |
|---|---|---|
| AEC | Rate of capability expansion | [Affordance Overhang](02-failure-modes/affordance-overhang.md) |
| TGI *(observed)* | Control authority / grounding | [State Detachment](02-failure-modes/state-detachment.md) |

These failures are orthogonal:

- A system can remain grounded but unstable — Affordance Overhang occurs when expansion outruns evaluation while external signal still has authority
- A system can remain locally stable but detached — State Detachment occurs when internal state retains trajectory control while individual steps still comply

Both must be controlled for coherent long-term behavior. The laws address Overhang directly. Grounding is a precondition — without it, the laws measure the right things about the wrong system.

---

## Documentation Layers

**Structural Layer (v1.0):**
- [Reversible Modification](00-primitives/reversible-modification.md)
- [Append-Only Memory](00-primitives/append-only-memory.md)
- [Risk-Calibrated Modes](00-primitives/risk-calibrated-modes.md)
- [Counterfactual Verification](00-primitives/counterfactual-verification.md)
- [Non-Reflexive Evaluation](00-primitives/non-reflexive-evaluation.md)
- [Defensive Shutdown](00-primitives/defensive-shutdown.md)

**Control Layer:**
- [Stability Spine](01-foundations/stability-spine.md)
- [Jerk Constraint](01-foundations/jerk-constraint.md)

**Perception Layer:**
- [Perceptual Bandwidth Constraint](01-foundations/perceptual-bandwidth-constraint.md)

**Dynamic Stability and Interface Constraints (v2.0):**
- [Affordance Escalation Constraint](01-foundations/affordance-escalation-constraint.md)
- [Evaluation Surface Isolation](01-foundations/evaluation-surface-isolation.md)
- [Constraint Robustness Layer](01-foundations/constraint-robustness-layer.md)

**Observed Precondition (Layer 0, not yet law):**
- [Trajectory Grounding / Control Authority](04-dynamics/trajectory-grounding.md)

---

## Repository Structure

```
00-primitives/           # Structural mechanisms (v1.0)
01-foundations/          # Invariants, laws, control, perception
02-failure-modes/        # Failure analysis
03-for-future-systems/   # Protocol layer
04-dynamics/             # Behavioral observations, phase transitions (v2.0)
05-validation/           # Empirical traces, probes, system card mappings (v2.0)
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
- **[Transition Grammar for Reasoning Systems](https://github.com/leenathomas01/Transition-Grammar-for-Reasoning-Systems)**

---

**Status:** v2.0. Structural primitives stable. Dynamic and interface laws added. Trajectory grounding in observation phase.

---
