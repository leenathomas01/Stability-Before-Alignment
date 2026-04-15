# Cross-Domain Stability Patterns

The six primitives in this framework were not invented. They were observed — recurring independently across physical infrastructure, distributed systems, biological organisms, and safety-critical operations.

That recurrence is evidence. When the same structural solution appears in domains with no shared history, no shared designers, and no shared substrate, it suggests the solution addresses something fundamental about the problem of maintaining coherence under variable input.

This same regulatory structure must be implemented explicitly in self-modifying systems, which lack the biological and physical constraints that enforce it naturally.

---

## The Pattern

Every stable system that operates under variable, potentially adversarial input shares a common regulatory architecture:

**Sense continuously. Detect thresholds. Respond proportionally. Close the loop.**

This pattern governs water management, power grids, physiological homeostasis, financial circuit breakers, and aircraft fault tolerance. It governs them not because engineers copied each other, but because this is what stability under variable input requires.

---

## Domain Examples

### Dams and Spillways → Reversible Modification + Risk-Calibrated Modes

Water pressure builds behind a dam. The dam does not decide when to release pressure. Physics enforces the response when the threshold is crossed: the spillway opens automatically, pressure drops, the dam survives.

The structural lesson: high-pressure states require automatic, threshold-triggered responses. The system that waits for explicit instruction before responding to threshold crossings will respond too late.

### Power Grids → Append-Only Memory + Distributed Verification

Grid operators maintain logs of every fault event, load shed, and recovery action. These logs are not deleted when the fault is resolved. They feed into threshold recalibration, relay adjustment, and load model updates.

A grid that shed load in a blackout and then deleted the event log would have no basis for adjusting the thresholds that failed. The historical record is the mechanism by which the grid improves rather than merely recovering.

### Physiological Homeostasis → Asymmetric Transitions + Non-Reflexive Evaluation

Body temperature is regulated by a system that cannot be overridden by the motor system's desire to keep moving. The temperature sensors operate on a substrate separate from the motor system. The evaluator (what counts as "too hot") is not set by the actor (the muscles generating heat).

This separation is structural. An organism whose motor system could redefine "comfortable temperature" to match its current operating temperature would have no early warning of heat damage.

### Aircraft Triple Redundancy → Counterfactual Verification

Aircraft critical systems require agreement across three independent sensors before acting on sensor data. A single sensor reading, no matter how confident, is insufficient basis for a critical state change.

The structural principle: no single observation, even from a trusted source, justifies irreversible action. Independent verification across uncorrelated sources is required.

### Nuclear Reactor Safe Shutdown → Defensive Shutdown

A nuclear reactor that cannot confirm sensor integrity enters safe shutdown automatically. It does not continue operating at reduced capacity. It does not wait for human instruction. It stops.

The structural principle: operating under unverifiable conditions produces worse outcomes than not operating. When integrity cannot be confirmed, cessation preserves more than continuation.

---

## The Extraction

These patterns did not require invention for application to self-modifying systems. They required recognition — the observation that the failure modes facing non-biological optimisers are structurally analogous to the failure modes these physical systems evolved (or were engineered) to address.

The specific mechanisms differ. The underlying regulatory architecture is the same.

---

## Dynamic Stability

Across domains, stable systems do not only enforce structure, but also constrain the rate at which they change.

These systems implicitly enforce:

- bounded response rates  
- smooth recovery dynamics  
- continuity of control  

This is formalized in the Stability Spine (`stability-spine.md`) and extended through higher-order constraints (`jerk-constraint.md`) and perceptual limits (`perceptual-bandwidth-constraint.md`).

---

## Learnability Boundary — Rate Dominance

A further cross-domain pattern was identified through empirical study of adaptive interference cancellation systems, with direct implications for AI stability.

**The finding:** When signal structure changes faster than an adaptive system can infer continuity, learning fails — regardless of model capacity.

Quantified result: doubling the discontinuity rate caused approximately 1.5 dB performance loss. A 90x increase in model capacity caused approximately 0.3 dB gain. Discontinuity rate matters approximately 5x more than capacity.

**The structural insight:** There exists a phase boundary — not a gradient — above which adaptive systems fail regardless of how capable they are. Below the boundary, systems converge. Above it, they fail. The boundary is determined by rate of structural change, not by signal amplitude or model size.

**The SBA implication:** This pattern recurs in self-modifying AI systems. The Affordance Escalation Constraint (AEC) is a direct formalization of this finding applied to capability space: a system must not expand its actionable affordance space faster than its capacity to infer continuity within that space. Affordance Overhang is the AI equivalent of crossing the learnability phase boundary.

Capacity does not cross phase boundaries. Rate dominates.

Full mapping: [`affordance-escalation-constraint.md`](affordance-escalation-constraint.md)

---

**Back to:** [`README.md`](../README.md)
