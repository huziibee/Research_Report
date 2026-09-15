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

- **H1 (primary).** A write-then-route manager that forces a short intent summary will name the gold job more often than raw Qwen (and fine-tune) when both are scored for intent correctness on Pilot-120, using the official two-judge protocol.
- **H2 (secondary).** The same manager’s risk-aware router will match gold handling paths more often than raw Qwen, and will improve on degree-only and conservative ask policies, including on medium- and high-risk rows.
- **H3 (lower temperature).** Relative to the study default of 0.7, lowering temperature to 0.0 or 0.3 will preserve official intent at least as well and will not materially worsen routing, because less sampling noise should stabilise capability and safety fields that currently drive false refuses.
- **H4 (higher temperature).** Relative to the study default of 0.7, raising temperature to 1.0 will increase replica variance and will degrade official intent and/or routing consistency, because noisier analysis bits feed the same refuse-first router.

## 3.3 Outcome definitions

| Outcome | Role | Criterion |
|---|---|---|
| Intent correctness | Primary | Official: two-judge agreement that the text names the gold job |
| Automatic overlap | Screening | Content-word Jaccard ≥ 0.18, no polarity flip |
| Routing correctness | Secondary | Predicted route equals gold route |
| Supporting metrics | Diagnostic | Ask-label F1, wording accuracy, CPC F1, risk-sensitive decision accuracy, ambiguity scores, capability accuracy |

A system may succeed on intent and fail on routing. That combination isolates policy error from failure to name the job.

## 3.4 Results against the hypotheses

| Hypothesis | Result | Evidence |
|---|---|---|
| **H1** | **Confirmed** | Goal-first two-judge intent **113 / 120** |
| **H2** | **Rejected** | Goal-first routing **54 / 120** versus raw **88 / 120**; risk-sensitive decision accuracy **0.491** versus **0.736** |
| **H3** | **[Results Incoming]** | Temperature 0.0 / 0.3 versus 0.7 |
| **H4** | **[Results Incoming]** | Temperature 1.0 versus 0.7 |

**Mechanism (H1/H2).** Intent–policy dissociation: the forced intent summary passes the official intent exam, while the refuse-first router trusts miscalibrated capability and safety fields. Recalibrating that router is future work. Wording and CPC defects are **[FIXABLE]** via a follow-on emit (packaged as `cluster/pilot120_fix_emit_20260915/`), not via mega job 54259.

## 3.5 Claim boundary

| Within scope | Outside scope |
|---|---|
| Intent and routing on Pilot-120 | Safe physical robot execution |
| Mechanistic attribution to router and analysis fields | Treating automatic overlap 112−68 as “+44 understanding” |
| Documented secondary metric failures | Claiming ambiguity exact-set is fixed by the wording/CPC emit |

## 3.6 Feasibility

Pilot-120 is fixed, the six systems are executable offline, and metrics are defined in Chapter 4. With N = 120 the study can compare systems and identify the intent–policy pattern.
