# Glossary

| Term | Plain meaning |
|---|---|
| **Pilot-120** | Fixed 120 compound robot commands with gold labels. |
| **Intent correctness** | **Primary metric** — did the writing name the gold job? |
| **Routing correctness** | **Secondary metric** — did we press gold’s button? |
| **Intent–policy dissociation** | High intent with low routing because the router trusts bad bits. |
| **Intent summary** | Short job box the new manager must fill first. |
| **SGC / two-judge** | Two models, blinded to the route, both say the text names the gold job. |
| **Cheap rule / Jaccard** | Word-overlap pass; threshold 0.18. |
| **Ask-label** | Whether we pressed Ask on gold-ask rows. |
| **Wording** | Whether the clarification question names licensed alternatives. |
| **CPC** | Slot-binding frame (parameters of the job). |
| **Sidecar** | Extra official gold file; core gold stays frozen. |
| **PEFT / adapter** | Small fine-tune add-on weights. |
| **Goal-first** | Write the job; Python chooses the route. |
| **Degree** | Same writing; uncertainty-only; never refuses. |
| **Timid** | Same writing; ask-unless-clean. |
| **Context-blind** | Scene/card hidden; same goal-first router. |
| **The 62** | Intent yes, routing no (46 refuse / 13 ask / 3 execute). |
| **Silent-resolve** | Act without asking; gold support = 0 on Pilot-120. |
| **Salvage** | Broken GPU JSON rebuilt on CPU. |
| **Temperature study** | Decoding at 0.0, 0.3, 0.7, 1.0; comparison tables use T=0 matched set. |
| **[FIXABLE]** | Known bug; frozen scores stand until a new emit. |
