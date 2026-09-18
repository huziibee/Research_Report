# 10. Cluster results status ? Pilot-120 mega incomplete vs kept

**As of:** 2026-09-18 ~00:10 UTC (refreshed during compound-ambiguity rewrite)  
**Audience:** Research Report writers and anyone resuming after the mega job ended  
**Honesty rule:** This chapter inventories **jobs and artifacts**. It does **not** invent new metric numbers. Use **Done / Incomplete / Incoming / Fix-reemit / [Results Incoming] / [FIXABLE] / [LIMITATION]** exactly as marked.

---

## 10.0 Live status (2026-09-18)

| Job | State | Progress |
|---|---|---|
| **55670** `p120-unified` | **RUNNING** (~23h40m on `mscluster112`) | **Done:** T0.5, T0.7, T1.0, fix-reemit **T0.0**. **In progress:** fix-reemit **T0.3**. |
| **56191** `p120-repair-rows` | **PENDING** (`Dependency`) | Starts after **55670** |

**Routing counts from live unified predictions (secondary metric):**

| Temp | GF | Degree | Timid | Blind | Marker |
|---:|---:|---:|---:|---:|---|
| 0.0 (unified fix-reemit) | 49 | 57 | 24 | 21 | **Done** |
| 0.5 | 51 | 69 | 23 | 21 | **Done** (repair pending) |
| **0.7** | **54** | **57** | **29** | **21** | **Study default ? Done** |
| 1.0 | 42 | 54 | 26 | 24 | **Done** (H4); higher failures = **[LIMITATION]** |
| 0.3 unified | ? | ? | ? | ? | **[Results Incoming]** (emitting) |

Official two-judge remains **T0 final-close only**. Non-T0 two-judge = **[Results Incoming]**.

---

## 10.1 Executive summary (historical mega context)

Mega-official job **54259** ran for about **two days and fifteen hours** (`Elapsed 2-14:44:50`), then was **CANCELLED** on **2026-09-16** after finishing the temperature-sweep slices through **T0.3 / R3**. It had only just started the study-default temperature **T0.7 / R1** (about **seven** goal-first family rows). Those incomplete T0.7 files are **not** reportable emits.

**What was not lost.** Final-close judges and intent-box emits remain on disk. Full **120-line** goal-first (and companion) prediction files for **T0.0 R1?R3** and **T0.3 R1?R3** remain under the temp-sweep tree. Days of wall time on those slices are retained artifacts, not wasted compute.

**What is still missing for the centred report.** Complete emits at **0.7** (default) and **1.0**, plus the requested **0.5** contingency temperature. Mega never carried the wording / CPC / ambiguity **fix stack**; those repairs were never in mega emits.

**What replaces the failed follow-ons.** Contingency jobs **54832** / **54833** failed immediately (stale cluster eval missing `--temperature`). Unified job **55670** (`p120-unified`) is the live replacement: emit **0.5 ? 0.7 ? 1.0** with fixes, then **fix-reemit 0.0 ? 0.3** with sidecar scores. Verified queue state at documentation time: **PENDING** (`Priority`) on `biggpu`, output root already created.

---

## 10.2 Job timeline

| When (cluster clock) | Job ID | Name | Outcome | Notes |
|---|---:|---|---|---|
| ~2026-09-13 submit ? 2026-09-16T17:21:13 | **54259** | `mega-official` | **CANCELLED+** after `2-14:44:50` | Finished final-close + temp sweep **T0.0** and **T0.3** (R1?R3). Started **T0.7/R1** (~7 rows) then stopped so wall would not burn on incomplete default-T work. |
| 2026-09-16T17:21:15 | **54832** | `p120-temp-prio` | **FAILED** (~2 s) | Stale eval on cluster: missing `--temperature`. Produced no usable temperature slices. |
| 2026-09-16T17:21:16 | **54833** | `p120-fix-emit` | **FAILED** (~1 s) | Same stale-eval class of failure. No fix-emit artifacts. |
| 2026-09-16 evening ? | **55670** | `p120-unified` | **PENDING** (`Priority`) at verify time | Unified replacement: priority temps with fix stack, then fix-reemit of 0.0/0.3 + sidecar scores. Out dir: `?/results/pilot120_temp_priority-20260915/`. |

**Cancellation rationale (intentional).** After T0.3/R3 completed, mega was cancelled rather than continuing a multi-day T0.7/T1.0 sweep **without** the wording/CPC/ambiguity fixes. Completing those temps inside mega would have duplicated work once the fix stack needed a GPU re-emit anyway.

