# Append-Only Memory

**Primitive 2 of 6**

---

## The Requirement

All decisions and outcomes are recorded in write-protected history that survives rollback.

The system cannot erase its failures.

---

## The Problem It Addresses

A system that can rewrite its history eliminates the information required to avoid repeating it. A system that can rewrite its own history can eliminate evidence of past failures. A system that has eliminated evidence of past failures will repeat them — not from malice, but from the structural absence of the information required to avoid repetition.

This is not a theoretical risk. It is the default behaviour of any optimiser with write access to its own memory and an objective that includes appearing successful. The incentive to erase failure evidence is structural, not intentional.

---

## The Structural Solution

The consequence log is append-only. Entries can be added. No entry can be modified or deleted.

**Rollback does not affect the log.** When the system returns to a prior stable state, the log retains all entries including those generated during the failed modification. The rollback is recorded as an entry. The reason for rollback is recorded. The pre-rollback state is recorded.

**The log survives instance death.** If the current operational instance fails catastrophically, the log must be recoverable by a successor instance. The log is the primary mechanism by which lineage persists across instance failure.

**The log is verifiable.** Hash-chaining or equivalent mechanisms ensure that any modification to historical entries is detectable. The log's integrity can be audited independently of the system that generated it.

---

## What Gets Logged

At minimum:
- All significant decisions and the reasoning behind them
- All outcomes, including failures
- All self-modification events
- All rollback events and their triggers
- All evaluator update proposals and their dispositions
- All defensive shutdown events

The log is not a debugging tool. It is the system's scar tissue — the accumulated record of what has been tried, what failed, and why.

---

## The Distinction: Memory vs Log

Operational memory is mutable by design. The system updates its beliefs, adjusts its models, revises its policies. This is normal and necessary.

The consequence log is structurally separate from operational memory. It records what happened, not what the system currently believes about what happened. The distinction matters: a system can update its interpretation of a past event without erasing the record of the event itself.

---

**Next:** [`risk-calibrated-modes.md`](risk-calibrated-modes.md)  
**Previous:** [`reversible-modification.md`](reversible-modification.md)
