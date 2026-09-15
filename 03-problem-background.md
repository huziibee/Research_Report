# 2. Problem background

## 2.1 From speech acts to robot instructions

What a sentence *says* is not always what a hearer should *do* (Austin, 1962; Searle, 1969, 1975; Grice, 1975). In robotics that gap becomes operational: map messy language into a **plan**, a **question**, or a **refusal**.

Zhang et al. (2025) motivate open slots in collaborative talk. We use that as **motivation only** — this study is text NLU on Pilot-120, not a physical tool-passing experiment.

## 2.2 Ambiguity and clarification — what we took into the build

We do **not** score AmbiK / CLARA / ClarifyVC as our main experiment. We **do** take specific design and measurement lessons into Pilot-120:

| Prior work | Idea we needed | What we implemented on Pilot-120 |
|---|---|---|
| Ivanova et al., 2025 (AmbiK) | Compound ambiguity is a real task class | Pilot-120 authored as multi-slot underspecification with gold jobs + routes |
| Park et al., 2024 (CLARA) | Context can change feasibility / disambiguation | **Context-blind** system: same router, card/scene hidden |
| Madureira & Schlangen, 2023 | “Did you ask?” ≠ “did you ask well?” | Separate **ask-label F1** and **wording** exams (+ official wording sidecar) |
| Mannekote et al., 2024 | Surface form ≠ true intent | `indirect_request` speech-act in schema; router treats it as actionable |
| Zhou et al., 2026 (ClarifyVC) | Ask is a valid system action | Clarify is a first-class gold route (23 / 120) |

| Typical prior focus | This report’s primary focus |
|---|---|
| Ambiguity type or clarification quality alone | **Intent writing** first, routing second |
| Embodied task success in simulation | Fixed Pilot-120 gold: 76 execute / 23 ask / 21 refuse |

## 2.3 Risk, capability, and rejection — what we took into the build

| Prior work | Idea we needed | What we implemented |
|---|---|---|
| Sarathy et al., 2025 | Fluent generation ≠ sound architecture | **Write-then-route**: LLM writes; Python presses the button; ablations swap only the router |
| Scheutz et al., 2022 | Refuse can be competence | Gold refuse path (21 / 120) + face-preserving rejection templates |
| Sucker et al., 2024; Sucker & Henrich, 2025 | Fuzzy time/quantity; not everything silent-resolves | Pilot tags `fuzzy_temporal` / `fuzzy_quantity`; gold silent-resolve support = **0** |
| Yin et al., 2024 (SafeAgentBench) | Risk should affect decisions | Official risk sidecar; risk-sensitive accuracy on 53 med+high rows |

Yin et al. motivate the risk metric; we did **not** run SafeAgentBench as a corpus. The risk exam is Pilot-native.

## 2.4 Gap this project fills

| Common pattern | What we do instead |
|---|---|
| End-to-end simulation success | Hold the **model fixed**, swap only the router |
| Clarification quality alone | Score **intent** (primary) and **routing** (secondary) side by side |
| JSON fidelity alone | Official risk / CPC / wording sidecars |

**Purpose:** show whether a risk-aware write-then-route manager improves **intent writing** on compound commands, and use routing to explain *how* the system got there. Chapter 3 states the question.
