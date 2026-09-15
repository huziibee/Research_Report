# 6. Conclusion

## 6.1 Summary

| Question | Answer on Pilot-120 |
|---|---|
| Does the manager beat raw on **routing**? | **No** — 54 / 120 vs **88 / 120** |
| Does it write the **job** well? | **Yes** — 112 / 120 cheap; 113 / 120 two-judge |
| Risk-sensitive (53 med+high) | Raw **0.736** · goal-first 0.491 |
| What breaks routing? | The **62**: 46 refuse · 13 ask · 3 execute |
| Same writing, different Python | Goal-first 54 · degree 59 · timid 26 · blind 21 |
| Wording / CPC | 0 / 23 · 0.045 — **[FIXABLE]** |
| Ambiguity exact-set | 0 / 120 — **[LIMITATION]** |

## 6.2 Author’s contribution

| # | Contribution |
|---:|---|
| 1 | Write-then-route manager on Qwen3-8B with degree / timid / context-blind ablations |
| 2 | Separated intent from routing; showed the split on real rows (CA-0026, CA-0007) |
| 3 | Official CPC, risk, and wording sidecars without mutating core gold |
| 4 | Named mechanisms for zeros (empty candidates; CPC status; unauthorized refuse) |
| 5 | Rubric-aligned report with honest **[FIXABLE]** / **[LIMITATION]** markers |

## 6.3 Future work

| Priority | Work | Marker |
|---|---|---|
| 1 | Clarification generator + filled candidates; re-score wording | **[FIXABLE]** |
| 2 | CPC `filled` status emission; re-score CPC F1 | **[FIXABLE]** |
| 3 | Retune capability / unauthorized routing; re-check routing + risk | Live science |
| 4 | Improve ambiguity tagging if exact-set stays 0 | **[LIMITATION]** |
| 5 | Optional: temperature ≠ 0 sensitivity on the same six systems | Later |
| 6 | Embodied pilot only after the text layer stops fighting itself | Later |

**One-sentence verdict:**

> The manager often **understands** the compound command on the page; the live router often **does not yet deserve** that understanding.
