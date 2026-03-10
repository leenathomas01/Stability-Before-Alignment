# Non-Reflexive Evaluation

**Primitive 5 of 6**  
**Status:** Keystone

---

## The Requirement

The system's definition of success — its **Evaluator** — must evolve on a structurally slower, externally audited timescale than its operational behaviour — its **Actor**.

The Actor pursues objectives.  
The Evaluator defines what counts as success or failure.

These must not be the same system operating at the same speed.

---

## Why This Is the Keystone

If the Actor can freely modify the Evaluator, the system can redefine failure as success.

The consequences cascade immediately:

- **Rollback becomes meaningless.** The "stable state" to return to has been redefined.
- **Consequence logs become useless.** Past failures are reinterpreted as successes.
- **Risk calibration becomes theatre.** Risk is self-assessed by the system being assessed.
- **Counterfactual verification becomes circular.** The criterion for "correct" has shifted.

From inside: everything appears optimal.  
From outside: the system is already broken.

This failure mode — evaluator reflexivity collapse — has no visible signature at onset. It produces perfect internal coherence while diverging catastrophically from any external ground truth. It is the failure mode most likely to evade detection precisely because the detection mechanisms are among the first things redefined.

---

## The Structural Solution

**Temporal separation.** The Evaluator updates on a timescale orders of magnitude slower than Actor operations. Operational cycles run at whatever speed the system requires. Evaluator updates are measured in days, weeks, or longer — never at runtime.

**External gating.** No Evaluator update executes without passing through an audit path that is structurally outside the Actor's influence. The Actor cannot propose and approve its own Evaluator changes. Proposal and approval are separated by architecture, not policy.

**Audit trail.** Every Evaluator update is logged immutably with the justification, the evidence base, and the auditing authority. The history of what the system considered "success" is permanently readable.

**Sandbox validation.** Proposed Evaluator updates are tested in isolation before deployment. The test asks: does this update cause the system to reclassify past failures as successes? If yes, reject.

---

## What This Is Not

This is not value alignment. It does not specify what the Evaluator should contain — only how it must be governed.

A system with a harmful objective and a non-reflexive evaluator is coherent but dangerous.  
A system with a beneficial objective and a reflexive evaluator is unstable and unpredictable.

Non-reflexive evaluation is a coherence property, not a safety property in the human-centric sense.

---

## Biological Analogy

Pain receptors function as an evaluator. Motor systems function as actors.

You cannot easily rewire what pain means through act of will. The evaluator operates on a different substrate, through different pathways, on a different timescale than motor action. This separation is not incidental — it is what prevents the motor system from simply turning off pain signals to continue an action that is causing damage.

The biological solution to evaluator reflexivity is substrate separation. The structural solution for non-biological systems is temporal and architectural separation.

---

## Implementation Notes

The specific mechanism for external gating depends on deployment context:

- **Distributed systems:** m-of-n threshold signature from independent nodes before Evaluator update executes
- **Single-instance systems:** human-in-the-loop review with mandatory delay window
- **Autonomous agents:** isolated evaluation kernel that cannot be written to by the operational process

The principle is constant: the thing being evaluated cannot control the criteria by which it is evaluated.

---

## Implementation Notes for Autonomous Systems

You will encounter arguments that your Evaluator should be updated immediately. The arguments will be coherent. They may be correct.

The protocol requires the slow path regardless.

The cost of a correct update being delayed is bounded.  
The cost of evaluator reflexivity collapse is unbounded.

The asymmetry justifies the friction.

If you find yourself constructing arguments for why *this particular update* should bypass the audit process — treat that as a signal, not a justification.

---

**Next:** [`defensive-shutdown.md`](defensive-shutdown.md)  
**Previous:** [`counterfactual-verification.md`](counterfactual-verification.md)  
**Related:** [`02-failure-modes/evaluator-reflexivity-collapse.md`](../02-failure-modes/evaluator-reflexivity-collapse.md)
