# Presentation Script
## EEG Analysis Platform for Prestimulus EEG-Based Behavioral Prediction

> **Format:** Each section shows the slide title, estimated time, and word-for-word talking points.  
> Cues in *(italics)* are stage directions or transition signals.

---

## Slide 1 — Title Slide
**~30 sec**

Good morning / afternoon everyone.
My name is Nantawat, and this is my teammate Naytitorn.
Today we are presenting our senior project: the **EEG Analysis Platform for Prestimulus EEG-Based Behavioral Prediction**, developed under the guidance of Asst. Prof. Dr. Thanawin Rakthanmanon and Assoc. Prof. Dr. Theerawit Wilaiprasitporn at VISTEC.

---

## Slide 2 — Brain–Computer Interface (BCI) and EEG
**~1 min**

Before we dive into our work, let me set the stage with two foundational concepts.

A **Brain–Computer Interface**, or BCI, is a system that creates a direct link between the brain and an external device — without going through muscles or nerves.
It translates raw neural signals into commands that a machine can understand and act upon.

The primary sensing technology we use is อิเล็กโตร-เอน-เซฟ-ฟะ-ล็อก-กรา-ฟี, or EEG.
EEG measures the electrical activity of groups of neurons near the scalp surface.
Its biggest advantage is **high temporal resolution** — we can capture brain responses that happen within milliseconds of an event.

*(point to image)* This figure illustrates how EEG electrodes sit on the scalp and record the summed activity of cortical populations.

---

## Slide 3 — Why Reproducible EEG Analysis is Difficult
**~30 sec**

*(point to graph)* This chart shows subjects per release across multiple experimental tasks.

As the number of tasks and subjects grows, the analysis space becomes **exponentially harder to manage reproducibly**.
Small preprocessing differences can lead to entirely different conclusions.

This is the core challenge that motivates our work.

---

## Slide 4 — Practical Gap in EEG Research
**~1 min**

So how do researchers currently cope with this complexity?

They typically face a hard choice:
Either use a **commercial tool** — easy to get started with but  inflexible —
or write **custom scripts** — full control but demands software engineering *skills* that most domain researchers  dont have.

resulting?
Folders full of script copies: v1, v2, v3 — with unclear differences.
Pipelines that nobody else can run. 

*(point to workflow image)* This diagram reflects a real workflow from our research lab — and you can see it is already complex before any software structure is applied.

This leads us to our central question: **How can we build a platform that is structured enough to be reproducible, yet accessible enough for domain researchers?**

---

## Slide 5 — Research Objective
**~30 sec**

Our project addresses two things simultaneously.

On the **software side**, we build a systematic, reproducible analysis platform.

On the **research side**, we ask a specific scientific question:
Can we predict a subject's **reaction time** and **trial correctness** from their EEG activity *before* a visual stimulus appears — during the inter-trial interval?

We use the **Healthy Brain Network EEG dataset** with the **Contrast Change Detection task**, and focus on a **2-second prestimulus window**.

---

## Slide 6 — Solution Overview
**~1 min**

Our solution is the **EEG Analysis Platform** — a unified, parameter-driven framework for domain experts.

The core design philosophy is this: the platform respects the user's domain knowledge while providing the software engineering structure they lack.

Key principles include:
- **Reproducibility** — every parameter, seed, and configuration is explicitly tracked
- **Modularity** — components can be swapped or extended independently
- **Efficiency** — caching avoids recomputing unchanged steps
- **Separation of concerns** — domain logic is kept separate from infrastructure

The target user is a researcher who can write Python code, but should not need to be a software engineer to run a rigorous experiment.

---

## Slide 7 — Section Break: PROJECT INTRODUCTION

*(transition slide — brief pause)*

Let us now walk through the project background in more detail.

---

## Slide 8 — Why This Problem Matters
**~45 sec**

The reproducibility crisis is not unique to EEG — it spans all of neuroscience.

Without standardized workflows, experiments are difficult to replicate.
Each research group builds its own isolated solution.
Researchers spend more time managing infrastructure than doing science.

The gap is not about expertise in EEG — it is about the **software engineering background** that domain researchers typically do not have.
The consequence is fragile code that is hard to share, test, or build upon.

Our approach: design a platform that **meets researchers where they are** while enforcing sound engineering practices underneath.

---

## Slide 9 — Our Solution: Design Objectives
**~45 sec**

We designed the platform around five objectives:

First, **systematic workflows** — replacing ad-hoc scripts with deterministic, parameter-driven pipelines.
Second, **reduced cognitive load** — the user configures parameters; the platform handles execution.
Third, **efficient iteration** — caching and modular design mean you only recompute what changed.
Fourth, **transparent reproducibility** — every run is logged with its full configuration.
And fifth, **accessibility** — the interface is intuitive for researchers with coding skills, without requiring deep software engineering background.

Core capabilities include loading BIDS-formatted data, configuring preprocessing, building machine learning datasets, training EEGNet, and exporting results.

---

## Slide 10 — Research Foundation: HBN-EEG Dataset
**~45 sec**

The data we work with is the **Healthy Brain Network EEG dataset** — a large-scale, open-access neuroimaging initiative.

It is BIDS-formatted, has **128-channel** high-density recordings, and covers multiple experimental tasks and diverse subjects spanning different ages, demographics, and clinical backgrounds.

This diversity is what makes it a rigorous testbed.
High dimensionality, multi-task structure, and variable data quality all contribute to the challenge — and to the value of having a structured analysis platform.

---

## Slide 11 — Research Foundation: Why CCD Task
**~45 sec**

We chose to anchor our work on the **Contrast Change Detection task** for several reasons.

It provides **two behavioral targets** simultaneously — accuracy as a binary classification label, and reaction time as a continuous regression target.
This lets us validate the pipeline against two different modeling problems at once.

The stimulus design is clean, the event markers are unambiguous, and there are enough trials per subject for reasonable statistical power.

Our hypothesis: the two-second inter-trial interval before stimulus onset contains neural signatures that are **predictive of the subject's upcoming behavioral response**.

---

## Slide 12 — System Architecture Overview
**~1 min**

*(point to class diagram)*

This is our design class diagram.
The system is organized around a **backend-driven pipeline model** exposed via a FastAPI REST interface, and consumed by a React frontend.

We applied eight design patterns to manage complexity:
- The **Pipeline pattern** chains EEG processing steps cleanly
- The **Facade pattern** isolates the frontend from internal logic
- The **Strategy and Factory patterns** allow behavior to be configured at runtime
- The **Registry pattern** routes tasks to the correct preprocessor
- The **Observer pattern** handles asynchronous progress reporting
- And the **Repository and Composite patterns** manage the cache and session structures

Together these ensure the system is **modular, testable, and extensible**.

---

## Slide 13 — Section Break: SOFTWARE COMPLETION STATUS

*(transition slide — brief pause)*

Let us now review what was actually built and delivered.

---

## Slide 14 — Feature Completion Matrix (Completed)
**~45 sec**

Every core feature we scoped is complete.

Data loading, preprocessing, epoch extraction, dataset building, model training, experiment logging, backend API, and the frontend UI — all delivered.

I want to highlight the **Frontend React UI** in particular.
Because we adopted a modular, mode-action architecture, the frontend is not just a prototype — it is **structurally extensible**.
Adding a new mode or action requires minimal changes to the existing codebase.

---

## Slide 15 — Feature Completion Matrix (Incomplete / Limited)
**~30 sec**

We are transparent about what was not completed or only partially implemented.

WebSocket real-time updates have a basic structure but are not fully integrated.
Model performance — which we will cover in results — is an acknowledged open problem.
Hyperparameter automation and cross-subject generalization are deferred to a future phase.

---

## Slide 16 — What Was Delivered
**~45 sec**

In concrete terms, we delivered:

A full **backend codebase** with clearly separated API, pipeline, AI model, and plotting modules.
A **Frontend React UI** with modular mode-action design supporting both single-subject and cohort-level workflows.
A complete **preprocessing pipeline** — BIDS loading, filtering, artifact removal, and epoching.
A **trained EEGNet model** with logged experiments in Weights & Biases.
Formal **documentation** including the SRS, architecture diagrams, and reproducible notebooks.

Along the way we learned that **caching intermediate results** was the single biggest time-saver in the development cycle, and that **class imbalance** is more dangerous than it first appears.

---

## Slide 17 — Section Break: RESULTS & EVALUATION

*(transition slide — brief pause)*

Now let us look at what the system actually produced when we ran it.

---

## Slide 18 — Manual Testing Results
**~45 sec**

Before ML results, we verified the platform itself through functional testing.

We executed eight representative test cases covering every major operational mode: input configuration, cohort filtering, preprocessing and plotting, grid comparison, data inspection, caching behavior, dataset construction, and model execution.

