# Glossary

| Term | Definition |
|---|---|
| **Pilot-120** | Fixed set of 120 compound robot commands with gold labels |
| **Intent correctness** | Primary outcome: written job matches gold |
| **Two-judge protocol** | Official intent exam: two judges, blinded to the route, both affirm the text names the gold job |
| **Automatic overlap** | Screening lexical Jaccard overlap at threshold 0.18; not the final intent verdict when two-judge exists |
| **Routing correctness** | Secondary outcome: predicted handling path matches gold |
| **Intent–policy dissociation** | High intent with low routing because the router trusts miscalibrated analysis fields |
| **Intent summary** | Short job paragraph required by the write-then-route manager |
| **Ask-label F1** | F1 for pressing Ask on the 23 gold-ask rows |
| **Wording accuracy** | Whether the clarification question covers licensed alternatives |
| **CPC** | Slot-binding parameter frame |
| **CPC F1** | Micro-F1 over gold cells with `status == filled` |
| **Risk-sensitive decision accuracy** | Routing accuracy on the 53 medium+high gold-risk rows only |
| **Gold execute / clarify / refuse** | Gold handling paths (not “do-it”) |
| **Sidecar** | Official supplementary gold file; core gold remains frozen |
| **PEFT adapter** | Parameter-efficient fine-tune weights |
| **Goal-first / Degree / Timid / Context-blind** | Live manager family (see Chapter 4) |
| **The 62** | Correct intent, incorrect routing (46 refuse, 13 ask, 3 execute) |
| **[FIXABLE]** | Known implementation defect on frozen outputs |
| **[LIMITATION]** | Study limit that is not a small emit patch |
| **[Results Incoming]** | Awaiting finished GPU outputs (especially temperature 0.7) |
| **Temperature study** | 0.0, 0.3, **0.7 default**, 1.0 |
