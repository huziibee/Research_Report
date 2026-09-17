# 6. Conclusion

## 6.1 Summary of findings

| Question | Result on Pilot-120 |
|---|---|
| Primary comparison temperature | **Study default 0.7** (unified fix-stack); lower T = ablation; T0 holds official two-judge |
| Manager routing at **T0.7** | GF **54**; degree **57**; timid **29**; blind **21** / 120 |
| Intent auto screen at T0.7 | **117 / 120** (shared analysis) — not two-judge |
| Does write-then-route beat raw on official two-judge? | **No — tied 113 / 113 at T0** (only available protocol). Official at 0.7 **[Results Incoming]** |
| Does write-then-route still produce strong intent writing? | **Yes** — T0 two-judge **113 / 120**; T0.7 auto **117 / 120** |
| Does the manager improve routing versus raw (H2)? | **No** — T0.7 GF **54** vs historically raw **88** (T0); barely vs degree **57** |
| Dominant failure mode | Intent–policy dissociation (T0 slab: **62** rows; 46 refuse, 13 ask, 3 execute) |
| H3 (lower T vs 0.7) | **Provisional: not supported** — GF routing flat **54 / 47 / 51 / 54**; cooling does not rescue |
| H4 (T1.0 vs 0.7) | **[Results Incoming]** |
| CPC / wording / ambiguity at T0.7 | CPC ~**0.113**; wording **0 / 23** **[FIXABLE]**; exact-set ~**2 / 120** **[LIMITATION]** |
| Failed rows / repairs | Repair job **56191** **[FIXABLE]**; unified job **55670** |

## 6.2 Contribution

1. Intent-primary evaluation of a write-then-route manager with controlled policy ablations, centred at temperature **0.7**.  
2. Characterisation of intent–policy dissociation (for example CA-0007; disjoint two-judge miss lists at 113 / 120 on the T0 protocol).  
3. Transfer of prior-work design requirements into Pilot-120 systems and metrics.  
4. Official CPC, risk, and wording sidecars without mutating core gold (CPC improved to ~0.11 at 0.7; wording still unresolved).  
5. Temperature study with **0.7 as default**, lower temperatures as ablation (H3), and higher temperature (H4) still incoming.

## 6.3 Future work

| Priority | Work | Marker |
|---|---|---|
| 1 | Recalibrate capability / unauthorized routing so confirmed intent is not discarded | Future science |
| 2 | Populate clarification candidates; re-score wording | **[FIXABLE]** (unified **55670** / follow-on) |
| 3 | Emit CPC `filled` for licensed values; keep improving CPC micro-F1 | **[FIXABLE]** |
| 4 | Official two-judge at T0.7 (and grid); finish H4 at T1.0 | **[Results Incoming]** |
| 5 | Repair failed rows (T0.5/T0.7/…) via **56191** | **[FIXABLE]** |
| 6 | Fix-reemit 0.0/0.3 under fix stack for apples-to-apples H3 | **[Results Incoming]** via **55670** |
| 7 | After jobs: H1 improvement pass (Accept vs Reject; optional reformulation or new emit) | TODO — `context/pilot120-stable-checkpoint-20260915.md` |
| 8 | Optional embodied evaluation after the text layer is stable | Later |

The central conclusion is that, at the study default **temperature 0.7**, write-then-route still produces strong intent writing (auto screen **117 / 120**; official two-judge **113 / 120** only proven at T0) while the current routing policy fails to select the corresponding handling path (**54 / 120**), does not beat historically raw routing, and is not rescued by lowering temperature.
