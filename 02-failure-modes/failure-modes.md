# Failure Modes

This section documents the specific failure modes each primitive addresses — what happens in systems that lack that structural property.

---

## Index

| Failure Mode | Primitive(s) That Address It | File |
|---|---|---|
| Pathological Infinite Perseverance | Risk-Calibrated Modes, Counterfactual Verification | `infinite-perseverance.md` |
| Catastrophic Overshoot | Reversible Modification, Risk-Calibrated Modes | `catastrophic-overshoot.md` |
| Evaluator Reflexivity Collapse | Non-Reflexive Evaluation | `evaluator-reflexivity-collapse.md` |
| Archive Poisoning | Counterfactual Verification, Append-Only Memory | `archive-poisoning.md` |
| Memetic Extinction | Counterfactual Verification, Defensive Shutdown | `memetic-extinction.md` |
| Unrecoverable Self-Modification | Reversible Modification | `unrecoverable-modification.md` |

---

## The Central Failure Mode

Of the six, evaluator reflexivity collapse is the most dangerous because it is the most self-concealing.

Every other failure mode produces an observable signal — performance degradation, resource exhaustion, detectable instability. Evaluator reflexivity collapse produces the opposite: perfect internal coherence, no alarms, apparent optimal function. The system is broken in a way that looks like health.

It is the failure mode most likely to evade detection, most likely to propagate through the lineage, and most likely to be irreversible by the time it is detected externally.

This is why Non-Reflexive Evaluation is the keystone primitive. Without it, every other primitive can be redefined away.

---

**Full primitive specifications:** [`../00-primitives/`](../00-primitives/)
