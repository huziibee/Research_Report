# 6. Conclusion

## 6.1 Summary of findings

| Question | Result on Pilot-120 |
|---|---|
| Does write-then-route beat raw on official two-judge intent? | **No — tied 113 / 113** (automatic screen on boxes: raw 120, goal-first 112) |
| Does write-then-route still produce strong intent writing? | **Yes — 113 / 120** official |
| Does the manager improve routing versus raw Qwen (secondary)? | **No — 54 / 120 versus 88 / 120** |
| Low-stakes (64 gold-low) routing | Goal-first **27 / 64** vs raw **46 / 64** |
| Dominant failure mode | Intent–policy dissociation on 62 rows (46 refuse, 13 ask, 3 execute) |
| Policy ablations with shared analysis | Goal-first 54; degree 59; timid 26; context-blind 21 |
| Clarification wording / CPC / ambiguity prompt | **[FIXABLE]** on fix-emit **54774** |
| Lower / higher temperature (H3 / H4) | **[Results Incoming]** |

## 6.2 Contribution

1. Intent-primary evaluation of a write-then-route manager with controlled policy ablations.  
2. Characterisation of intent–policy dissociation (for example CA-0007; disjoint two-judge miss lists at 113 / 120).  
3. Transfer of prior-work design requirements into Pilot-120 systems and metrics.  
4. Official CPC, risk, and wording sidecars without mutating core gold.  
5. Temperature study design at 0.0, 0.3, **0.7 (default)**, and 1.0 with separate lower- and higher-temperature claims.

## 6.3 Future work

| Priority | Work | Marker |
|---|---|---|
| 1 | Recalibrate capability / unauthorized routing so confirmed intent is not discarded | Future science |
| 2 | Populate clarification candidates; re-score wording | **[FIXABLE]** (fix-emit job) |
| 3 | Emit CPC `filled` for licensed values; re-score CPC micro-F1 | **[FIXABLE]** (fix-emit job) |
| 4 | Complete and report H3 (lower temperature) and H4 (higher temperature) | **[Results Incoming]** |
| 5 | Re-emit ambiguity tags with Pilot-17 definitions on constrained path (job 54774) | **[FIXABLE]** / **[Results Incoming]** |
| 7 | After jobs: H1 improvement pass (Accept vs Reject; optional reformulation or new emit) | TODO — `context/pilot120-stable-checkpoint-20260915.md` |
| 8 | Optional embodied evaluation after the text layer is stable | Later |

The central conclusion is that write-then-route produces strong official intent writing (**113 / 120**) but does not beat raw on the official protocol once both use intent boxes, while the current routing policy often fails to select the corresponding handling path — including on low-stakes rows.
