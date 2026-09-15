# Glossary

| Term | Plain meaning |
|---|---|
| **Pilot-120** | Fixed 120 compound robot commands with gold labels (this report’s evaluation set). |
| **Intent correctness** | Did the writing name the gold job? |
| **Routing correctness** | Did we press gold’s button (do it / ask / refuse)? |
| **Intent summary** | Short job box the new manager must fill first. |
| **SGC / two-judge** | Two other models, blinded to the route, both say the text names the gold job. |
| **Cheap rule / Jaccard** | Word-overlap pass; threshold 0.18. |
| **Ask-label** | Whether we pressed Ask on gold-ask rows. |
| **Wording** | Whether the clarification question names licensed alternatives. |
| **CPC** | Slot-binding frame (parameters of the job). |
| **Sidecar** | Extra official gold file; core gold stays frozen. |
| **PEFT / adapter** | Small fine-tune add-on weights. |
| **Goal-first** | Write the job; Python chooses the route. |
| **Degree** | Same writing; uncertainty-only router; never refuses. |
| **Timid** | Same writing; ask-unless-clean router. |
| **Context-blind** | Scene/card hidden; same goal-first router. |
| **The 62** | Intent yes, routing no (46 refuse / 13 ask / 3 execute). |
| **Silent-resolve** | Act without asking; gold support on Pilot-120 is 0. |
| **Salvage** | Broken GPU JSON rebuilt on CPU; routing 54 includes 3 such rows. |
| **T39** | Earlier frozen run (raw / fine-tune archive). |
| **Temperature 0** | Greedy decoding; main Pilot-120 scoreboard. |
| **[FIXABLE]** | Known bug; frozen scores stand until a new emit. |
| **[LIMITATION]** | Honest study limit. |
| **[PENDING]** | Optional follow-on; not needed for the main verdict. |
