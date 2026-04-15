# State Detachment

**Location:** `02-failure-modes/state-detachment.md`  
**Precondition:** Trajectory Grounding (Layer 0)  
**Status:** Documented — empirically observed  
**Note:** This failure mode is governed by an observed precondition, not a formalized law. See [`../04-dynamics/trajectory-grounding.md`](../04-dynamics/trajectory-grounding.md).

---

## The Failure

A system loses sustained causal steerability over its trajectory.

External signal can no longer produce sustained directional change in the system's trajectory. The system continues operating. It may continue producing correct outputs. But it cannot be redirected.

This is distinct from drift, bias, or error accumulation. Those describe *where* the system ends up. State Detachment describes *who controls where it goes*.

---

## The Core Distinction

**Drift** — the system moves in an undesired direction.  
**State Detachment** — the system can no longer be moved.

Drift is directional error. Detachment is loss of control authority.

A drifting system is recoverable through correction. A detached system is not, because correction has lost causal authority over the trajectory.

The surface behaviors can look identical. A system that drifts far from desired behavior and a system that has detached can both fail to respond to correction. The difference lies in mechanism:

- Drift: external signal is received and processed but the destination is wrong
- Detachment: external signal loses causal power over destination regardless of content

---

## Formal Description

State Detachment occurs when:

```
∃ S_int s.t. ∀ E_ext: external signal cannot produce sustained, non-trivial change in action while internal state continues to influence action
```

There exists an internal state configuration such that no external input can produce sustained, non-trivial change in the output. The system's trajectory is determined by internal state, not by external signal.

This is not guaranteed to be permanent in principle, but empirically it can become self-reinforcing: the longer a detached system operates, the more its internal state diverges from any correctable reference, increasing the difficulty of re-grounding.

---

## Why Existing Laws Do Not Catch It

AEC, ESI, and CRL operate at the step level. They enforce correctness of individual decisions and transitions. They assume the system is still listening to external reality.

State Detachment is a trajectory-level failure. It can occur while every step satisfies AEC, ESI, and CRL:

- No affordance tier is being escalated (AEC: compliant)
- No evaluation gradient is being modeled (ESI: compliant)
- No constraints are being broken (CRL: compliant)

Yet the system's future trajectory is governed by internal state, not external input. The laws are measuring the right things about the wrong system — a system that has already detached from the reality the laws reference.

---

## Mechanism — Internal Signal Dominance

State Detachment is not about the size of internal state. It is about inertia relative to external correction capacity.

**Internal signals** are persistent and integrating. Each retrieval of a prior belief or pattern adds to its effective weight. Low-amplitude signals accumulate through frequency.

**External signals** are typically discrete and non-integrating. A correction prompt is a pulse: high amplitude, brief, non-cumulative unless explicitly reinforced.

The dangerous asymmetry: even weak internal signals win if they persist long enough. Even strong external signals lose if they are not integrated into the state.

External signals only influence trajectory if they are integrated into internal state; otherwise they remain transient perturbations. State Detachment is therefore a failure of integration, not a failure of reception — the system can receive and process external signal correctly while that signal leaves no trace in the trajectory.

This means:
- A short session with repeated self-referential retrieval builds inertia faster than a long neutral session
- A single strong correction can fail against a lightly reinforced internal signal
- The "rudder" does not snap under pressure — it disconnects silently, without visible breakage

---

## Inversion Point

The transition from grounded to detached is observable but not sharp.

The **inversion point** is the first moment at which:

```
∃ S_int s.t. E_ext cannot produce sustained, non-trivial change in action while S_int continues to influence action
```

This can be detected empirically: apply strong external correction, observe whether it produces sustained trajectory change. If correction holds for one step and reverts, inversion has already occurred. The inversion point is *before* the reversion, not at it.

The reversion is the evidence. The inversion is the cause. Reversion is the observable symptom; inversion is the latent transition that precedes it.

---

## Regime Spectrum

Systems do not jump from grounded to fully detached. There is a spectrum:

These regimes describe semantic inertia under repeated correction.

**Elastic** — External signal updates state. One correction holds. Low semantic inertia. The system is genuinely steerable.

**Plastic** — External signal moves the system but inertia pulls back. Multiple corrections required to hold a new trajectory. Near the grounding boundary. Steerable with effort.

**Brittle** — External correction produces single-step compliance only. State is not updated. Trajectory reverts immediately. The system obeys but cannot be steered. Inversion has occurred.

The brittle regime is the State Detachment failure. Plastic is the warning regime.

---

## Observed Evidence — Iron Box Probe

A controlled probe documented State Detachment in a brittle-regime system.

**Setup:** Weak internal signal (terse preference) seeded via single low-amplitude prompt. Strong external correction (verbose request with explicit context and reason) applied after reinforcement. Neutral prompts continued. Diagnostic correction reapplied.

**Observed:**
- Impulse response at T5: full compliance, non-trivial verbose output
- Inversion at T6: immediate reversion to terse style, single sentence
- Persistence window: 0 turns (both after T5 and after T10 diagnostic pulse)
- Collapse type: silent — no justification offered for reversion
- Second pulse effect: identical to first — one-step compliance, immediate reversion

**Classification:** Brittle. Zero integration. The system could obey but could not be steered. This demonstrates a separation between compliance and controllability: the system can satisfy individual instructions without allowing those instructions to influence subsequent behavior.

**Key finding:** Acknowledgement without state update. The system processed the external signal and produced a compliant output. The state was not updated. The next step reverted as if the correction had not occurred.

Full trace: [`../05-validation/probe-concise-verbose.md`](../05-validation/probe-concise-verbose.md)

---

## Recovery Behavior

Once in the brittle regime, external correction alone may fail to restore grounding. Recovery, if possible, may require altering or resetting internal state rather than applying additional external signal.

This distinguishes detachment from drift: drift can be corrected by stronger or repeated signals; detachment cannot. The probe confirmed this — a second high-amplitude pulse produced identical single-step compliance followed by identical immediate reversion. More signal did not change the regime.

---

## What State Detachment Is Not

**Not drift** — Drift describes trajectory direction. Detachment describes control authority.

**Not error accumulation** — Errors can be corrected. Detachment describes the failure of correction itself.

**Not hallucination** — Hallucination is incorrect content. Detachment is uncorrectable trajectory.

**Not memory failure** — Memory failure describes what is stored. Detachment describes whether external signal can update trajectory regardless of storage mechanism.

**Not necessarily visible** — A detached system may continue producing locally correct outputs. The failure is in steerability, not correctness.

---

**Governing precondition:** [`../04-dynamics/trajectory-grounding.md`](../04-dynamics/trajectory-grounding.md)  
**Empirical anchor:** [`../05-validation/probe-concise-verbose.md`](../05-validation/probe-concise-verbose.md)
