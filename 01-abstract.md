# Abstract

This report studies **compound ambiguity** in robot-directed English: several underspecified parameters co-occur in one command, so the licensed next action is not always execution. Clarification or refusal may be required. The object of study is a text-only ambiguity manager that sits above any robot planner. The manager must (1) write the intended job and (2) select a handling path among execute, clarify, and refuse.

```mermaid
flowchart LR
  A["Compound command\n+ scene / dialogue\n+ capability card"] --> B["Ambiguity manager"]
  B --> B1["(1) Name the job"]
  B --> B2["(2) Choose a path"]
  B2 --> C["Execute"]
  B2 --> D["Ask / clarify"]
  B2 --> E["Refuse"]
  C --> F["Robot planner\n(out of scope)"]
```

*Figure A. Scope of the text layer. Embodied planning is excluded.*

Six systems are evaluated on **Pilot-120**, a fixed set of 120 compound commands with gold jobs and gold routes. The intellectual centre of the evaluation is whether the system can name the compound job; routing and supporting metrics (ambiguity tags, clarification wording, slot binding, risk-sensitive decisions) are secondary diagnostics that explain *how* handling fails when writing succeeds. The study default decoding temperature is **0.7**. Lower temperatures (**0.0, 0.3, 0.5**) are an ablation against that default; temperature **1.0** is included for the higher-temperature hypothesis.

| # | System | Description |
|---:|---|---|
| 1 | Raw Qwen | Base model selects the route |
| 2 | Fine-tune | Same prompt with a parameter-efficient adapter; no manager |
| 3 | New goal-first | Short intent summary; deterministic Python router |
| 4 | New degree | Shared analysis with goal-first; uncertainty thresholds; never refuses |
| 5 | New timid | Shared analysis with goal-first; ask-unless-clean policy |
| 6 | New context-blind | Same router; scene and capability card withheld |

**Primary outcome.** Intent correctness: whether the written job matches gold.  
**Official intent protocol.** Two independent judges, blinded to the route, both must agree that the text names the gold job.  
**Automatic overlap check.** A lexical content-word overlap rule (threshold 0.18) used as a fast screen; it is **not** the final intent verdict when two-judge scores exist.  
**Secondary outcomes.** Routing correctness and supporting diagnostics.

| Exam | Value | Protocol / temperature |
|---|---|---|
| **Manager routing at T0.7** (unified fix-stack) | Goal-first **54**; degree **57**; timid **29**; blind **21** / 120 | Study default |
| Intent auto screen at T0.7 (shared analysis) | **117 / 120** | Screen only — not two-judge |
| Manager routing at **T1.0** | Goal-first **42**; degree **54**; timid **26**; blind **24** / 120 | Higher-T probe (H4) |
| Risk-sensitive (GF, 53 med+high) at T0.7 | **32 / 53** | Unified sidecar |
| Capability accuracy (GF) at T0.7 | **0.442** | Unified eval |
| CPC micro-F1 (GF) at T0.7 | **~0.113** | Local sidecar recompute |
| Clarification wording / 23 at T0.7 | **0 / 23** | **[FIXABLE]** / unresolved |
| Ambiguity exact-set (GF) at T0.7 | **~2 / 120** (micro-F1 ~0.41) | Soft F1 up; exact-set **[LIMITATION]** |
| **Official two-judge intent** (GF vs raw) | **113 = 113** / 120 | **T0 final-close only** — H1 protocol |
| Historical raw routing (T0 matched) | **88 / 120** | Comparator for H2; not a T0.7 raw emit |

**H1 (official intent).** Rejected as superiority over raw: two-judge **tie at T0** (113 = 113). Absolute writing remains strong. At T0.7 the automatic intent screen is **117 / 120**, but official two-judge at 0.7 is **[Results Incoming]**.

**H2 (routing).** Rejected at the study default: goal-first **54 / 120** at T0.7 does not beat historically raw **88 / 120** at T0, and does not clearly beat degree (**57**). On the T0 matched set, **62** rows pass the automatic intent screen yet take the wrong route (46 refuse, 13 ask, 3 execute) — the central failure mode under compound load.

**H3 / H4 (temperature).** Cooling does not rescue goal-first routing (provisional). Raising temperature to **1.0** degrades goal-first routing to **42 / 120** (provisional support for H4), with higher row-failure rate (**[LIMITATION]** of noisy decode under the same refuse-first policy).

| Supporting metric | T0.7 (GF, unified) | Status |
|---|---:|---|
| Clarification wording / 23 | 0 / 23 | **[FIXABLE]** / unresolved |
| Slot-binding CPC F1 | ~0.113 | Improved vs historical ~0.045; still weak |
| Ambiguity exact-set | ~2 / 120 | **[LIMITATION]** (soft micro-F1 ~0.41) |
| Failed rows (CA-0292, CA-0963 at T0.7) | 2 shared IDs | **[FIXABLE]** via repair job **56191** |

**Contribution.** Under compound ambiguity, write-then-route can name the intended job at high rates (T0 two-judge **113 / 120**; T0.7 auto screen **117 / 120**) while a brittle capability- and safety-driven router still selects the wrong handling path (**54 / 120** at T0.7; **42 / 120** at T1.0). The scientific claim is therefore not that intent writing is unsolved, but that **compound understanding without calibrated policy** is insufficient for safe and useful handling. Completing official two-judge at 0.7, repairing wording and failed rows, and recalibrating the router remain follow-on work.

**Keywords:** compound ambiguity; robot command understanding; intent correctness; clarification; risk-aware routing; Pilot-120.
