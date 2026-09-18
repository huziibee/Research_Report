# Glossary

| Term | Definition |
|---|---|
| **Compound ambiguity** | Several underspecified parameters co-occur in one command; naming the job and choosing execute / ask / refuse are joint decisions |
| **Pilot-120** | Fixed set of 120 compound robot commands with gold labels |
| **Intent correctness** | Primary outcome: written job matches gold |
| **Two-judge protocol** | Official intent exam: two judges, blinded to the route, both affirm the text names the gold job |
| **Automatic overlap** | Screening lexical Jaccard overlap at threshold 0.18; not the final intent verdict when two-judge exists |
| **Routing correctness** | Secondary outcome: predicted handling path matches gold |
| **Intent–policy dissociation** | High intent with low routing because the router trusts miscalibrated analysis fields |
| **Intent summary** | Short job paragraph required by the write-then-route manager |
| **Ask-label F1** | F1 for pressing Ask on the 23 gold-ask rows |
| **Wording accuracy** | Whether the clarification question covers licensed alternatives |
| **CPC** | Slot-binding parameter frame (proposal sidecar; **demoted** — not required for primary interpretation) |
| **CPC F1** | Micro-F1 over gold cells with `status == filled` (diagnostic only) |
| **Risk-sensitive decision accuracy** | Routing accuracy on the 53 medium+high gold-risk rows only |
| **Gold execute / clarify / refuse** | Gold handling paths |
| **Sidecar** | Official supplementary gold file; core gold remains frozen |
| **PEFT adapter** | Parameter-efficient fine-tune weights |
| **Goal-first / Degree / Timid / Context-blind** | Live manager family (see Chapter 4) |
| **The 62** | Correct intent, incorrect routing on the T0 matched set (46 refuse, 13 ask, 3 execute) |
| **[FIXABLE]** | Concrete emit / packaging / repair path exists |
| **[LIMITATION]** | Study or stack limit that is not a small emit patch |
| **[Results Incoming]** | Awaiting finished protocol or temperature cell; do not invent numbers |
| **Temperature study** | Ablation **0.0 / 0.3 / 0.5** vs study default **0.7**; higher-T probe **1.0** |
