# Appendix A ? What is done vs what is still running

**Read this first if ?Incoming? feels unclear.**  
This appendix is an inventory, not the scientific argument.

**Cluster clock check:** 2026-09-18 ~00:31 UTC

---

## A.1 Plain-English status

| Job | State | What it is doing right now |
|---|---|---|
| **55670** `p120-unified` | **RUNNING** (~24h+) | Has finished T0.5, T0.7, T1.0, and fix-reemit **T0.0**. It is **currently generating fix-reemit T0.3** (~16/120 rows at last probe). |
| **56191** `p120-repair-rows` | **PENDING** | Waiting for 55670 to finish. Then it repairs shared failed IDs (e.g. CA-0070/0211 at 0.5; CA-0292/0963 at 0.7). |

Nothing else is queued behind these two for the temperature pack.

---

## A.2 Done (usable now)

| Item | Marker | Notes |
|---|---|---|
| Official two-judge intent (H1) | **Done** | **Only at T0** final-close. GF = raw = **113/120**. |
| Study-default manager routing at **T0.7** | **Done** | GF **54**, degree **57**, timid **29**, blind **21**. |
| Intent auto screen at T0.7 | **Done** | Shared analysis **117/120** (screen, not two-judge). |
| T1.0 manager routing (H4) | **Done** | GF **42**, degree **54**, timid **26**, blind **24**. |
| Unified fix-reemit T0.0 | **Done** | GF **49**. |
| Unified T0.5 | **Done** | GF **51**; 2 failed IDs still need repair. |
| Mega T0.0 / T0.3 full sweeps | **Done** (pre-fix) | Usable for trends with stack-mix caveat. |
| Mechanism digs (the 62, CA-0007, heatmaps) | **Done** | Measured on T0 matched set. |

---

## A.3 Still Incoming / not finished

| Item | Why it is still open | Blocks which claim? |
|---|---|---|
| **Unified fix-reemit T0.3** | Job **55670** still emitting (~16/120) | Cleaner H3 apples-to-apples vs 0.7 |
| **Repair job 56191** | Depends on 55670 | A few failed rows at 0.5/0.7 (and possibly 1.0) |
| **Official two-judge at T0.7** | Never launched as a judge pack for 0.7 | Cannot claim official H1 at the study default |
| **Official two-judge at T1.0** | Same | Cannot claim official intent for H4 |
| **Matched Raw/Fine-tune routing at T0.7** | Not in this unified manager pack | H2 uses historically raw **88** at T0 as comparator |
| **Wording 0/23 fix** | Emit still has empty candidates | Secondary metric only |
| **Cluster sidecar CPC files** | Often empty on cluster; local recompute used | Secondary; see CPC demotion in Results |

**Interpretation does not wait on CPC.** The primary story (compound-job naming vs refuse-first policy) is already supported by intent + routing + the 62.

---

## A.4 Temperature routing snapshot (secondary)

| Temp | GF | Degree | Timid | Blind | Source |
|---:|---:|---:|---:|---:|---|
| 0.0 | 49 | 57 | 24 | 21 | Unified fix-reemit **Done** |
| 0.3 | 47* | 56* | 25* | 21* | Mega pre-fix (*); unified still **Incoming** |
| 0.5 | 51 | 69 | 23 | 21 | Unified **Done** |
| **0.7** | **54** | **57** | **29** | **21** | Unified **Done** (default) |
| 1.0 | 42 | 54 | 26 | 24 | Unified **Done** |

---

## A.5 Paths

| Item | Path |
|---|---|
| Unified results | `/home-mscluster/mbangie/t12-hpc/results/pilot120_temp_priority-20260915/` |
| Final-close judges | `/home-mscluster/mbangie/t12-hpc/results/final_close-20260913/` |
| Local evidence | `Research Project/outputs/cluster_pulls/unified_55670/` |
