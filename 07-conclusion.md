# 6. Conclusion

## 6.1 Summary of findings

| Question | Result on Pilot-120 |
|---|---|
| What is the scientific object? | **Compound ambiguity** — multi-slot underspecification in one command |
| Primary comparison temperature | **Study default 0.7** (unified fix-stack); lower T = ablation; T1.0 = hotter probe |
| Manager routing at **T0.7** | GF **54**; degree **57**; timid **29**; blind **21** / 120 |
| Intent auto screen at T0.7 | **117 / 120** (shared analysis) — not two-judge |
| Does write-then-route beat raw on official two-judge? | **No — tied 113 / 113 at T0**. Official at 0.7 **[Results Incoming]** |
| Does write-then-route still produce strong intent writing? | **Yes** — T0 two-judge **113 / 120**; T0.7 auto **117 / 120** |
| Does the manager improve routing versus raw (H2)? | **No** — T0.7 GF **54** vs historically raw **88** (T0); barely vs degree **57** |
| Dominant failure mode | Intent–policy dissociation under compound load (T0 slab: **62** rows; 46 refuse, 13 ask, 3 execute) |
| H3 (lower T vs 0.7) | **Provisional: not supported** — cooling does not rescue GF (unified T0.0 **49**) |
| H4 (T1.0 vs 0.7) | **Provisional: supported** on routing — GF falls to **42 / 120** |
| CPC / wording / ambiguity at T0.7 | CPC ~**0.113**; wording **0 / 23** **[FIXABLE]**; exact-set ~**2 / 120** **[LIMITATION]** |

## 6.2 Contribution

1. An intent-primary evaluation of write-then-route under **compound ambiguity**, with controlled policy ablations, centred at temperature **0.7**.  
2. Characterisation of intent–policy dissociation as the operational failure mode: the job is often named; refuse-first policy on miscalibrated capability / authorization bits discards that writing (for example CA-0007; the **62**; disjoint two-judge miss lists at 113 / 120 on the T0 protocol).  
3. Transfer of prior-work design requirements into Pilot-120 systems and metrics without pretending secondary metrics are the primary claim.  
4. Official CPC, risk, and wording sidecars without mutating core gold (CPC improved to ~0.11 at 0.7; wording still unresolved).  
5. A temperature reading with **0.7 as default**, cooling as a non-rescue (H3), and hotter sampling as a routing degradation (H4 provisional at **42 / 120**).

## 6.3 Future work

| Priority | Work | Marker |
|---|---|---|
| 1 | Recalibrate capability / unauthorized routing so confirmed compound-job writing is not discarded | Future science |
| 2 | Populate clarification candidates; re-score wording | **[FIXABLE]** |
| 3 | Emit CPC `filled` for licensed values; keep improving CPC micro-F1 | **[FIXABLE]** |
| 4 | Official two-judge at T0.7 (and grid) | **[Results Incoming]** |
| 5 | Repair failed rows via **56191**; finish unified T0.3 fix-reemit | **[FIXABLE]** / **[Results Incoming]** |
| 6 | After jobs: H1 improvement pass (Accept vs Reject; optional reformulation) | TODO — checkpoint note |
| 7 | Optional embodied evaluation after the text layer is stable | Later |

The central conclusion is that, under **compound ambiguity** at the study default **temperature 0.7**, write-then-route can name the intended job at high rates (auto screen **117 / 120**; official two-judge **113 / 120** only proven at T0) while the current routing policy fails to select the corresponding handling path (**54 / 120**), does not beat historically raw routing, is not rescued by cooling, and degrades further at **1.0** (**42 / 120**). The open scientific problem is calibrated policy for compound decisions — not the absence of job writing.