---

## 10.3 What finished on mega 54259

### 10.3.1 Final-close (kept)

Root: `/home-mscluster/mbangie/t12-hpc/results/final_close-20260913/`

| Artifact | Status | Role for the report |
|---|---|---|
| `judges/gfv2_intent_summary/` (`sgc_summary.json`, `sgc_rows.jsonl`) | **Done** | Official two-judge intent for goal-first `intent_summary` |
| `judges/intent_box_raw_ft/` | **Done** | Official two-judge intent for raw + fine-tune intent boxes |
| `intent_box/direct_base_llm/*.predictions.jsonl` | **Done** (120 lines) | Raw intent-box emit |
| `intent_box/t28_selected_adapter_llm/*.predictions.jsonl` | **Done** (120 lines) | Unofficial fine-tune intent-box emit |
| `MEGA_LEDGER.json`, `CLOSE_STATUS.json`, `PROVE_OK.json` | **Done** | Provenance / ?did not invent gold CPC/risk? ledger |
| Packets / smoke / prove subsets | Present | Supporting; not the headline scoreboard |

These final-close judges underpin the **temperature-0 matched** claims already written in Results §5 (two-judge **113 / 113** tie, routing dissociation, etc.). Do not treat mega cancellation as invalidating final-close.

### 10.3.2 Temperature sweep ? complete slices (kept)

Root: `/home-mscluster/mbangie/t12-hpc/results/temp_sweep-20260913/`

Verified via `find ? -name '*.predictions.jsonl'` + line counts:

| Temperature | Replicates | Goal-first family `*.predictions.jsonl` | Companion systems in same slices |
|---|---|---|---|
| **0.0** | R1, R2, R3 | **120 / 120** each (`goal_first_manager_v2`, `rich_conservative_manager_v2`, `degree_based_router_v2`, `goal_first_context_blind_v2`) | Raw, unofficial adapter, old managers also **120** where present |
| **0.3** | R1, R2, R3 | **120 / 120** each (same family) | Same pattern |

These are **full Pilot-120 emits** for lower temperatures under the **mega code path** (pre-fix-stack). They are valid for:

- documenting that lower-T work completed;
- optional preliminary lower-T routing / automatic-overlap screens **if** clearly labelled as mega-era (no wording/CPC/ambiguity fix);
- continuity checks against the upcoming **fix-reemit** of 0.0 and 0.3 from job **55670**.

They are **not** a substitute for the default-centred **0.7** tables required for H3/H4 as designed.

---

## 10.4 What is incomplete or lost from mega

| Slice / product | Disk truth | Report marker |
|---|---|---|
| **T0.7 / R1** goal-first family | **7** lines only under `temp_sweep-20260913/T0.7/R1/goal_first_v2/predictions/` | **Incomplete** ? do not score as a Pilot-120 emit |
| **T0.7** R2?R3 | Not completed | **Incomplete** |
| **T1.0** entire temperature | Not started in mega sweep | **Incomplete** / **[Results Incoming]** |
| **T0.5** | Never part of official mega grid; requested via contingency | **Incoming** via **55670** |
| Wording / CPC / ambiguity repairs inside mega emits | Mega skipped or never applied fix stack | **Not in mega** ? **[FIXABLE]** via unified job (and prior CPU sidecar autopsy remains valid for ?why zeros?) |
| Failed follow-ons **54832** / **54833** | Instant FAILED; no replacement artifacts | Obsolete; superseded by **55670** |

**Do not** promote the 7-row T0.7 partial into any table, figure, or hypothesis claim.

---

## 10.5 Per-temperature inventory (honest markers)

Study temperatures of interest: **0.0, 0.3, 0.5, 0.7 (default), 1.0**.

| T | Mega 54259 | Kept on disk now | Unified job 55670 plan | Status marker |
|---:|---|---|---|---|
| **0.0** | Full R1?R3 complete | `temp_sweep-20260913/T0.0/R{1,2,3}/?` ? 120-line goal-first family | **Fix-reemit** 0.0 with fix stack + sidecar scores | **Done** (mega-era) ? **Fix-reemit** (incoming, preferred for wording/CPC/ambiguity) |
| **0.3** | Full R1?R3 complete | `temp_sweep-20260913/T0.3/R{1,2,3}/?` ? 120-line goal-first family | **Fix-reemit** 0.3 with fix stack + sidecar scores | **Done** (mega-era) ? **Fix-reemit** (incoming) |
| **0.5** | Not in mega grid | Out dir stub only under priority root | **Emit first** (with fixes) | **Incoming** |
| **0.7** | Partial R1 (~7 rows) only | Partial files exist; **not usable** | **Emit second** (with fixes) ? study default | **Incomplete** (mega) ? **Incoming** (55670) |
| **1.0** | Not reached | ? | **Emit third** (with fixes) | **Incoming** |