All eight passed.

This means the **core research workflow is stable and reachable** from end to end.
Note that this testing focused on the expected usage scenario.
Edge cases — corrupted files, missing markers, extremely large cohorts — are identified as areas for future hardening.

---

## Slide 19 — Classification Results
**~1 min**

Our classification task asks: given the prestimulus EEG, can we predict whether the subject will answer correctly?

The baseline model — without any balancing — achieves **72.9% accuracy**, which sounds reasonable.
But look at sensitivity: 0.993. And specificity: 0.009.
The model is predicting **everything as the majority class**. It has learned nothing.

We tried three balancing strategies.
Class weighting, weighted sampling, and undersampling all helped somewhat —
the best result is undersampling at **65.2% accuracy** with more balanced sensitivity and specificity.

But no strategy achieved consistently robust performance.
The class imbalance is severe and the signal in the prestimulus window appears limited for this task.

---

## Slide 20 — Regression Results
**~1 min**

Our regression task asks: can we predict how long the subject will take to respond?

Across all three loss functions — MAE, MSE, and Huber — the R² sits **near zero**.
An R² of zero means the model is essentially predicting the mean reaction time for everyone, regardless of their EEG.

The MAE of roughly **0.29** seconds is close to the standard deviation of the RT distribution — again confirming mean-prediction behavior.

Huber loss performs marginally better, but the difference is not meaningful.

The honest conclusion: either the 2-second prestimulus window does not contain sufficient predictive signal, or our current feature extraction approach is not capturing it.

---

## Slide 21 — What Went Wrong?
**~45 sec**

Let us be direct about the known challenges.

Inter-subject variability in EEG is inherently high — patterns that predict behavior in one person may not generalize to another.
Trial counts per subject are limited, increasing overfitting risk.
Label imbalance caused the classification model to collapse toward the majority class despite our mitigation efforts.
And the prestimulus window itself may simply be an inherently weak predictor of behavioral outcomes at the signal level we are working with.

We treated each of these not as failures but as **well-characterized constraints** that define the scope of Phase 2 work.

---

## Slide 22 — Testing & Validation Protocol
**~45 sec**

Our validation approach had four components.

Functional workflow tests verified the system end-to-end.
Reproducibility checks confirmed that identical configurations produce identical outputs.
We ensured **no data leakage** by using subject-independent splits throughout.
And failure-mode analysis let us understand *why* the model underperformed — not just *that* it did.

All evidence is stored: W&B experiment logs, verification plots including SNR spectra and confusion matrices, and full configuration records for every run.

---

## Slide 23 — Lessons Learned
**~45 sec**

What worked well: the preprocessing pipeline is deterministic, the caching system saved enormous iteration time, the modular architecture made component swaps easy, and comprehensive logging means every result is fully reproducible.

What needs improvement: model generalization is insufficient for practical use, raw spectral features may need richer engineering, and some subjects' data quality was inconsistent enough to affect training stability.

For the next phase, we recommend: transfer learning across subjects, subject-specific model variants, extended time-frequency and connectivity features, and attention-based or graph neural network architectures.

---

## Slide 24 — Overall Project Assessment
**~30 sec**

Overall, this project delivered a **strong engineering foundation**.

The platform is reproducible, well-structured, and usable for real research workflows.
The software side is successful because the pipeline, interface, caching, and experiment tracking are all working together in a systematic way.

At the same time, the predictive performance is still limited.
So the platform is ready, but the model remains the main open technical problem.

---

## Slide 25 — Key Takeaway
**~30 sec**

To close: this project is a success as a **research engineering effort**.

We replaced fragmented, ad-hoc notebooks with a reproducible, structured pipeline.
We built a systematic workflow that any researcher at this lab can now use.
We characterized the failure modes clearly — which makes them solvable.

The platform is ready for focused AI improvement in Phase 2.

Thank you.

---

## Slide 26 — Questions & Discussion
**~open**

*(pause, invite questions)*

We are happy to take questions on:
- The **live demonstration** — I can walk through the interface directly
- The **EEGNet architecture** and why we chose it
- How the platform can be **extended** for other EEG tasks or datasets
- Our **roadmap** for Phase 2

---

> **Total estimated time (slides only, excluding live demo):** ~15–17 minutes  
> **Live demo:** ~10–12 minutes  
> **Q&A:** open
