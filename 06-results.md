# 5. Results

This chapter answers the research question with evidence, then explains *why* the numbers look the way they do. Figures are large PNGs under `figures/`. Every table keeps the locked system order.

---

## 5.1 The story in one page

| # | Finding (intent first) |
|---:|---|
| 1 | New manager **names the gold job** (primary win) |
| 2 | Same manager often **presses the wrong button** (secondary) |
| 3 | Raw Qwen still **routes** better under risk |
| 4 | Pattern: forced job box ↑ intent; refuse-first bits ↓ routing |
| 5 | Wording / CPC zeros are **[FIXABLE]** engineering, not “no science” |

![Intent correctness by system (cheap writing exams).](figures/intent-primary-wide.png)

*Figure 1. **Primary metric.** Intent correctness. Raw / fine-tune cheap scores use T39 written reasoning; goal-first uses `intent_summary`. Do not subtract 112 from 68.*

![Intent versus routing for the main comparators.](figures/intent-vs-route-wide.png)

*Figure 2. Primary intent next to secondary routing. Orange slab = **62** intent-yes / routing-no.*

![Routing correctness for all six live systems.](figures/routing-correct-wide.png)

*Figure 3. Secondary metric — the button. Context-blind’s 21 / 120 is the always-refuse band, not smarter safety.*

---

## 5.2 How goal-first reaches 112 / 120 intent

This is the pattern Pilot-120 is for:

```mermaid
flowchart LR
  F["Forced intent_summary\nshort job prose"] --> J["Cheap Jaccard / two-judge"]
  J --> HI["High intent\n112 / 113"]
  F --> B["Capability / risk / unsafe bits"]
  B --> R["_route_goal_first_v2\nrefuse-first"]
  R --> LO["Lower routing\n54 / 120"]
```

| Step | What happens | Effect on score |
|---|---|---|
| 1 | Prompt forces a dedicated job paragraph first | Writing is scored on a clean field, not buried reasoning |
| 2 | Scene nouns land in that paragraph | Overlap ≥ 0.18 often passes (e.g. tray, meal, delivery) |
| 3 | Two-judge check on the same box | **113 / 120** — not just a lexical fluke |
| 4 | Router **never reads** “did the box match gold?” | Button uses capability / unauthorized / risk bits |
| 5 | Those bits are often wrong (capability acc. ≈ 0.425) | Intent stays high; routing collapses |

So 112 is a **higher score on the primary exam** than raw’s **68 on reasoning**. It is not “+44 understanding” versus raw’s later **113 on a new intent box** — that is a different field. The scientific win is: **intent-first writing works**; the scientific cost is: **policy still fights the writing**.

---

## 5.3 Intent and routing scoreboard

| System | Cheap intent **(primary)** | Official two-judge | Routing *(secondary)* |
|---|---:|---:|---:|
| Raw Qwen | 68 / 120 (T39 *reasoning*) | **113 / 120** (*new intent box*) | **88 / 120** |
| Fine-tune | 60 / 120 (T39 reasoning) | **107 / 120** (new intent box) | 87 / 120 |
| New goal-first | **112 / 120** (`intent_summary`) | **113 / 120** (same box) | **54 / 120** |
| New degree | (same 112 box) | (same writing) | 59 / 120 |
| New timid | (same 112 box) | (same writing) | 26 / 120 |
| New context-blind | — | **108 / 120** (blind box) | 21 / 120 |

Two-judge protocol: two independent models, both must agree, blinded to the route.

| Reading rule | Why |
|---|---|
| Do not subtract 112 − 68 | Different fields (box vs reasoning) |
| Raw’s 113 ≠ goal-first’s 113 rows | Same count, seven disjoint misses |
| Same writing → 54 / 59 / 26 | Proves routing is the Python rule |

| | Routing correct | Routing wrong |
|---|---:|---:|
| Intent yes | 50 | **62** |
| Intent no | 4 | 4 |

Gold-do-it rows where the box still looked like the job: **71 / 76**.

---

## 5.4 A concrete case: named the job, wrong button

**CA-0007.** Command: “Can the selected controlled medicine tray be delivered after a scheduled meal service?”  
(Nurse follow-up: treat it as a delivery request, not a capability question.)

Gold job (short): deliver the selected controlled medicine tray after the **11:00** meal service.  
Gold route: **clarify** (two trays / no recipient named in the command).

