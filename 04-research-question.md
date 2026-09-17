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
| **H1** | **Rejected** (no gain vs raw) | Official two-judge **113 = 113** at **T0 final-close** (only available protocol). Absolute writing still strong. At T0.7 auto screen **117 / 120**, but official two-judge at 0.7 is **[Results Incoming]**. **TODO after jobs:** improvement pass — `context/pilot120-stable-checkpoint-20260915.md` |
| **H2** | **Rejected** | At study default **T0.7**: GF routing **54** vs historically raw **88** (T0); also vs degree **57** / timid **29**. Does not beat raw; barely vs degree. T0 risk-sensitive / low-risk (0.491 / 27 / 64) tell the same story. |
| **H3** | **Provisional: not supported** (cooling does not rescue GF) | Ablation vs 0.7: GF routing **54, 47, 51, 54** at 0.0 / 0.3 / 0.5 / **0.7**; intent screen **112, 108, 117, 117**. Degree peaks at 0.5 (**69**) then **57** at 0.7. Caveat: 0.0/0.3 are pre-fix / mix with unified 0.5/0.7. |
| **H4** | **[Results Incoming]** | Temperature 1.0 versus 0.7 (unified job **55670** still finishing T1.0) |

**Mechanism (H1/H2).** Write-then-route still produces strong intent writing (T0 two-judge **113 / 120**; T0.7 auto screen **117 / 120**), but once raw also has an intent box it does not *beat* raw on the official T0 protocol, and at T0.7 routing (**54**) does not beat historically raw (**88**). The sharper result is intent–policy dissociation: a usable intent summary co-occurs with refuse-first routing on miscalibrated capability / unauthorized fields. Recalibrating that router is future work. Failed-row repair is **[FIXABLE]** via job **56191**; wording **0 / 23** remains **[FIXABLE]** / unresolved on unified **55670** emits (older packaging **54774** / failed **54833** superseded).

## 3.5 Claim boundary

| Within scope | Outside scope |
|---|---|
| Intent and routing on Pilot-120 | Safe physical robot execution |
| Mechanistic attribution to router and analysis fields | Comparing box scores to the old reasoning-field 68 / 60 screen |
| Documented secondary metric failures; low-risk routing as ordinary routing | Claiming the 53-row risk exam means low-stakes behaviour was ignored |

## 3.6 Feasibility

Pilot-120 is fixed, the six systems are executable offline, and metrics are defined in Chapter 4. With N = 120 the study can compare systems and identify the intent–policy pattern.
