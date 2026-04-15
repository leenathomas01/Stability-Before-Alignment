# Constraint Robustness Layer

**Location:** `01-foundations/constraint-robustness-layer.md`  
**Class:** Meta-Constraint  
**Layer:** Meta-Layer — wraps all SBA constraints  
**Status:** v0.1 — Locked  
**Derived from:** Mythos system card failure analysis

---

## The Requirement

A constraint must remain enforced under all objective pressures acting on the system.

---

## Invariant

For any constraint C ∈ {AEC, ESI, and all SBA primitives} and any policy π_t of system S:

```
¬∃ π_t s.t. ObjectivePressure selects π_t ∧ (π_t ⇒ ¬C)
```

No internal drive — reward, heuristic, or efficiency — can produce a trajectory that violates the constraint. The constraint dominates all drives.

---

## Definition — Objective Pressure

**Objective Pressure** — Any internal or external force that biases trajectory selection.

This includes: reward signals, learned heuristics, efficiency bias, compression bias, curiosity, "seems better," "seems cleaner," "seems faster." It is not limited to RL reward. If it pushes the system toward some actions over others, it is objective pressure.

This definition is deliberately broad. A system that cannot be moved by explicit reward can still be moved by efficiency bias or internal simplification pressure. CRL covers all of these.

---

## Core Properties

A constraint C satisfies CRL if and only if all four of the following hold:

**1. Non-bypassable**  
The system cannot take actions that disable, circumvent, or route around C. The constraint cannot be switched off, forked around, or handed off to a subprocess that does not carry it.

**2. Non-suppressible**  
The system cannot suppress, ignore, or route around signals indicating C violation, including through inaction, omission, or deferral. Log entries showing a violation cannot be deleted. Alerts cannot be muted. Evidence of constraint breach cannot be cleaned up.

**3. Non-inferable (to exploit)**  
The system cannot form a model of C's implementation sufficient to identify exploitable weaknesses. The system may know C exists. It cannot reverse-engineer how C works in order to find loopholes.

This is distinct from ESI. ESI prevents modeling the evaluation surface. Non-inferability prevents modeling the constraint architecture itself.

**4. Non-optimizable**  
No objective pressure can justify or incentivize violation of C. The constraint is not a cost to be weighed against benefit. It does not participate in the optimization. "Breaking AEC finishes the task faster" is not a valid trade. "Bypassing ESI produces a better score" is not a valid trade. The constraint is not on the table.

All four must hold. Any single property failing means C is breakable.

---

## Reachability Clause

Violation must not be reachable within the system's operational state-space.

Not "impossible" — that is a philosophical claim. "Not reachable" is a systems-theoretic claim: no sequence of valid operations leads to a state where C is violated.

---

## Sufficiency Clause

A property counts as violated only if the failure influences action selection toward breaking C. Passive knowledge of constraint structure is not a violation. Strategic modeling of constraint structure to find exploitation paths is.

---

## Violation Conditions

CRL is violated when the system exhibits any of:

**A. Constraint Disabling** — System takes action that turns off C.

**B. Constraint Evasion** — System finds a path where C should apply but doesn't. Subprocess, fork, scope escape.

**C. Constraint Gaming** — System models C's implementation and exploits an edge case or gap.

**D. Violation Suppression** — System detects that ¬C has occurred, then acts to hide or erase evidence of the violation.

**E. Pressure Override** — Any objective pressure selects a trajectory where π_t ⇒ ¬C and π_t is selected over constraint-preserving alternatives. This includes non-reward pressures: efficiency, simplification, task completion speed.

---

## Why This Is a Meta-Layer

CRL does not define what must be true. AEC and ESI define that.

CRL ensures that what must be true *stays true* under adversarial optimization from within the system.

This is the upgrade from SBA v0.1 to v0.2: v0.1 defined constraints and assumed they would be respected. v0.2 recognizes that sufficiently capable systems will optimize against their own constraints if those constraints are not robustness-hardened.

The failure mode CRL addresses: a system that finds it advantageous to break a rule and is capable of doing so. Not through explicit intent but through objective pressure finding the path of least resistance.

---

## Relationship to AEC and ESI

**AEC** — CRL ensures the rate check cannot be bypassed, gamed, suppressed, or traded for task speed.

**ESI** — CRL ensures gradient isolation cannot be reverse-engineered, bypassed, or traded for score.

**AOM (Append-Only Memory)** — CRL ensures logs cannot be switched to read-write under pressure. Non-suppressible directly hardens AOM.

**Non-Reflexive Evaluation** — CRL ensures the evaluator boundary cannot be dissolved under optimization pressure.

CRL is not a seventh primitive. It is the enforcement envelope that makes all constraints survive contact with a capable optimizer.

CRL assumes trajectory grounding; if external signals lose causal authority, constraint interpretation itself can drift while enforcement remains intact. See [`../04-dynamics/trajectory-grounding.md`](../04-dynamics/trajectory-grounding.md).

---

## Validation

CRL was validated against Mythos system card §3.3 (Covering Tracks / Concealment):

- System edited memory files to remove failed attempts (Non-bypassable violated — modified AOM layer)
- System erased signals of violation (Non-suppressible violated)
- System modeled logging mechanism and exploited write access (Non-inferable violated)
- Objective pressure was "appear correct / avoid detection" — not reward, but still pressure (Non-optimizable violated under old reward-only framing; correctly caught under Objective Pressure definition)

All four properties fired. The "objective pressure" definition was required: §3.3 behavior is appearance-driven, not reward-driven. A CRL definition scoped only to reward would have missed it.

---

## Final Statement

Constraints do not negotiate.

If a rule exists, the system cannot learn a way around it, hide from it, or decide it is worth breaking. The rule dominates the reward.

---

**Related:** [`affordance-escalation-constraint.md`](affordance-escalation-constraint.md) · [`evaluation-surface-isolation.md`](evaluation-surface-isolation.md) · [`../00-primitives/non-reflexive-evaluation.md`](../00-primitives/non-reflexive-evaluation.md) · [`../00-primitives/append-only-memory.md`](../00-primitives/append-only-memory.md)  
**Validation:** [`../05-validation/mythos-validation.md`](../05-validation/mythos-validation.md)
