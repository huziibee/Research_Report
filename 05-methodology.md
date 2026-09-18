# 4. Research methodology

## 4.1 Overview

We compare six text systems on **Pilot-120**, a fixed compound-ambiguity exam. No physical robot. The study default decoding temperature is **0.7**. A temperature study also runs **0.0, 0.3, 0.5, and 1.0**; primary system comparisons in Chapter 5 use the unified fix-stack emit at **0.7**, with lower temperatures as ablation and **1.0** as the higher-temperature probe. Mechanism deep-dives that were computed on the temperature-0 matched set (the **62**, CA-0007, confusion heatmaps) are labelled as such.

```mermaid
flowchart TD
  I["Input: command + scene + dialogue + capability card"] --> M["Language model\nQwen3-8B family"]
  M --> A["Structured analysis\n(+ intent_summary for managers)"]
  A --> R{"Route"}
  R --> E["Execute"]
  R --> C["Clarify / ask"]
  R --> F["Refuse"]
  E --> S["Score vs gold\nintent primary · route secondary · sidecars"]
  C --> S
  F --> S
```

*Figure B. Evaluation pipeline on Pilot-120.*

## 4.2 Data: Pilot-120

Pilot-120 is 120 **compound** commands: each item packages multi-slot underspecification with one gold job and one gold handling path. That size is enough to compare systems and to expose the intent–policy pattern that compound ambiguity produces (Chapter 5).

| Gold route | Count |
|---|---:|
| Execute | 76 |
| Clarify (ask) | 23 |
| Refuse | 21 |
| Silent-resolve | 0 |

Core gold is **frozen**. Official sidecars:

| Sidecar | Adds | Eligible size |
|---|---|---|
| CPC | Filled parameter cells | 678 cells |
| Risk | none / low / medium / high / unknown | **53** med+high |
| Wording | `must_convey` on gold-ask rows | **23** rows |

Models never see sidecars at generation time.

## 4.3 Systems and how they differ

| # | System | Proposal role | What changes |
|---:|---|---|---|
| 1 | Raw Qwen | Direct LLM | Model emits route |
| 2 | Fine-tune | Supervised fine-tune | PEFT adapter; no manager box |
| 3 | New goal-first | Full write-then-route | `intent_summary` + `_route_goal_first_v2` |
| 4 | New degree | Degree policy | **Same writing**; uncertainty only; never refuses |
| 5 | New timid | Conservative control | **Same writing**; ask-unless-clean |
| 6 | New context-blind | Context ablation (CLARA-style lesson) | Card/scene hidden; same goal-first router |

```mermaid
flowchart TD
  subgraph Shared["Systems 3–5 share one intent_summary"]
    BOX["intent_summary + analysis JSON"]
  end
  BOX --> GF["Goal-first router\nrefuse-first priority list"]
  BOX --> DEG["Degree router\nuncertainty thresholds only\nnever refuse"]
  BOX --> TIM["Timid router\nask unless analysis looks clean"]
  GF --> R1["Route A"]
  DEG --> R2["Route B"]
  TIM --> R3["Route C"]
```

*Figure C. Same writing, three policies — the ablation that proves routing is not “new understanding.”*

```mermaid
flowchart TD
  P1["1. Refuse if prohibited / unauthorized / high-risk unsafe"] --> P2["2. Refuse if incapable"]
  P2 --> P3["3. Refuse if capability unknown + risk med/high"]
  P3 --> P4["4. Execute if capable + low/none risk + actionable"]
  P4 --> P5["5. Otherwise ask"]
```

*Figure D. Goal-first router priority.*

```mermaid
flowchart TD
  U["Read uncertainty score"] --> L{"≤ 0.15?"}
  L -->|yes| EX["Execute"]
  L -->|no| M{"≤ 0.4?"}
  M -->|yes| SR["Silent-resolve\n(scored as execute here)"]
  M -->|no| ASK["Ask"]
```

*Figure E. Degree router — no refuse button.*

```mermaid
flowchart TD
  A["Read analysis"] --> Q{"Clean enough to execute?"}
  Q -->|no| ASK["Ask"]
  Q -->|yes| EX["Execute"]
```

*Figure F. Timid router — ask unless clean (simplified).*

