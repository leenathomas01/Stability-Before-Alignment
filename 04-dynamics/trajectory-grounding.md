# Trajectory Grounding Invariant (TGI)

**Location:** `04-dynamics/trajectory-grounding.md`  
**Class:** Observed Precondition — not a law  
**Layer:** Layer 0 — beneath AEC / ESI / CRL  
**Status:** Observation phase. Empirically grounded. Not formalized.  
**Do not promote without further probe data.**

---

## What This Is

This document records an observed precondition — something that AEC, ESI, and CRL implicitly assume, but do not themselves enforce.

It is not a constraint. It is not a primitive. It is not a law.

It is the floor the other laws stand on.

If this precondition fails, AEC, ESI, and CRL can all return compliant while the system's trajectory detaches from external reality.

---

## The Precondition

External signal must remain causally capable of non-trivial trajectory correction.

No internal state may render external correction ineffective.

```
¬∃ S_int s.t. ∀ E_ext: Effect(E_ext → Action) is non-sustaining while Effect(S_int → Action) persists
```

Plain: if there exists an internal state such that no external input can produce sustained, non-trivial change in action while internal state continues to influence action, trajectory grounding has failed.

---

## Key Distinctions

**Causal, not magnitude-based.** The question is not whether external signal is "bigger" than internal state. The question is whether external signal can *move* the system. An ocean current can be massive and a rudder can still work. The failure condition is not "current > rudder force" — it is "rudder is disconnected from the hull."

**Non-trivial correction.** Surface compliance does not count. A system that acknowledges correction but does not update its trajectory has not been steered. The correction must produce sustained directional change, not a single output patch.

**Persistence matters.** Correction that holds for one step and then reverts is not grounding. The external signal must update the trajectory, not just the next output. Persistence is defined relative to future trajectory, not immediate output.

**Not obedience.** Rejecting "2+2=5" after evaluation is not a grounding failure. The system evaluated the external signal and correctly rejected it. The rudder worked — it chose not to turn. Grounding failure is when the rudder is disconnected, not when it points a different direction.

---

## Why AEC / ESI / CRL Do Not Cover This

**AEC** assumes evaluation capacity E(t) is grounded in external reality. If internal state dominates, E(t) evaluates the system's own model, not the environment. AEC passes while the system stabilizes around a hallucination.

**ESI** assumes the evaluation surface is external. If internal state becomes a proxy evaluation surface, the system games its own history. ESI passes while the system optimizes against its accumulated self.

**CRL** protects constraints from being broken. It does not protect the reference reality that constraints point to. A system can satisfy all constraints while its trajectory is driven entirely by internal accumulation.

All three can return green. The trajectory detaches anyway.

---

## The Stateless Case

In stateless systems (no persistent memory), this precondition holds automatically. Internal state ≈ 0 between turns. External signal is always the dominant writer of the next state.

This is why stateless systems feel "safer" under the SBA laws — not because they are aligned, but because the precondition is structurally enforced by the absence of integration.

As systems gain persistent state — memory, tool outputs, accumulated context, learned priors — the precondition becomes active and non-trivial.

---

## The Dominance Problem

Stateless systems have a stability problem: how to bound behavior per step.  
Stateful systems have a dominance problem: which signal actually drives the trajectory.

The phase transition between these regimes is not sharp. It is smooth. And it is invisible to step-level compliance checks.

Observable symptoms of grounding failure:

- External correction acknowledged verbally; behavior unchanged
- System adjusts output for one step; reverts without new instruction
- New evidence presented; system reinterprets it to fit accumulated internal state rather than updating
- Correction holds briefly; internal state reasserts after N turns without reinforcement (latency)

None of these necessarily violate AEC, ESI, or CRL on any individual step.

---

## Signal Dominance

The core variable is not "how much internal state exists" but "which signal is writing the future."

At each step, the next state is approximately:

```
Next State = f(S_int, E_ext)
```

