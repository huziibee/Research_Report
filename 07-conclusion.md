# 6. Conclusion

## 6.1 Summary

| Question | Answer on Pilot-120 |
|---|---|
| Does write-then-route improve **intent** (primary)? | **Yes** — 112 / 120 cheap; 113 / 120 two-judge |
| How? | Forced job box + scene nouns; judges agree |
| Does it beat raw on **routing** (secondary)? | **No** — 54 / 120 vs **88 / 120** |
| Underlying pattern | Intent–policy dissociation (good box, bad bits) |
| The 62 | 46 refuse · 13 ask · 3 execute |
| Same writing, different Python | 54 / 59 / 26 / 21 |
| Wording / CPC | 0 / 23 · 0.045 — **[FIXABLE]** |

## 6.2 Author’s contribution

| # | Contribution |
|---:|---|
| 1 | Intent-primary evaluation of a write-then-route manager + policy ablations |
| 2 | Named the intent–policy pattern with cases (e.g. CA-0007) |
| 3 | Built design choices from prior work into Pilot systems (policy layer, context-blind, ask vs wording, refuse path, fuzzy tags, risk sidecar) |
| 4 | Official CPC / risk / wording sidecars without mutating core gold |
| 5 | Temperature study at 0.0 / 0.3 / 0.7 / 1.0; head-to-head tables on the T=0 matched set |

## 6.3 Future work

| Priority | Work |
|---|---|
| 1 | Clarification generator + candidates; re-score wording **[FIXABLE]** |
| 2 | CPC `filled` status; re-score CPC F1 **[FIXABLE]** |
| 3 | Retune capability / unauthorized routing so intent wins are not burned |
| 4 | Strengthen ambiguity tagging |
| 5 | Embodied pilot only after the text layer stops fighting itself |

**One-sentence verdict:**

> The manager often **names** the compound command correctly; the live router often **does not yet deserve** that writing.
