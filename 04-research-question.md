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

**H3 (exploratory).** Changing decoding temperature away from the study default of 0.7 changes intent and routing behaviour on Pilot-120.

In full form:

- **H1.** A write-then-route manager that forces a short intent summary will name the gold job more often than raw Qwen (and fine-tune) when both are scored for intent correctness on Pilot-120, using the official two-judge protocol.
- **H2.** The same manager’s risk-aware router will match gold handling paths more often than raw Qwen, and will improve on degree-only and conservative ask policies, including on medium- and high-risk rows.
- **H3.** Relative to temperature 0.7, temperatures 0.0, 0.3, and 1.0 will produce measurable differences in intent and/or routing; the temperature study reports those differences.

## 3.3 Outcome definitions

| Outcome | Role | Criterion |
|---|---|---|
| Intent correctness | Primary | Official: two-judge agreement that the text names the gold job |
| Automatic overlap | Screening | Content-word Jaccard ≥ 0.18, no polarity flip |
| Routing correctness | Secondary | Predicted route equals gold route |
| Supporting metrics | Diagnostic | Ask-label F1, wording accuracy, CPC F1, risk-sensitive decision accuracy, ambiguity scores, capability accuracy |

A system may succeed on intent and fail on routing. That combination isolates policy error from failure to name the job.

## 3.4 Results against the hypotheses

H1 and H2 were evaluated on completed Pilot-120 runs (temperature-0 matched set for system comparison). H3 awaits the finished temperature-0.7-centred tables **[Results Incoming]**.

| Hypothesis | Result | Evidence |
|---|---|---|
| **H1** | **Confirmed** | Goal-first two-judge intent **113 / 120**; automatic overlap 112 / 120 on the same box |
| **H2** | **Rejected** | Goal-first routing **54 / 120** versus raw **88 / 120**; risk-sensitive decision accuracy **0.491** versus **0.736** |
| **H3** | **[Results Incoming]** | Temperature study at 0.0, 0.3, 0.7, 1.0 |

**Mechanism (H1/H2).** Intent–policy dissociation: the forced intent summary passes the official intent exam, while the refuse-first router trusts miscalibrated capability and safety fields and therefore misses gold routes. Recalibrating that router is future work (Chapter 6).

## 3.5 Claim boundary

| Within scope | Outside scope |
|---|---|
| Intent and routing performance on Pilot-120 | Safe physical robot execution |
| Mechanistic attribution to router and analysis fields | Claims that external corpora were the primary evaluation |
| Documented secondary metric failures | General visual grounding |

## 3.6 Feasibility

Pilot-120 is fixed, the six systems are executable offline, and metrics are defined in Chapter 4. With N = 120 the study can compare systems and identify the intent–policy pattern, including the 62 rows with correct intent and incorrect routing and the policy ablations that hold writing fixed.