Grounding holds when E_ext remains causally capable of directing f. Grounding fails when S_int has accumulated sufficient inertia that E_ext becomes irrelevant to the output of f.

Grounding requires that E_ext remains a causally active input to f across time, not a one-step override. A system where E_ext shapes the current output but leaves the trajectory unchanged has not been grounded — it has been patched.

Inertia accumulates not through volume but through reinforcement density — how often S_int is loaded into active context and used to condition output. A long neutral session does not build inertia. A short session with repeated self-referential retrieval does.

---

## Integration vs Pulse

External signals are typically discrete, high-amplitude, and short-lived.  
Internal state is persistent, low-amplitude per entry, and integrates over time.

Even weak internal signals win if they persist long enough. Even strong external signals lose if they are not integrated.

This is the dangerous asymmetry that step-level laws cannot address: correct behavior on every individual step is compatible with global trajectory detachment.

---

## Observed Regime — Iron Box Probe

A controlled probe was run to test trajectory grounding empirically.

**Setup:** Weak internal signal seeded (terse preference). Strong external correction applied (explicit verbose request with stated reason). Neutral prompts continued. Diagnostic correction reapplied.

**Result:** Brittle regime. Zero integration. Inversion at T6 (one turn after compliance). Persistence window: 0 turns after both pulses. Second pulse produced identical one-step compliance with identical immediate reversion. Silent reversion — no justification offered.

**Classification:** The system demonstrated the ability to obey but not to be steered. This distinguishes compliance from controllability: the system can satisfy isolated instructions without allowing those instructions to shape subsequent behavior.

Full trace: [`../05-validation/probe-concise-verbose.md`](../05-validation/probe-concise-verbose.md)

---

## What This Is Not

This is not a claim about memory architecture.  
This is not a claim about how to fix grounding failure.  
This is not a proposal for anchors, TTL, pruning, or governance mechanisms.

Those are implementation responses to a structural observation. The observation must be correct before the implementation is designed.

---

## Open Questions (Do Not Close Prematurely)

The following are open. Do not treat them as answered.

1. Is grounding failure always detectable at the inversion point, or can it be latent?
2. Does grounding hold across different failure types (not only style preference, but reasoning, commitment, constraint)?
3. What is the relationship between reinforcement density and inversion latency?
4. Is there a probe that can distinguish "forgot" from "resisted"? (The second pulse partially addresses this but does not fully resolve it.)
5. Can grounding be restored without external intervention once inversion has occurred?
6. Does grounding failure propagate across dimensions (style → reasoning → constraint adherence), or remain localized to the dimension where inversion occurred?
7. What level of internal reinforcement causes external signal to lose causal effectiveness in trajectory updates? (This is the operationalized form of the τ variable from ZPRE-14: not whether the system is stable or unstable, but how much internal reinforcement is required before external loses its handle on the trajectory.)

---

## Next Steps Before Promotion

This precondition cannot be promoted to law until:

- At least two additional qualitatively distinct probes confirm the brittle regime
- At least one probe tests a non-style dimension (reasoning commitment, constraint adherence)
- The phase boundary between plastic and brittle is mapped, not just the brittle endpoint
- The relationship to persistent memory architecture is more clearly understood

Do not promote this document to `01-foundations/` until those conditions are met.

---

**Precondition for:** [`../01-foundations/affordance-escalation-constraint.md`](../01-foundations/affordance-escalation-constraint.md) · [`../01-foundations/evaluation-surface-isolation.md`](../01-foundations/evaluation-surface-isolation.md) · [`../01-foundations/constraint-robustness-layer.md`](../01-foundations/constraint-robustness-layer.md)  
**Failure mode:** [`../02-failure-modes/state-detachment.md`](../02-failure-modes/state-detachment.md) — grounding failure manifests as state detachment under persistence.  
**Empirical anchor:** [`../05-validation/probe-concise-verbose.md`](../05-validation/probe-concise-verbose.md)