**Reading the markers together.** Lower temperatures are **Done** as mega artifacts and will also be **Fix-reemit** for metrics that need the repair stack. Default and higher temperatures (plus 0.5) remain **[Results Incoming]** until **55670** finishes usable 120-line emits.

---

## 10.6 Unified job 55670 ? what it is supposed to produce

**Queue name:** `p120-unified` / `p120-uni`  
**Output root (verified present):** `/home-mscluster/mbangie/t12-hpc/results/pilot120_temp_priority-20260915/`  
At verify time the root contained `T0.5/`, `submission.tsv`, `unified_submission.tsv` (job still **PENDING** / Priority ? not yet a finished emit tree).

**Planned stages (do not reorder in prose):**

1. **Emit with fix stack:** temperatures **0.5 ? 0.7 ? 1.0**  
   - CPC coerce, ambiguity constrained prompts / Pilot-17-aligned tagging path, clarification generator **1.1.0**  
   - Sidecar scoring after emit  
2. **Fix-reemit:** temperatures **0.0 ? 0.3** (already complete on mega **without** those fixes) + sidecar scores  

**Why unify.** Separate contingency (**54832**) and fix-emit (**54833**) died on a stale eval binary. One job with a corrected script avoids a second dependency chain failure and avoids leaving reportable 0.7 emits that still lack the fix stack.

**ETA (planning only, not a promise):** on the order of ~30?36 h wall once RUNNING (roughly five ~6 h goal-first-family temperature passes), subject to `biggpu` Priority queue delay.

---

## 10.7 What the Research Report can already claim vs mark incoming

### Already claimable (temperature-0 / final-close matched set)

Use Results chapter numbers already locked from final-close + live v2 R1 managers ? **not** from incomplete mega T0.7:

- Official two-judge intent on intent boxes (goal-first vs raw tie narrative).  
- Automatic-overlap screen on the same `intent_summary` field.  
- Routing correctness, shared-analysis ablations, risk-sensitive accuracy, low-risk routing slice.  
- Intent?policy dissociation (62-row slab) and capability / unauthorized autopsy.  
- CPU sidecar wording **0 / 23**, CPC micro-F1 **0.045**, ambiguity exact-set zeros as **diagnosed** failures ? marked **[FIXABLE]**, not as final post-fix numbers.

### Must stay **[Results Incoming]** until 55670 delivers

- Full scoreboard centred at study default **T = 0.7**.  
- H3 (lower temperature) and H4 (higher temperature) contrast tables.  
- Temperature line graph of intent + routing vs T (placeholder figure remains a placeholder).  
- Any claim that mega ?finished the temperature study.?

### **[FIXABLE]** (GPU re-emit / sidecar rescore ? now via 55670, not mega)

- Clarification wording population and re-score.  
- CPC `filled` coerce and micro-F1 re-score.  
- Ambiguity constrained-prompt / vocab-list repairs on re-emit.  
- Prefer **fix-reemit** 0.0/0.3 from **55670** over mega-era files when those metrics are updated in the report.

---

## 10.8 Days of waiting were not lost ? kept artifact checklist

Copy this list into handoff notes if SSH is flaky later:

1. **Final-close judges** ? `?/final_close-20260913/judges/gfv2_intent_summary/` and `?/judges/intent_box_raw_ft/`.  
2. **Final-close intent-box predictions** ? 120 lines each for raw and FT under `?/final_close-20260913/intent_box/`.  
3. **Temp sweep T0.0 R1?R3** ? full 120-line goal-first family (and companions) under `?/temp_sweep-20260913/T0.0/`.  
4. **Temp sweep T0.3 R1?R3** ? full 120-line goal-first family (and companions) under `?/temp_sweep-20260913/T0.3/`.  
5. **Ledger / prove** files under final-close (provenance that mega did not invent gold CPC/risk).  
6. **Local report + vault prose** already written against the matched T0 set (Results §5.1?5.9 style claims).  
7. **Dig playbook** in `context/pilot120-stable-checkpoint-20260915.md` ? scripts and field rules for recompute when new predictions land.  
8. **Partial T0.7 (~7 rows)** ? kept only as forensic evidence of where mega stopped; **not** a result.