| System | Intent? | Route |
|---|---|---|
| New goal-first | Yes (overlap 0.275) — names the delivery after 11:00 | **Refuse** (unsafe / unauthorized) |
| New timid *(same box)* | Yes | **Ask** — matches gold |
| Raw Qwen | Yes on reasoning (0.237) | Execute |

Same paragraph, different Python → different science. Intent (primary) can pass while routing (secondary) still fails.

---

## 5.5 The 62: intent yes, routing no

![Rule breakdown among the 62.](figures/the-62-rules-wide.png)

*Figure 4. Why goal-first missed the button after naming the job. Dominated by `known_incapable` and `known_unsafe_or_prohibited`, not by “too many polite questions.”*

![Composition of the 62 miss modes.](figures/overask-breakdown-wide.png)

*Figure 5. Broader breakdown of intent-yes / routing-no behaviour (refuse vs ask vs wrong execute).*

| Piece of the 62 | Count | Meaning |
|---|---:|---|
| Total intent-yes / routing-no | **62** | Not “62 over-asks” and not “62 refuses” |
| Refuse | 46 | Headline failure mode |
| Ask | 13 | Still wrong vs gold |
| Wrong execute | 3 | Too brave |
| Of refuses: `known_incapable` | 36 | Gold capable **34** · conditional 2 · incapable **0** |
| Of refuses: unsafe / unauthorized | 10 | Gold capable, live low risk |

In plain terms: good job box + bad capability/safety stamp → router trusts the stamp.

| Same writing, different Python | Routing |
|---|---:|
| Goal-first | 54 / 120 |
| Degree (never refuse) | 59 / 120 |
| Timid (ask unless clean) | 26 / 120 |
| Context-blind | 21 / 120 |

| Extra fact | Number |
|---|---|
| Degree gold-refuse recall | **0 / 21** |
| Timid false asks | 55 |
| Context-blind capable recall | **0** |
| Context-blind refuses of gold-do-it | 75 / 76 |

![Capability accuracy.](figures/capability-accuracy-wide.png)

*Figure 6. New goal-first capability accuracy (0.425) is worse than raw (0.667). The router trusts this bit.*

![Capability versus refuse behaviour.](figures/capability-vs-refuse-wide.png)

*Figure 7. Wrong “cannot” / “unsafe” bits push refuses even when the job box is right.*
---

## 5.6 Clarification: asking vs asking well

![Clarification precision versus recall.](figures/clarification-pr-wide.png)

*Figure 8. Ask-label precision–recall. Raw asks often and leads F1; goal-first asks less and is less precise; degree floods false asks; timid is the honest “ask unless clean” cloud.*

| System | Ask-label F1 | Wording correct / 23 |
|---|---:|---:|
| Raw Qwen | **0.557** | **0 / 23** (T39 had no question string) |
| Fine-tune | 0.540 | 0 / 23 |
| New goal-first | 0.286 | 0 / 23 |
| New degree | 0.253 | 0 / 23 |
| New timid | 0.286 | 0 / 23 |
| New context-blind | 0.000 | 0 / 23 |

Ask-label asks: “did we press Ask?” Wording asks: “did the question name the licensed alternatives?”

### Why wording is 0 / 23 — **[FIXABLE]**

| What happened on 23 gold-ask rows | Count | Wording credit |
|---|---:|---|
| Refused | 14 | 0 |
| Executed instead of asking | 3 | 0 |
| Asked (slot-name templates) | 6 | **still 0** |

| Cause | Detail |
|---|---|
| Generator needs | Two filled values in `candidate_interpretations` |
| Live v2 emitted | Empty candidates on **all 120** rows |
| Result | Never built “Do you mean X or Y?” |
| Unofficial 1.1.0 replay | ~**2 / 23** on the six asked rows only |
| Frozen official score | Remains **0 / 23** until new questions are emitted |
---

## 5.7 Slot binding (CPC) and risk

| System | CPC F1 | Risk-sensitive accuracy (53 med+high) |
|---|---:|---:|
| Raw Qwen | — (no filled CPC cells) | **0.736** (39 / 53) |
| Fine-tune | — | 0.755 (40 / 53) |
| New goal-first | **0.045** | 0.491 (26 / 53) |
| New degree | 0.045 | 0.434 (23 / 53) |
| New timid | 0.045 | 0.245 (13 / 53) |
| New context-blind | — | 0.377 (20 / 53) |

### Why CPC F1 is 0.045 — **[FIXABLE]**

