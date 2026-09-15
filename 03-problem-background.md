# 2. Problem background

## 2.1 From speech acts to robot instructions

What a sentence *says* is not always what a hearer should *do* (Austin, 1962; Searle, 1969, 1975; Grice, 1975). In robotics that gap becomes operational: map messy language into a **plan**, a **question**, or a **refusal**.

Zhang et al. (2025) show everyday collaboration often leaves slots open and expects the partner to notice — the same pressure a robot faces when object, place, or time is underspecified in a compound command.

## 2.2 Ambiguity and clarification

The proposal situates this project in prior work on ambiguous instructions and clarification (not as evaluation sets used here):

| Idea from prior work                              | Source                      | Relevance to this project            |
| ------------------------------------------------- | --------------------------- | ------------------------------------ |
| Recover the intended reading of an ambiguous task | Ivanova et al., 2025        | Motivation for compound ambiguity    |
| Classify *and* disambiguate user commands         | Park et al., 2024           | Clarification as a first-class skill |
| Clarifying ambiguous control commands             | Zhou et al., 2026           | Ask is a valid system action         |
| Clarification as a measurable dialogue move       | Madureira & Schlangen, 2023 | Ask-label vs wording quality         |
| Surface form (“Can you…?”) ≠ true intent          | Mannekote et al., 2024      | Speech-act caution                   |

This project stays **text-only**. Evaluation is on **Pilot-120**, not on those external corpora.

| Typical prior focus | This report’s focus |
|---|---|
| Ambiguity type or clarification quality alone | **Intent writing** and **route choice** together |
| Embodied task success in simulation | Fixed Pilot-120 gold mix: 76 execute / 23 ask / 21 refuse |

That is why a **112-intent / 54-routing** split reads as a *manager* failure, not “the model never understood.”

## 2.3 Risk, capability, and rejection

| Idea                                   | Source                                      | Lesson for routing                    |
| -------------------------------------- | ------------------------------------------- | ------------------------------------- |
| Safe task planning for LLM agents      | Yin et al., 2024                            | Risk must affect the button           |
| Rejection with justification           | Scheutz et al., 2022                        | Refuse can be competence              |
| Fluent generation ≠ sound architecture | Sarathy et al., 2025                        | Need an explicit policy layer         |
| Fuzzy time / quantity                  | Sucker et al., 2024; Sucker & Henrich, 2025 | Not everything can be silent-resolved |

**Practical lesson:** naming the job and choosing the path are different skills. A system can write the correct move and still refuse on a wrong capability bit.

## 2.4 Gap this project fills

| Common pattern | Still rare — and what we do |
|---|---|
| End-to-end simulation success | Hold the **model fixed**, swap only the router |
| Clarification quality alone | Report **intent** and **routing** side by side |
| JSON fidelity alone | Official risk / CPC / wording sidecars on Pilot-120 |

**Purpose:** build and evaluate a risk-aware write-then-route manager on Pilot-120, against the proposal’s direct, degree, conservative, and context-blind comparators. Chapter 3 states the testable question.