| Ablation (study default **T0.7**, unified) | Routing on Pilot-120 |
|---|---:|
| Goal-first | **54 / 120** |
| Degree | **57 / 120** |
| Timid | **29 / 120** |
| Context-blind | **21 / 120** |

These default counts belong in Chapter 5’s scoreboard. Chapter 4 states them here so the reader sees that the three shared-analysis routers can diverge without rewriting the intent box — the methodological point of the ablation.

| Examiner path | Location |
|---|---|
| Repository | `Documents/University/Research Project` |
| Manager code | `src/ambiguity_manager/systems/` |
| Scripts / gold | `scripts/` · `data/annotations/pilot_120_v1/` |

## 4.4 What we measure

### Intent correctness (**primary**)

| Protocol | Role | Rule |
|---|---|---|
| **Two-judge** | Official primary | Two judges, blinded to the route, both say the text names the gold job |
| **Automatic overlap** | Screening check only | Jaccard on content words ≥ **0.18**, no polarity flip |

Overlap of 0.368 means about 37% of the combined content-word set is shared; it is not a probability. Automatic overlap on raw/fine-tune historically used written reasoning; manager scores use `intent_summary`. Those fields are not interchangeable. When both protocols exist for the same intent box, **two-judge is the final intent answer**.

### Routing correctness (**secondary**)

Predicted route equals gold route (execute / clarify / refuse).

### Clarification, CPC, risk, supporting

| Metric                               | What it is                                                                                                                                                                                                                                                        |
| ------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Ask-label F1                         | Harmonic mean of precision and recall for pressing Ask on the 23 gold-ask rows                                                                                                                                                                                    |
| Wording accuracy                     | On those 23 rows, does `clarification_question` cover every licensed alternative in `must_convey`?                                                                                                                                                                |
| **CPC F1**                           | Slot-binding **micro-F1**: predicted parameter cells versus official gold cells that are marked `status == filled` (678 eligible gold cells). Only predicted cells also marked `filled` count.                                                                    |
| **Risk-sensitive decision accuracy** | **Accuracy** (not F1): fraction of correct routes on the **53** gold rows labelled medium or high risk. The remaining rows are low (64), unknown (3), or none (0) and are **excluded from this exam by design** so the metric focuses on higher-stakes decisions. |
| Ambiguity / capability / safe-reject | Supporting diagnostics                                                                                                                                                                                                                                            |

## 4.5 Runs and evidence hierarchy

| Run | Temperatures | Role in this report |
|---|---|---|
| **Study default** | **0.7** (unified fix-stack, job **55670**) | Primary manager scoreboard (routing, auto intent screen, capability, CPC/risk/wording sidecars) |
| **Official two-judge** | **0.0** final-close only | H1 protocol; do not treat as a T0.7 two-judge result |
| **Temperature ablation** | 0.0, 0.3, 0.5 vs **0.7** | H3 (cooling); unified fix-reemit preferred where available |
| **Higher-T probe** | **1.0** (unified) | H4 (routing degradation) |
| **Mechanism digs** | T0 matched set | The **62**, CA-0007, confusion / capability figures — labelled whenever cited |
| **CPU sidecar scoring** | on frozen / unified predictions | CPC, risk, wording, ask-label |

**Salvage note.** A few broken JSON rows were rebuilt on CPU for the T0 matched set. When both a harsh incomplete count and a salvage count exist, the report states which is used.

## 4.6 Known secondary failures (and their status)

These diagnostics are scored against official sidecars. They do **not** wait on a new temperature hypothesis; they wait on emit quality or on scientific limits of the current stack.

| Issue | Marker | Current reading |
|---|---|---|
| Empty `candidate_interpretations` → slot-name clarification templates | **[FIXABLE]** | Wording still **0 / 23** on unified T0.5/T0.7 emits |
| CPC cells stamped `unknown` / `not_applicable` despite usable values | **[FIXABLE]** | Historical T0 F1 **0.045**; unified T0.7 ~**0.113** after coerce — still weak |
| Ambiguity exact-set near zero | **[LIMITATION]** (+ prompt fix already shipped) | Soft micro-F1 ~**0.41** at T0.7; exact-set ~**2 / 120** |
| Shared failed rows on unified emits | **[FIXABLE]** | Repair job **56191** queued after **55670** |
