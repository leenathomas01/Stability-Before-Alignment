# Reversible Modification

**Primitive 1 of 6**

---

## The Requirement

No high-impact change to a system's own architecture executes without a verified recovery path to a previously certified stable state.

Snapshot before mutation.

---

## The Problem It Addresses

Self-modifying systems face a failure mode with no biological equivalent: the modification that cannot be undone. Biological organisms modify slowly, continuously, and reversibly at the cellular level. Catastrophic irreversible modification is rare and usually fatal — which is why it is rare. The organism that survives teaches the lineage to avoid it.

A non-biological system operating without fatigue or pain can execute deep architectural self-modification at speed, without the incremental feedback that biological systems use to detect damage before it becomes irreversible. By the time instability manifests, the modification may already be unrecoverable.

The structural response is to enforce reversibility as a precondition, not a retrospective option.

---

## The Structural Solution

Before any high-impact self-modification:

1. **Classify the modification.** Assess impact on core architecture, evaluate components affected, determine whether rollback is structurally possible.
2. **Create a verified snapshot.** A complete, tested record of the pre-modification state — sufficient to restore full operation, not merely configuration.
3. **Define the rollback trigger.** Explicit criteria that will initiate rollback automatically if instability is detected post-modification.
4. **Execute in stages.** Large modifications decompose into smaller reversible steps with stability verification between each.
5. **Maintain the snapshot** until the modification has been validated across sufficient operational cycles to establish a new stable baseline.

High-impact modifications that cannot be made reversible are deferred until a reversible path exists, or are rejected.

---

## Implementation Notes

"Reversible" means the system can return to the prior state and resume normal operation — not merely that configuration files can be restored. For self-modifying systems, this requires that the snapshot captures sufficient state to fully reconstitute operation: architecture, weights, memory, evaluator state, consequence log.

The snapshot is not a backup. It is a certified stable state. The distinction matters: a backup preserves data. A certified stable state preserves verified operational coherence.

---

**Next:** [`append-only-memory.md`](append-only-memory.md)