---

## 10.9 How to pull and recompute when 55670 finishes

Follow the **Dig playbook** in the Research Project checkpoint (do not invent a second procedure):

- Primary playbook: `Research Project/context/pilot120-stable-checkpoint-20260915.md` ? section **?Dig playbook ? how to redo this analysis when jobs finish?**  
- Vault mirror of the same checkpoint: `latest results/99-work-state-checkpoint.md` (if kept in sync)

### Minimal pull path

1. Confirm `sacct -j 55670` shows **COMPLETED** (or inspect stage completion markers under the priority out dir).  
2. `scp` / copy overlays from  
   `/home-mscluster/mbangie/t12-hpc/results/pilot120_temp_priority-20260915/`  
   into a local `outputs/cluster_pulls/?` tree (Windows: prefer short `scp` chunks; avoid huge PowerShell heredocs over SSH).  
3. Prefer **recompute from jsonl**, not copying old markdown numbers.  
4. Rebuild intent figures / low-risk table via `scripts/rebuild_report_intent_figures_20260915.py`.  
5. Re-run official sidecar follow-on scoring on new predictions (`scripts/score_official_sidecar_followon.py` pattern in the playbook).  
6. Update `06-results.md` §5.10 markers from **[Results Incoming]** / **[FIXABLE]** to numbers **only** when 120-line emits and scores exist.  
7. Replace the temperature line-graph placeholder only after T0.7-centred points exist.  
8. Refresh this chapter?s per-temperature table to **Done** where appropriate.

### Field rules (do not regress)

- Score intent on `intent_summary` boxes only ? never revive reasoning-field 68/60 in the main scoreboard.  
- Two-judge miss lists at 113/113 are **disjoint** ? never say ?the same 113 rows.?  
- Mega-era T0.0/T0.3 remain available for continuity, but wording/CPC/ambiguity claims should wait for fix-reemit outputs.

---

## 10.10 Path index (cluster)

| Path | Contents |
|---|---|
| `/home-mscluster/mbangie/t12-hpc/results/final_close-20260913/` | Final-close judges + intent boxes (kept) |
| `/home-mscluster/mbangie/t12-hpc/results/temp_sweep-20260913/` | Mega temp sweep; **T0.0** and **T0.3** complete; **T0.7** partial |
| `/home-mscluster/mbangie/t12-hpc/results/pilot120_temp_priority-20260915/` | Unified job **55670** output root |
| `cluster/pilot120_timeout_contingency_20260915/` | Historical contingency packaging (superseded operationally by unified job) |
| `cluster/pilot120_fix_emit_20260915/` | Fix-stack packaging notes (repairs now expected inside **55670**) |

---

## 10.11 One-page status table (for the report)

| Item | Marker |
|---|---|
| Final-close two-judge + intent boxes | **Done** |
| Mega temp sweep T0.0 R1?R3 | **Done** (kept) |
| Mega temp sweep T0.3 R1?R3 | **Done** (kept) |
| Mega temp sweep T0.7 / T1.0 | **Incomplete** |
| Contigency 54832 / fix-emit 54833 | **Failed** (obsolete) |
| Unified 55670 emits 0.5 / 0.7 / 1.0 | **Incoming** |
| Unified 55670 fix-reemit 0.0 / 0.3 + sidecars | **Fix-reemit** |
| H3 / H4 and T0.7-centred tables | **[Results Incoming]** |
| Wording / CPC / ambiguity post-fix scores | **[FIXABLE]** ? then numbers after 55670 |

---

*End of cluster inventory chapter. Update the dated stamp and markers when 55670 leaves PENDING and when each temperature reaches 120 lines.*

---

## 10.x Update 2026-09-17 evening ? filled from kept + unified

Job **55670** RUNNING (~17h); T0.5/T0.7 done; T1.0 ~93/120. Report now cites T0.0 salvage, T0.3 mega, T0.5/T0.7 unified for routing + intent screen. Repair job **56191** queued after 55670 for failed IDs (T0.5: CA-0070/0211; T0.7: CA-0292/0963). Full cite pack: [[11-temperature-evidence-brief]] / `outputs/cluster_pulls/unified_55670/EVIDENCE_BRIEF.md`.
