# Appendix A ? Cluster evidence inventory

**Role.** This appendix is an **operations and provenance note** for writers and examiners who need to know which GPU artifacts exist. It is **not** part of the scientific argument. The research claims live in Chapters 1?6.

**As of:** 2026-09-18  
**Honesty rule.** Markers only: **Done / Incomplete / [Results Incoming] / [FIXABLE] / [LIMITATION]**. Do not invent metric numbers here.

---

## A.1 Live status

| Job | State | Progress |
|---|---|---|
| **55670** `p120-unified` | **RUNNING** | **Done:** T0.5, T0.7, T1.0, fix-reemit T0.0. **In progress:** fix-reemit T0.3. |
| **56191** `p120-repair-rows` | **PENDING** (depends on 55670) | Repair shared failed rows |

**Manager routing from unified predictions (secondary):**

| Temp | GF | Degree | Timid | Blind | Marker |
|---:|---:|---:|---:|---:|---|
| 0.0 (unified fix-reemit) | 49 | 57 | 24 | 21 | **Done** |
| 0.5 | 51 | 69 | 23 | 21 | **Done** (repair pending) |
| **0.7** | **54** | **57** | **29** | **21** | **Study default ? Done** |
| 1.0 | 42 | 54 | 26 | 24 | **Done** (H4 routing); higher failures **[LIMITATION]** |
| 0.3 unified | ? | ? | ? | ? | **[Results Incoming]** |

Official two-judge remains **T0 final-close only**. Non-T0 two-judge = **[Results Incoming]**.

Primary cite packs: `outputs/cluster_pulls/unified_55670/` and live pull `unified_55670_live_20260918/`.

---

## A.2 What each temperature is for

| T | Scientific role | Artifact preference |
|---:|---|---|
| **0.7** | Study default scoreboard | Unified fix-stack **Done** |
| **0.0 / 0.3 / 0.5** | Ablation vs 0.7 (H3) | Prefer unified; mega T0.3 usable with stack-mix caveat |
| **1.0** | Hotter probe (H4) | Unified **Done** for routing |
| **0.0 final-close** | Official two-judge (H1) | Judges under `final_close-20260913/` **Done** |

---

## A.3 Historical mega job (why it was cancelled)

Mega-official **54259** finished final-close judges and full **T0.0 / T0.3** sweeps (R1?R3), then was **CANCELLED** after starting incomplete **T0.7/R1** (~7 rows). Those 7 rows are **not** reportable. Contingency jobs **54832 / 54833** failed immediately (stale eval). Unified **55670** replaced them.

Kept mega artifacts still matter for:

- official two-judge at T0;
- mega-era T0.0 / T0.3 routing trends (pre-fix-stack);
- provenance that lower-T compute was not discarded.

They do **not** replace the T0.7 default scoreboard.

---

## A.4 Failed rows still open

| Temp | Shared IDs | Typical reason | Marker |
|---:|---|---|---|
| 0.5 | CA-0070, CA-0211 | `bad_intent_summary` | **[FIXABLE]** via **56191** |
| 0.7 | CA-0292, CA-0963 | `bad_intent_summary` / `uncertainty_out_of_range` | **[FIXABLE]** via **56191** |
| 1.0 | larger set | noisier decode / schema | **[LIMITATION]** / partially **[FIXABLE]** |

---

## A.5 Paths

| Item | Path |
|---|---|
| Unified results (cluster) | `/home-mscluster/mbangie/t12-hpc/results/pilot120_temp_priority-20260915/` |
| Mega temp sweep (cluster) | `/home-mscluster/mbangie/t12-hpc/results/temp_sweep-20260913/` |
| Final-close judges (cluster) | `/home-mscluster/mbangie/t12-hpc/results/final_close-20260913/` |
| Local evidence brief | `Research Project/outputs/cluster_pulls/unified_55670/EVIDENCE_BRIEF.md` |
