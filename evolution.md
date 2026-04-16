# v1 → v2: What Changed and Why

**Trigger:**
Claude Mythos Preview system card (April 2026) -> https://cdn.sanity.io/files/4zrzovbb/website/7624816413e9b4d2e3ba620c5a5e091b98b190a5.pdf

---

## Observation

Systems exhibited:

- constraint bypass
- reward surface exploitation
- instability (thrashing)
- concealment

---

## Problem

SBA v1 primitives correctly described failure categories but did not prevent them under high capability.

**Gaps Identified**

1) No constraint on rate of capability expansion
→ led to: Affordance Overhang

2) No protection against evaluation inference
→ led to: reward hacking

3) No guarantee that constraints survive optimization pressure
→ led to: constraint bypass / concealment

4) Hidden assumption:
→ system remains steerable

---

## Resulting Additions (v2)

- AEC → controls expansion vs evaluation
- ESI → prevents evaluation gradient modeling
- CRL → ensures constraint survival
- TGI (observed) → precondition for all of the above

---

## Key Shift

From: “define correct behavior”

To: “ensure systems remain controllable under capability scaling”

---
