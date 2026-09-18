# 3. Research question, hypothesis, and purpose

## 3.1 Research question

**Does a risk-aware write-then-route ambiguity manager improve intent correctness for compound ambiguous robot commands compared with direct LLM interpretation and uniform / degree-based ambiguity-handling policies, when evaluated primarily on intent writing and secondarily on ambiguity, clarification, routing, and risk-sensitive correctness?**

The question is deliberately intent-primary. Compound ambiguity makes naming the job hard; routing is the second decision. A system that names the job but mishandles the path has not solved the compound problem in an operational sense — but the failure mode must be attributed correctly (policy versus writing).

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

A system may succeed on intent and fail on routing. That combination isolates policy error from failure to name the compound job.

## 3.4 Results against the hypotheses

| Hypothesis | Result | Evidence |
|---|---|---|
| **H1** | **Rejected** (no gain vs raw) | Official two-judge **113 = 113** at **T0 final-close** (only available protocol). Absolute writing still strong. At T0.7 auto screen **117 / 120**; official two-judge at 0.7 **[Results Incoming]**. |
| **H2** | **Rejected** | At study default **T0.7**: GF routing **54** vs historically raw **88** (T0); also vs degree **57** / timid **29**. Does not beat raw; barely vs degree. The T0 **62**-row intent-yes / routing-no slab is the mechanism. |
| **H3** | **Provisional: not supported** | Ablation vs 0.7: GF routing does not improve under cooling (unified fix-reemit T0.0 **49**; mega T0.3 **47**; unified T0.5 **51**; default T0.7 **54**). Degree peaks at T0.5 (**69**). Stack-mix caveat on pre-fix mega 0.3. Unified T0.3 fix-reemit still **[Results Incoming]**. |
| **H4** | **Provisional: supported** (routing degrades) | At T1.0, GF routing falls to **42 / 120** (degree **54**, timid **26**, blind **24**), with higher failure/schema-error rate (**[LIMITATION]** of noisy decode). Official intent at 1.0 still **[Results Incoming]**. |

**Mechanism (H1/H2).** Under compound ambiguity the stack often *names* the job (T0 two-judge **113 / 120**; T0.7 auto screen **117 / 120**) and still *handles* it badly (T0.7 routing **54 / 120** vs historically raw **88**). Once raw also has an intent box, write-then-route does not beat raw on official intent. The sharper result is intent–policy dissociation: refuse-first routing on miscalibrated capability / unauthorized fields discards usable writing. Recalibrating that router is future work. Wording **0 / 23** and shared failed rows remain **[FIXABLE]**; ambiguity exact-set remains a **[LIMITATION]**.

## 3.5 Claim boundary

| Within scope | Outside scope |
|---|---|
| Intent and routing on Pilot-120 under compound ambiguity | Safe physical robot execution |
| Mechanistic attribution to router and analysis fields | Treating secondary zeros as proof that intent writing failed |
| Documented secondary metric failures; low-risk routing as ordinary routing | Claiming the 53-row risk exam means low-stakes behaviour was ignored |
| Marking unresolved items as **[FIXABLE]**, **[LIMITATION]**, or **[Results Incoming]** | Treating automatic overlap as official two-judge |

## 3.6 Feasibility

Pilot-120 is fixed, the six systems are executable offline, and metrics are defined in Chapter 4. With N = 120 the study can compare systems and identify the intent–policy pattern that compound ambiguity exposes.
