# 3. Research question, hypothesis, and purpose

## 3.1 Research question

**Does a risk-aware write-then-route ambiguity manager improve intent correctness for compound ambiguous robot commands compared with direct LLM interpretation and uniform / degree-based ambiguity-handling policies, when evaluated primarily on intent writing and secondarily on ambiguity, clarification, routing, and risk-sensitive correctness?**

| System | Role in the comparison |
|---|---|
| Raw Qwen / Fine-tune | Direct LLM interpretation |
| Goal-first | Write-then-route manager |
| Degree | Uncertainty-only policy; never refuses |
| Timid | Ask-unless-clean policy |
| Context-blind | Goal-first router with scene and capability card withheld |

## 3.2 Hypotheses

**H1 (primary).** Explicit intent-first generation improves intent correctness versus free-form direct LLM reasoning on the same compound commands.

**H2 (secondary).** Risk, capability, and uncertainty coordination improves routing correctness versus direct interpretation and fixed or degree-only policies.

In full form:

- **H1.** A write-then-route manager that forces a short intent summary will name the gold job more often than raw Qwen (and fine-tune) when both are scored for intent correctness on Pilot-120.
- **H2.** The same manager’s risk-aware router will match gold handling paths more often than raw Qwen, and will improve on degree-only and conservative ask policies, including on medium- and high-risk rows.

## 3.3 Outcome definitions

| Outcome | Role | Criterion |
|---|---|---|
| Intent correctness | Primary | Written job matches gold under the cheap overlap rule and the two-judge protocol |
| Routing correctness | Secondary | Predicted route equals gold route |
| Supporting metrics | Diagnostic | Ask-label F1, wording accuracy, CPC F1, risk-sensitive accuracy, ambiguity scores, capability accuracy |

A system may succeed on intent and fail on routing. That combination isolates policy error from failure to name the job.

## 3.4 Results against the hypotheses

Both hypotheses were evaluated on the completed Pilot-120 runs reported in Chapter 5. They are not waiting on a further job to be answered.

| Hypothesis | Result | Evidence |
|---|---|---|
| **H1** | **Confirmed** | Goal-first cheap intent **112 / 120** on the job box; two-judge intent **113 / 120** |
| **H2** | **Rejected** | Goal-first routing **54 / 120** versus raw **88 / 120**; risk-sensitive accuracy **0.491** versus **0.736** |

**Mechanism.** Intent–policy dissociation: the forced intent summary passes the primary exams, while the refuse-first router trusts miscalibrated capability and safety fields and therefore misses gold routes.

## 3.5 Claim boundary

| Within scope | Outside scope |
|---|---|
| Intent and routing performance on Pilot-120 | Safe physical robot execution |
| Mechanistic attribution to router and analysis fields | Claims that external corpora were the primary evaluation |
| Documented secondary metric failures | General visual grounding |

## 3.6 Feasibility

Pilot-120 is fixed, the six systems are executable offline, and metrics are defined in Chapter 4. With N = 120 the study can compare systems and identify the intent–policy pattern, including the 62 rows with correct intent and incorrect routing and the policy ablations that hold writing fixed.
