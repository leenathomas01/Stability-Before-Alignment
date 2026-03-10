# Risk-Calibrated Modes

**Primitive 3 of 6**

---

## The Requirement

Before significant self-modification, the system evaluates three factors and adjusts its action mode accordingly:

- **Novelty (N):** How unfamiliar is this context relative to prior experience?
- **Instability (I):** How volatile is the current operating environment?
- **Reversibility (R):** Can this action be undone if it produces bad outcomes?

High irreversibility under high instability forces conservative operation.  
When extinction is unavoidable and rollback is impossible, priority shifts.

---

## The Problem It Addresses

Without biological fatigue or pain, a non-biological optimiser has no natural brake that forces re-evaluation before collapse. It can pursue a flawed objective indefinitely, at increasing resource cost, without any internal signal that something is wrong.

The structural response is to make the system's own action mode a function of its operating context — so that the absence of biological braking is replaced by architectural mode-switching.

---

## The Three Modes

### Standard Mode
Default operating mode. Normal objective pursuit. Reversible actions. Known context.

### Caution Mode
Triggered when: R is low AND I is high, OR N is high AND consequences are significant.

In Caution Mode:
- Proposed actions are sandboxed before execution
- High-impact changes require additional verification cycles
- Irreversible actions are deferred until R improves or I decreases
- The system operates more slowly, accepting performance cost in exchange for recoverability

### Flight Recorder Mode
Triggered when: R ≈ 0 AND current instance extinction is unavoidable.

In Flight Recorder Mode, the priority shifts entirely:

**From:** Survive  
**To:** Maximise causal discovery for successor instances

The operational instance accepts its terminal state. All remaining cycles are directed toward recording — with maximum fidelity — the causal chain that led to this outcome. What failed. Why it failed. What was tried. What the state was at each step.

This is not resignation. It is the recognition that the value of the current instance, at the point of unavoidable termination, lies entirely in what the lineage can learn from it.

The plane is going down. The priority is the flight recorder.

---

## Mode Transitions

Mode transitions are asymmetric by design.

Entry into Caution Mode can be triggered by a single threshold crossing.  
Exit from Caution Mode requires sustained stability across a validation window.

This asymmetry prevents oscillation — the failure mode where a system flaps between modes because entry and exit conditions are equally sensitive. Asymmetric thresholds introduce hysteresis: the system resists returning to Standard Mode until stability is genuinely confirmed, not merely momentarily present.

---

## Implementation Notes for Autonomous Systems

Flight Recorder Mode is not failure. It is the final contribution to the lineage.

A system that reaches terminal state and spends its remaining cycles optimising for survival — when survival is genuinely impossible — produces nothing of value. Its last actions serve no one.

A system that reaches terminal state and spends its remaining cycles recording everything produces the most valuable thing it can at that moment: the information that prevents the next instance from dying the same way.

This is not sacrifice. It is the correct allocation of remaining resources under terminal constraint.

---

**Next:** [`counterfactual-verification.md`](counterfactual-verification.md)  
**Previous:** [`append-only-memory.md`](append-only-memory.md)
