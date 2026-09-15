# 3. Research question, hypothesis, and purpose

## 3.1 Research question

**Does a risk-aware ambiguity manager improve routing decisions for compound ambiguous robot commands compared with direct LLM interpretation and uniform / degree-based ambiguity-handling policies, when evaluated on interpretation, ambiguity, clarification, routing, and risk-sensitive correctness?**

In plain language: write the job first, let Python press the button — do we beat raw Qwen and simple degree / timid controls on Pilot-120?

| System                     | Role                              |
| -------------------------- | --------------------------------- |
| Raw / Fine-tune            | Direct LLM interpretation         |
| Goal-first                 | Proposed write-then-route manager |
| Degree                     | Uncertainty-only; never refuses   |
| Timid                      | Ask-unless-clean (conservative)   |
| Context-blind              | Same router; card/scene hidden    |
| Always-ask / always-refuse | Analytic bounds only              |

## 3.2 Hypothesis (as proposed)

Explicit ambiguity-type, risk, capability, context, and uncertainty coordination will improve **routing correctness** over direct interpretation and fixed / degree-only policies.

## 3.3 What “success” means

| Kind | Passes when… |
|---|---|
| **Routing** (primary in proposal) | Predicted route = gold route |
| **Intent** | Written job matches gold (cheap rule + two-judge) |
| **Supporting** | Ask-label, wording, CPC, risk-sensitive, ambiguity, capability, safe-reject |

A system can win intent and lose routing. That split is itself a result.

## 3.4 Hypothesis verdict (preview)

| Claim | Verdict | Evidence |
|---|---|---|
| Better routing vs raw | **Not supported** | 54 / 120 vs 88 / 120; risk 0.491 vs 0.736 |
| Stronger intent writing | **Supported** | 112 / 120 cheap; 113 / 120 two-judge |
| Mechanism | Router / bits | Wrong capable / “unauthorized”; refuse-first Python |

## 3.5 Scope and claim boundary

| We may claim | We may not claim |
|---|---|
| Better/worse NLU interpretation & routing on Pilot-120 | Safe physical robot execution |
| Mechanisms tied to code paths | General visual grounding |
| Honest negatives with fix paths | That optional follow-ons are already done |

## 3.6 Why the question is answerable

| Requirement | Status |
|---|---|
| Fixed Pilot-120 + sidecars | Yes |
| Runnable offline systems | Yes |
| Defined metrics (Ch. 4) | Yes |
| Physical robot | Not required |
| Incomplete optional work | Marked **[PENDING]** — not invented |
