# 3. Research question, hypothesis, and purpose

## 3.1 Research question

**Does a risk-aware write-then-route ambiguity manager improve intent correctness for compound ambiguous robot commands compared with direct LLM interpretation and uniform / degree-based ambiguity-handling policies, when evaluated primarily on intent writing and secondarily on ambiguity, clarification, routing, and risk-sensitive correctness?**

That is the same *shape* as the May proposal question, with one deliberate change of spotlight: **intent writing is primary**; routing and the other proposal metrics remain in the evaluation, but as supporting / secondary outcomes. In plain language: force a short job box, then let Python press the button — do we **name the gold job** more often than raw Qwen and the degree / timid / context-blind controls, and what happens to the button, ask behaviour, and risk-sensitive decisions under the same analysis?

| System | Role |
|---|---|
| Raw / Fine-tune | Direct LLM interpretation |
| Goal-first | Proposed write-then-route manager |
| Degree | Uncertainty-only; never refuses |
| Timid | Ask-unless-clean (conservative) |
| Context-blind | Same router; card/scene hidden |

## 3.2 Hypothesis

**Primary.** Explicit intent-first generation improves **intent correctness** versus free-form direct LLM reasoning on the same compound commands.

**Secondary (proposal wording).** Risk/capability/uncertainty coordination improves **routing** versus direct interpretation and fixed/degree-only policies.

## 3.3 What “success” means

| Kind | Role | Passes when… |
|---|---|---|
| **Intent** | **Primary** | Written job matches gold (cheap rule + two-judge) |
| **Routing** | Secondary | Predicted route = gold route |
| **Supporting** | Diagnostic | Ask-label, wording, CPC, risk-sensitive, ambiguity, capability |

Winning intent and losing routing is still a scientific result: it isolates policy failure from “never understood.”

## 3.4 Hypothesis verdict (preview)

| Claim | Verdict | Evidence |
|---|---|---|
| Better **intent** writing vs raw reasoning | **Supported** | 112 / 120 cheap on the job box; 113 / 120 two-judge |
| Better **routing** vs raw | **Not supported** | 54 / 120 vs 88 / 120; risk 0.491 vs 0.736 |
| Mechanism | Intent–policy dissociation | Forced box passes exams; refuse-first router trusts bad bits |

## 3.5 Scope and claim boundary

| We may claim | We may not claim |
|---|---|
| Better/worse intent writing and routing on Pilot-120 | Safe physical robot execution |
| Mechanisms tied to code paths | That we “ran AmbiK/CLARA/SafeAgentBench” as our main exam |
| Honest negatives with fix paths | General visual grounding |

## 3.6 Why the question is answerable

Pilot-120 is fixed, systems are runnable offline, and metrics are defined in Chapter 4. N = 120 is enough to **surface the intent–policy pattern** (same writing → different buttons; 62 intent-yes / routing-no rows) — that is the point of the study, not a size apology.
