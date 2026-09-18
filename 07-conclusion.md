# 6. Conclusion

## 6.1 Summary of findings

| Question | Result on Pilot-120 |
|---|---|
| Scientific object | **Compound ambiguity** — multi-slot underspecification in one command |
| Default temperature | **0.7** (unified fix-stack) |
| Manager routing at T0.7 | GF **54**; degree **57**; timid **29**; blind **21** / 120 |
| Intent auto screen at T0.7 | **117 / 120** (not two-judge) |
| Official two-judge vs raw | **Tied 113 = 113 at T0** (H1 Rejected as superiority) |
| Routing vs historically raw | GF **54** does not beat raw **88** (H2 Rejected) |
| Dominant failure | Intent–policy dissociation (T0 **62**: 46 refuse / 13 ask / 3 execute) |
| H3 / H4 | Cooling does not rescue GF; T1.0 drops GF to **42** |
| CPC | **Demoted** — not required for the interpretation |

## 6.2 Contribution

1. Intent-primary evaluation under compound ambiguity at temperature **0.7**.  
2. Characterisation of intent–policy dissociation: the job is often named; refuse-first policy on miscalibrated capability / authorization bits discards that writing.  
3. Controlled policy ablations with writing held fixed.  
4. Temperature reading: cooling is a non-rescue; hotter sampling worsens routing.  
5. Honest separation of settled claims from still-running cluster cells (unified T0.3; repair **56191**; non-T0 two-judge).

## 6.3 Future work (ordered — do these in sequence)

### Immediate (finish the open pack)

| # | Work | Marker |
|---:|---|---|
| 1 | Let **55670** finish unified T0.3; run **56191** repairs | **[Results Incoming]** / **[FIXABLE]** |
| 2 | Optional: official two-judge at T0.7 if H1 at default is required | **[Results Incoming]** |
| 3 | Wording candidate emit if clarification quality is kept in scope | **[FIXABLE]** |

### Next science (after the pack above)

| # | Work | Why |
|---:|---|---|
| 4 | **LLM capability classifier (or judge)** that re-labels capable / incapable / unauthorized from command + card + scene, *before* refuse-first routing | Stops the 62’s dominant false-refuse gate so the manager’s ambiguity behaviour becomes observable |
| 5 | Re-run routing with calibrated capability; analyse residual errors by ambiguity type | Answers how the manager handles compound underspecification once it is no longer blocked upstream |
| 6 | **Multi-LLM ambiguity adjudication:** two models propose/debate ambiguity types (and/or route) with written reasons; a third adjudicates | Current exact-set tagging is near floor (**[LIMITATION]**); debate + reasons is a stronger protocol than a single brittle bag |

### Only after 4–6 (theory for calibrated deferral)

These papers strengthen a *later* calibrated execute/defer architecture. They are **not** required to finish the present Pilot-120 interpretation.

| Paper | Why it helps later |
|---|---|
| Ren et al., KnowNo / “Robots That Ask For Help” (CoRL 2023) | Conformal ask-for-help under uncertainty — matches execute vs defer/refuse as the dominant remaining failure |
| Geifman & El-Yaniv, SelectiveNet (ICML 2019) | Reject-option / risk–coverage curves instead of refusal judged only by route accuracy |
| Farquhar et al., semantic entropy (Nature 2024) | Meaning-level uncertainty feature to replace weak ambiguity/degree signals |
| Wang, He & Kantaros (2024) | Language-instructed multi-robot planning with conformal assistance requests |

CPC is not on this roadmap unless a later proposal reinstates slot-binding as a primary claim.

The central conclusion stands: under compound ambiguity at **0.7**, write-then-route can name the job while refuse-first policy still mishandles the path. The open problem is calibrated capability and ambiguity adjudication — not more CPC.
