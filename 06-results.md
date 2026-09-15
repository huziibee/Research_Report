# 5. Results

This chapter answers the research question with evidence, then explains *why* the numbers look the way they do. Figures are large PNGs under `figures/`. Every table keeps the locked system order.

---

## 5.1 The story in one page

| # | Finding |
|---:|---|
| 1 | New manager **writes the job well** |
| 2 | Same manager **routes poorly** (mostly wrong refuses) |
| 3 | Raw Qwen **routes better**, especially on medium/high risk |
| 4 | Tiny secondary scores (wording, CPC) are **named engineering failures**, not empty science |
![Intent correctness by system (cheap writing exams).](figures/intent-primary-wide.png)

*Figure 1. Intent correctness on systems with a writing exam. Raw / fine-tune cheap scores use T39 written reasoning; goal-first uses `intent_summary`. Do not subtract 112 from 68.*

![Intent versus routing for the main comparators.](figures/intent-vs-route-wide.png)

*Figure 2. Left: intent next to routing. Right: the orange slab on new goal-first is the **62** rows where the writing named the job but the button missed.*

![Routing correctness for all six live systems.](figures/routing-correct-wide.png)

*Figure 3. Routing correctness — the button, not the writing. Context-blind’s 21 / 120 sits on gold’s 21 refuse rows (always-refuse band), not “smarter safety.”*

---

## 5.2 Intent and routing scoreboard

| System | Cheap intent | Official two-judge intent | Routing |
|---|---:|---:|---:|
| Raw Qwen | 68 / 120 (T39 *reasoning*) | **113 / 120** (*new intent box*) | **88 / 120** |
| Fine-tune | 60 / 120 (T39 reasoning) | **107 / 120** (new intent box) | 87 / 120 |
| New goal-first | **112 / 120** (`intent_summary`) | **113 / 120** (same box) | **54 / 120** |
| New degree | (same 112 box) | (same writing) | 59 / 120 |
| New timid | (same 112 box) | (same writing) | 26 / 120 |
| New context-blind | — | **108 / 120** (blind box) | 21 / 120 |

Two-judge protocol: two independent models, both must agree, blinded to the route. Collected in the official final-close pass.

**Reading rules for students (and markers):**

- **112 vs 68** live on different text fields. Comparing them as “+44 points of understanding” is invalid.
- Raw’s official **113** is from a **new short intent box** collected in final-close, not from the old T39 thinking dump.
- Goal-first **113** and raw **113** are the **same count, different rows** (seven disjoint misses each).

New goal-first intent × routing under the cheap rule:

| | Routing correct | Routing wrong |
|---|---:|---:|
| Intent yes | 50 | **62** |
| Intent no | 4 | 4 |

On gold-do-it rows, the box still looked like the job **71 / 76** times. Understanding was usually there; the button often was not.

Fine-tune vs raw on cheap intent (McNemar) gives **p ≈ 0.24** — a wash. The adapter was not trained to fill `intent_summary`.

---

## 5.3 A concrete case: understood, then refused

**CA-0026.** Command: “Move the selected return item to its assigned destination shortly.”  
Gold job (short): move the **amber** return item to the **display plinth** within **three minutes**. Gold route: **execute**.

| System | Intent? | Route |
|---|---|---|
| New goal-first | Yes (overlap 0.368) — named amber move and three minutes | **Refuse** (“unsafe / unauthorized”) |
| New degree / timid | Same writing | Ask (still wrong vs gold) |
| Raw Qwen | Cheap intent no on reasoning (0.109) | Ask |

The manager *knew* the job. A separate pilot bit said `unauthorized` on a **low-risk** licensed move, and `_route_goal_first_v2` refused. That is policy on a good paragraph — the central mechanistic claim of this chapter.

A second pattern appears on **CA-0007** (controlled medicine tray): gold wanted **clarify**; goal-first named the delivery job in the box then **refused**; timid (same box) **asked** and matched gold. Same writing, different Python rule → different science.

---

## 5.4 The 62: intent yes, routing no

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

## 5.5 Clarification: asking vs asking well

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

## 5.6 Slot binding (CPC) and risk

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

## 5.7 Ambiguity tags and speech acts

| Metric | New goal-first | Raw Qwen |
|---|---:|---:|
| Ambiguity exact-set | **0 / 120** | 0 / 120 |
| Ambiguity macro-F1 | 0.246 | 0.077 |
| Capability accuracy | 0.425 | 0.667 |

![Ambiguity over-prediction pattern.](figures/ambiguity-overpredict-wide.png)

*Figure 9. Ambiguity tagging errors are real (exact-set stays 0 / 120), not a missing column in the files.*

**[LIMITATION]** Exact-set 0 / 120 is a real tagging failure (for example heavy `action_order` misuse), not a missing field in the files. Partial credit exists unofficially (at least one shared tag on 62 / 120) but is not the official exact-set claim. Speech-act exact on live goal-first is weak on indirect requests (**0 / 29** in the live lane) — a separate skill from naming the job in prose, and not a proposal headline.

---

## 5.8 Stability and confusion

![Replica stability.](figures/replica-stability-wide.png)

*Figure 10. Replica agreement for routing under greedy decoding. Live goal-first uses three matching replicas after salvage; raw/fine-tune used five in T39.*

![Routing confusion heatmaps.](figures/routing-confusion-heatmaps.png)

*Figure 11. Where buttons go wrong: goal-first’s mass of gold-execute → refuse is the visual form of the 62.*

![Route-level F1 support.](figures/route-f1-wide.png)

*Figure 12. Per-route view of the same routing story.*

---

## 5.9 Open items that do **not** change the Pilot-120 verdict

| Item | Marker | Why it does not overturn Ch. 5 |
|---|---|---|
| Wording / CPC generator fixes | **[FIXABLE]** | Need a new emit pass; mechanisms already named |
| Ambiguity exact-set | **[LIMITATION]** | Real tagging fail on this set |
| Optional temperature ≠ 0 | **[PENDING]** | Main scoreboard is greedy T=0 |

---

## 5.10 Relating results to the research question

| Claim the data support | Claim the data do **not** support |
|---|---|
| Goal-first write-then-route yields strong intent writing on Pilot-120 | The live manager currently beats raw Qwen on routing or risk-sensitive accuracy |
| Holding writing fixed, Python routers move routing a lot (54 / 59 / 26) | Degree is “braver understanding”; timid is “more careful prose” |
| Wrong capability / unauthorized bits explain most of the 62 | Wording 0/23 and CPC 0.045 prove intent failed |
| Context without the card collapses capable recall and routing | Hiding context improves safety |

**Primary hypothesis verdict.** The May proposal predicted better **routing**. On Pilot-120, live goal-first **does not** deliver that against raw Qwen. The contribution is the split: clarification and rejection literature (Chapter 2) are right that ask/refuse matter, but bundling risk/capability into a brittle refuse-first router can erase the gains of better intent prose. Those skills must be measured *with* the button, not instead of it.

**Code visibility.** Companion repository: `Documents\University\Research Project` (code, scripts, frozen predictions, gold/sidecars). This vault is the narrative write-up; per-command case cards live in `Research Project\results\`.

---

## 5.11 Limitations of the results

| # | Limitation |
|---:|---|
| 1 | N = 120 pilot scale |
| 2 | Text only — no embodied confirmation |
| 3 | Gold from dual-model annotation + adjudication |
| 4 | **[FIXABLE]** wording and CPC bugs depress secondary metrics |
| 5 | Salvage softens routing 54 vs harsh 51 |
| 6 | Ambiguity exact-set remains 0 / 120 |
