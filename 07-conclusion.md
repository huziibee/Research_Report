# 6. Conclusion

## 6.1 Summary of findings

| Question | Result on Pilot-120 |
|---|---|
| Does write-then-route improve intent (primary, official two-judge)? | **Yes — 113 / 120** (automatic overlap screen 112 / 120) |
| Mechanism of the intent gain | Forced intent summary; adjudicator agreement |
| Does the manager improve routing versus raw Qwen (secondary)? | **No — 54 / 120 versus 88 / 120** (temperature-0 completed set) |
| Dominant failure mode | Intent–policy dissociation on 62 rows (46 refuse, 13 ask, 3 execute) |
| Policy ablations with shared writing | Goal-first 54; degree 59; timid 26; context-blind 21 |
| Clarification wording / CPC micro-F1 | 0 / 23; 0.045 — **[FIXABLE]** on frozen outputs |
| Default temperature 0.7 scoreboard | **[Results Incoming]** (H3) |

## 6.2 Contribution

1. Intent-primary evaluation of a write-then-route manager with controlled policy ablations.  
2. Characterisation of intent–policy dissociation (for example CA-0007).  
3. Transfer of prior-work design requirements into Pilot-120 systems and metrics.  
4. Official CPC, risk, and wording sidecars without mutating core gold.  
5. Temperature study design at 0.0, 0.3, **0.7 (default)**, and 1.0.

## 6.3 Future work

| Priority | Work | Marker |
|---|---|---|
| 1 | Recalibrate capability / unauthorized routing so confirmed intent is not discarded | Future science |
| 2 | Populate clarification candidates; re-score wording | **[FIXABLE]** |
| 3 | Emit CPC `filled` for licensed values; re-score CPC micro-F1 | **[FIXABLE]** |
| 4 | Complete and report the temperature-0.7-centred scoreboard (H3) | **[Results Incoming]** |
| 5 | Improve ambiguity-type prediction | **[LIMITATION]** today |
| 6 | Optional embodied evaluation after the text layer is stable | Later |

The central conclusion is that the manager frequently names the intended job correctly under the official two-judge protocol, while the current routing policy often fails to select the corresponding handling path.