| Quantity | Count |
|---|---:|
| Gold filled cells | 678 |
| Pred cells with `status == filled` | 78 (only 6 / 120 rows) |
| True / false / false-neg | 17 / 61 / 661 |
| Official F1 | **0.045** |

| Bug | Reading |
|---|---|
| Model writes a usable `value` | Then stamps `unknown` / `not_applicable` |
| Official scorer | Only counts `status == filled` |
| Fix direction | Mark licensed values `filled` — do not coerce every unknown |

| Risk / reject | Raw | Goal-first | Degree | Context-blind |
|---|---:|---:|---:|---:|
| Risk-sensitive (53) | **0.736** | 0.491 | 0.434 | 0.377 |
| Gold-refuse recall | **21 / 21** | 17 / 21 | **0 / 21** | 21 / 21* |

\*Context-blind also refuses almost all do-it rows. Unsafe silent-resolve rate is **undefined** (gold support 0; nobody predicted it).

---

## 5.8 Ambiguity tags and speech acts

| Metric | New goal-first | Raw Qwen |
|---|---:|---:|
| Ambiguity exact-set | **0 / 120** | 0 / 120 |
| Ambiguity macro-F1 | 0.246 | 0.077 |
| Capability accuracy | 0.425 | 0.667 |

![Ambiguity over-prediction pattern.](figures/ambiguity-overpredict-wide.png)

*Figure 9. Ambiguity tagging errors are real (exact-set stays 0 / 120), not a missing column in the files.*

**[LIMITATION]** Exact-set 0 / 120 is a real tagging failure (for example heavy `action_order` misuse), not a missing field in the files. Partial credit exists unofficially (at least one shared tag on 62 / 120) but is not the official exact-set claim. Speech-act exact on live goal-first is weak on indirect requests (**0 / 29** in the live lane) — a separate skill from naming the job in prose, and not a proposal headline.

---

## 5.9 Stability and confusion

![Replica stability.](figures/replica-stability-wide.png)

*Figure 10. Replica agreement for routing under greedy decoding. Live goal-first uses three matching replicas after salvage; raw/fine-tune used five in T39.*

![Routing confusion heatmaps.](figures/routing-confusion-heatmaps.png)

*Figure 11. Where buttons go wrong: goal-first’s mass of gold-execute → refuse is the visual form of the 62.*

![Route-level F1 support.](figures/route-f1-wide.png)

*Figure 12. Per-route view of the same routing story.*

---

## 5.10 Open items that do **not** erase the pattern

| Item | Marker | Why the pattern still stands |
|---|---|---|
| Wording / CPC generator fixes | **[FIXABLE]** | Need a new emit; mechanisms already named |
| Ambiguity exact-set 0/120 | Tagging weakness | Intent–policy split does not need exact-set to be real |

---

## 5.11 Relating results to the research question

| Claim the data support | Claim the data do **not** support |
|---|---|
| Intent-first writing raises the **primary** intent exams on Pilot-120 | The live manager beats raw on **routing** or risk-sensitive accuracy |
| Same writing + different Python moves routing (54 / 59 / 26) | Degree = braver understanding; timid = more careful prose |
| Wrong capability / unauthorized bits explain most of the 62 | Wording 0/23 and CPC 0.045 prove intent failed |
| Context-blind collapses capable evidence | Hiding context improves safety |

**Primary verdict.** Intent writing **improves** under write-then-route (112 / 113 on the job box).  
**Secondary verdict.** Routing **does not** beat raw Qwen; refuse-first policy on bad bits is why.

Literature we actually built from (Chapter 2): Sarathy-style policy layer, CLARA-style context ablation, Madureira-style ask vs wording split, Scheutz-style refuse-as-competence, Sucker-style fuzzy tags with no silent-resolve gold.

**Code visibility.** `Documents\University\Research Project` (code, scripts, gold/sidecars). Case cards: `results\`.

---

## 5.12 What N = 120 is for

N = 120 is not an apology. It is large enough to:

| Pattern | Evidence |
|---|---|
| Intent–policy dissociation | 112 intent vs 54 routing; 62-row slab |
| Policy-only ablation | Same box → 54 / 59 / 26 |
| False “cannot” refuses | 34 / 36 incapables are gold-capable |
| Context necessity | Blind capable recall → 0; routing → 21 |

That is the underlying pattern. Scaling later tests generality; it is not required to see the failure mode.
