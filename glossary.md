# Glossary

| Term | Definition |
|---|---|
| **Pilot-120** | Fixed set of 120 compound robot commands with gold labels |
| **Intent correctness** | Primary outcome: written job matches gold |
| **Routing correctness** | Secondary outcome: predicted handling path matches gold |
| **Intent–policy dissociation** | High intent with low routing because the router trusts miscalibrated analysis fields |
| **Intent summary** | Short job paragraph required by the write-then-route manager |
| **Two-judge protocol** | Two independent judges, blinded to the route, both affirm that the text names the gold job |
| **Cheap overlap rule** | Content-word Jaccard overlap at threshold 0.18 without polarity flip |
| **Ask-label F1** | Whether Ask was selected on gold-ask rows |
| **Wording accuracy** | Whether the clarification question covers licensed alternatives |
| **CPC** | Slot-binding parameter frame |
| **Sidecar** | Official supplementary gold file; core gold remains frozen |
| **PEFT adapter** | Parameter-efficient fine-tune weights |
| **Goal-first** | Write the job; Python selects the route |
| **Degree** | Shared writing; uncertainty-only router; never refuses |
| **Timid** | Shared writing; ask-unless-clean router |
| **Context-blind** | Scene and capability card withheld; goal-first router retained |
| **The 62** | Rows with correct intent and incorrect routing (46 refuse, 13 ask, 3 execute) |
| **Silent-resolve** | Act without asking; gold support on Pilot-120 is zero |
| **Salvage** | Reconstruction of a small number of broken JSON rows on CPU |
| **Temperature study** | Decoding at 0.0, 0.3, 0.7, and 1.0; comparison tables use the temperature-0 matched set |
