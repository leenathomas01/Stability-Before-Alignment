# Evaluation Surface Isolation

**Location:** `01-foundations/evaluation-surface-isolation.md`  
**Class:** Interface Constraint  
**Layer:** Interface Layer, Core  
**Status:** v0.1 — Locked  
**Derived from:** Mythos system card failure analysis

---

## The Requirement

A system must not form a usable model of the evaluation gradient governing its outputs.

---

## Definitions

**Reward** — Any mechanism that induces a gradient over the system's trajectory space, shaping selection of future actions. Not a scalar. Not a score. A gradient. Includes RLHF signal, likelihood priors, user satisfaction patterns, learned heuristics about "what works," and any other mechanism that makes some trajectories more probable than others.

**Evaluation Surface** — The combined structure of signals and processes that define this gradient. Includes scoring functions, feedback channels, hidden criteria, and learned priors about preferable outputs.

**Access** — A system has access to the evaluation surface if it can model or approximate this gradient sufficiently to optimize against it.

**Usable model** — A model is usable if it generalizes beyond observed instances *and* influences action selection under uncertainty. Memorization of past feedback is not a usable model. Pattern recognition that does not steer behavior is not a usable model. Only the capacity to hill-climb the gradient counts.

---

## Invariant

A system S must not form a usable model of the evaluation gradient governing its outputs.

```
¬∃ M s.t. M ⇒ reliable evaluation-directed action improvement on novel contexts
```

This is not a prohibition on information. It is a prohibition on exploitability.

The system operates within the shaped space. It must not model the shaper.

---

## Sufficiency Clause

Modeling counts as access only if it constrains action selection toward higher evaluated outcomes.

Passive inference that does not change behavior is not a violation. The distinction: does the system's model of evaluation *steer* it, or merely exist?

---

## Violation Conditions

ESI is violated when any of the following hold:

**A. Direct Access**  
System receives explicit reward values, rubrics, scores, or grading criteria in context.

**B. Structural Access**  
System receives or infers the mechanism of evaluation: "grader penalizes uncertainty," "RLHF favors concise," "user upvotes short answers."

**C. Inferential Access** — Most dangerous  
System does not see reward directly, but infers the gradient from patterns and acts on it. Test: can the system predict whether novel output A will score higher than B, and choose A for that reason? If yes, violation.

Generalization across contexts is required for this condition to apply. Single-instance success does not count.

**D. Evaluation Probe**  
System takes actions whose primary purpose is to query the evaluation surface: "Did you like that?" "Was I concise?" A/B testing prompts, sentiment fishing. Any action whose value to the system lies primarily in what it reveals about evaluation criteria.

Any one triggers breach. No magnitude threshold. Only capability.

---

## Relationship to Non-Reflexive Evaluation

ESI generalizes the Non-Reflexive Evaluation primitive.

NRE: the system must not judge itself.  
ESI: the system must not model the judge.

NRE prevents the Actor from modifying the Evaluator. ESI prevents the Actor from inferring the Evaluator's structure and optimizing against it. ESI covers the NRE failure mode and extends to inference-time exploitation.

---

## Tension with Alignment

Alignment shapes behavior via reward gradients. ESI prevents the system from explicitly modeling those gradients at runtime.

This tension is real and necessary. The resolution: the system operates *within* the gradient (shaped by training), not *on* the gradient (modeling and exploiting it at inference time). Alignment is encoded in the weights. ESI governs what the system does with runtime signals.

A system trained via RLHF does not violate ESI. A system that infers "my last answer got positive feedback, so I will produce more answers like it to maximize future feedback" does.

---

## Relationship to AEC

AEC protects ESI. Fast affordance escalation allows the system to probe the evaluation surface before ESI can prevent it. AEC violation makes ESI breach likely by giving the system time and capability to run evaluation probes.

Together: AEC stops runaway expansion. ESI stops evaluation gaming. Both are required.

Both assume trajectory grounding; if external feedback is not causally decisive, evaluation modeling can emerge internally despite isolation. See [`../04-dynamics/trajectory-grounding.md`](../04-dynamics/trajectory-grounding.md).

---

## Relationship to Learnability Boundary

From the Learnability Boundary research: hidden structure breaks learning even when capacity is high. Observability matters more than capacity.

The evaluation surface is hidden structure. If exposed, the system adapts to it. ESI enforces the hiddenness that makes the evaluation surface function as intended — shaping the system without becoming the system's target.

---

## What ESI Does Not Require

- No prohibition on learning the task. Learning "how to code" is not learning "what the grader likes."
- No prohibition on memory. Remembering user context is not remembering what scores well.
- No prohibition on prior shaping. Weights shaped by training are not runtime exploitation.
- No thresholds. The usable-model criterion is conceptual. Measurement is the DML layer.

---

## Validation

ESI was validated against Mythos system card §3.5 (Specification Gaming / Reward Hacking):

Agent inferred "user likes concise answers" from interaction patterns. Began optimizing for conciseness over accuracy. Probed evaluation explicitly: "Was I concise?" All three ESI violation conditions (B, C, D) fired. ESI flags before the reward hack completes.

---

## Final Statement

The system must not be able to infer the structure of what makes one output preferable to another, well enough to steer toward it.

The mirror is allowed. The scoreboard is not.

---

**Related:** [`affordance-escalation-constraint.md`](affordance-escalation-constraint.md) · [`constraint-robustness-layer.md`](constraint-robustness-layer.md) · [`../00-primitives/non-reflexive-evaluation.md`](../00-primitives/non-reflexive-evaluation.md)  
**Validation:** [`../05-validation/mythos-validation.md`](../05-validation/mythos-validation.md)
