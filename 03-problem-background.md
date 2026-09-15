# 2. Problem background

## 2.1 From speech acts to robot instructions

What a sentence says is not always what a hearer should do (Austin, 1962; Searle, 1969, 1975; Grice, 1975). In robotics the gap is operational: natural language must be mapped to execution, clarification, or refusal. Zhang et al. (2025) document underspecified collaborative requests; their physical setting motivates the problem but is not replicated here. The present study is restricted to text-level understanding and routing on Pilot-120.

## 2.2 Ambiguity and clarification

Prior work supplies design requirements that were implemented on Pilot-120:

| Prior work | Design requirement | Implementation in this study |
|---|---|---|
| Ivanova et al., 2025 | Compound ambiguity as a task class | Pilot-120 commands with multi-slot underspecification, gold jobs, and gold routes |
| Park et al., 2024 | Context affects feasibility and disambiguation | Context-blind system: identical router with scene and capability card withheld |
| Madureira and Schlangen, 2023 | Asking is distinct from asking well | Separate ask-label F1 and wording accuracy metrics, with an official wording sidecar |
| Mannekote et al., 2024 | Surface form need not equal intent | `indirect_request` speech-act label; router treats the act as actionable |
| Zhou et al., 2026 | Clarification is a legitimate system action | Clarify is a gold route on 23 of 120 rows |

| Focus in much prior work | Focus in this report |
|---|---|
| Ambiguity typing or clarification quality alone | Intent writing as primary outcome; routing as secondary |
| Embodied task success | Fixed Pilot-120 route mix: 76 execute, 23 clarify, 21 refuse |

## 2.3 Risk, capability, and rejection

| Prior work | Design requirement | Implementation in this study |
|---|---|---|
| Sarathy et al., 2025 | Fluent generation is not sound architecture | Write-then-route design: the language model writes analysis; Python selects the route; ablations change only the router |
| Scheutz et al., 2022 | Refusal can be competent behaviour | Gold refuse path on 21 rows; face-preserving rejection templates |
| Sucker et al., 2024; Sucker and Henrich, 2025 | Fuzzy time and quantity; silent resolution is not always appropriate | Pilot tags for fuzzy temporal and quantity phenomena; gold silent-resolve support is zero |
| Yin et al., 2024 | Risk should influence decisions | Official risk sidecar; risk-sensitive accuracy on 53 medium- and high-risk rows |

The risk-sensitive metric follows the proposal’s evaluation plan on Pilot-120. SafeAgentBench itself is not used as an evaluation corpus.

## 2.4 Gap addressed by this project

| Common evaluation pattern | Approach taken here |
|---|---|
| End-to-end simulation success | Hold the model fixed and vary only the routing policy |
| Clarification quality in isolation | Report intent correctness primarily and routing secondarily |
| Structured-output fidelity alone | Add official risk, CPC, and wording sidecars |

The purpose of the work is to determine whether a risk-aware write-then-route manager improves intent writing on compound commands, and to use routing and supporting metrics to explain the observed handling paths. Chapter 3 states the research question formally.
