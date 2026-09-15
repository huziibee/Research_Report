# 6. Conclusion

## 6.1 Summary of findings

| Question | Result on Pilot-120 |
|---|---|
| Does write-then-route improve intent correctness (primary)? | Yes: 112 / 120 cheap; 113 / 120 two-judge |
| Mechanism of the intent gain | Forced intent summary containing scene-grounded job content; adjudicator agreement |
| Does the manager improve routing versus raw Qwen (secondary)? | No: 54 / 120 versus 88 / 120 |
| Dominant failure mode | Intent–policy dissociation on 62 rows (46 refuse, 13 ask, 3 execute) |
| Policy ablations with shared writing | Goal-first 54; degree 59; timid 26; context-blind 21 |
| Clarification wording / CPC F1 | 0 / 23; 0.045 (implementation defects on frozen outputs) |

## 6.2 Contribution

1. An intent-primary evaluation of a write-then-route ambiguity manager with controlled policy ablations.  
2. Characterisation of intent–policy dissociation, including case evidence such as CA-0007.  
3. Transfer of prior-work design requirements into Pilot-120 systems and metrics (explicit policy layer, context-blind control, ask-label versus wording, refuse as a gold path, fuzzy tags, risk-sensitive scoring).  
4. Official CPC, risk, and wording sidecars without mutation of core gold.  
5. A temperature study at 0.0, 0.3, 0.7, and 1.0, with head-to-head system tables on the temperature-0 matched set.

## 6.3 Future work

| Priority | Work |
|---|---|
| 1 | Populate clarification candidates and regenerate wording; re-score wording accuracy |
| 2 | Emit CPC status `filled` for licensed values; re-score CPC F1 |
| 3 | Recalibrate capability and unauthorized routing so correct intent summaries are not discarded |
| 4 | Improve ambiguity-type prediction |
| 5 | Optional embodied evaluation after the text layer is stable |

The central conclusion is that the manager frequently names the intended job correctly, while the current routing policy often fails to select the corresponding handling path.
