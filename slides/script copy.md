# Presentation Script
## EEG Analysis Platform for Prestimulus EEG-Based Behavioral Prediction

> *(italics)* = stage direction / transition cue

---

## Slide 1 — Title
Good morning. I'm Nantawat, and this is Naytitorn. We're presenting our senior project: the EEG Analysis Platform for Prestimulus EEG-Based Behavioral Prediction.

---

## Slide 2 — BCI and EEG
A Brain–Computer Interface creates a direct link between the brain and a device — without muscles.
EEG records electrical brain activity from the scalp with millisecond-level resolution, making it ideal for event-locked analysis.
*(point to image)*

---

## Slide 3 — Why Reproducible EEG Analysis is Difficult
*(point to graph)* This shows growing subject counts across many different tasks in the HBN dataset.
More tasks, more subjects, more variability — small differences in preprocessing choices lead to completely different results.
This is the challenge we address.

---

## Slide 4 — Practical Gap in EEG Research
Researchers face two bad options: rigid commercial tools, or flexible but fragile custom scripts.
In practice: folders of v1, v2, v3 copies that nobody else can run.
*(point to workflow image)* This is a real lab workflow — already complex before any structure is applied.
Our question: how do we give researchers structure without requiring software engineering expertise?

---

## Slide 5 — Research Objective
We tackle two things: build a reproducible analysis platform, and ask whether **prestimulus EEG** can predict **reaction time** and **trial correctness**.
Dataset: HBN-EEG. Task: Contrast Change Detection. Window: 2-second inter-trial interval.

---

## Slide 6 — Solution Overview
The EEG Analysis Platform is a unified, parameter-driven framework for domain experts.
Key principles: reproducibility, modularity, caching efficiency, and clean separation between domain logic and infrastructure.
Target user: a researcher who codes but shouldn't need to be a software engineer.

---

## Slide 7 — Section Break *(pause)*

---

## Slide 8 — Why This Problem Matters
Without standardized workflows, experiments can't be replicated, knowledge stays fragmented, and researchers spend time on infrastructure instead of science.
Domain experts have EEG knowledge but not software engineering training — the result is fragile, unmaintainable pipelines.

---

## Slide 9 — Our Solution: Design Objectives
Five objectives: systematic workflows, reduced cognitive load, efficient iteration via caching, transparent reproducibility with full logging, and accessibility for coding-capable but non-SE researchers.
Core capabilities: BIDS data loading, preprocessing, dataset building, EEGNet training, and result export.

---

## Slide 10 — HBN-EEG Dataset
The Healthy Brain Network EEG dataset: large-scale, open-access, BIDS-formatted, 128-channel recordings, diverse subjects across ages and clinical backgrounds.
High dimensionality and subject heterogeneity make it a rigorous testbed — and exactly where a structured platform adds value.

---

## Slide 11 — Why CCD Task
The CCD task gives us two behavioral targets at once: correctness (classification) and reaction time (regression).
Clean stimulus design, unambiguous event markers, sufficient trials per subject.
Hypothesis: the 2-second prestimulus window contains neural signatures predictive of upcoming behavior.

---

## Slide 12 — System Architecture
*(point to diagram)* FastAPI backend, React frontend, eight design patterns applied throughout.
Pipeline chains processing steps. Facade isolates the frontend. Strategy and Factory configure behavior at runtime. Registry routes tasks. Observer handles async progress. Repository and Composite manage cache and session structure.

---

## Slide 13 — Section Break *(pause)*

---

## Slide 14 — Feature Completion (Completed)
All core features delivered: data loading, preprocessing, epoch extraction, dataset building, EEGNet training, logging, backend API, frontend UI, and storage.
The frontend uses a **modular mode-action design** — adding new functionality requires minimal code changes.

---

## Slide 15 — Feature Completion (Incomplete)
Transparent about gaps: WebSocket updates are partial, model performance needs improvement, hyperparameter automation and cross-subject generalization are deferred to Phase 2.

---

## Slide 16 — What Was Delivered
Backend, frontend, preprocessing pipeline, trained EEGNet, W&B experiment tracking, SRS documentation, and reproducible notebooks.
Key lessons: caching saved the most development time, and class imbalance is more dangerous than it looks.

---

## Slide 17 — Section Break *(pause)*

---

## Slide 18 — Manual Testing Results
We ran 8 functional test cases across all modes: input config, cohort filter, preprocessing, grid plot, data inspection, caching, dataset build, and model execution. All passed.
The full end-to-end workflow is stable under expected usage. Edge cases are flagged for future hardening.

---

## Slide 19 — Classification Results
Can prestimulus EEG predict trial correctness?
Baseline: 72.9% accuracy — but sensitivity 0.99, specificity 0.009. It predicts everything as the majority class.
Best result: undersampling at 65.2%, but still unstable. Severe class imbalance limits all strategies.

---

## Slide 20 — Regression Results
Can we predict reaction time?
All three loss functions give R² ≈ 0 — the model predicts the mean RT for everyone.
MAE ~0.29 confirms mean-prediction behavior. The prestimulus window may not carry sufficient signal with current feature extraction.

---

## Slide 21 — What Went Wrong?
High inter-subject EEG variability, limited trials per subject, severe label imbalance, and potentially weak predictive signal in the prestimulus window.
These are well-characterized constraints, not surprises — they define the Phase 2 research agenda.

---

## Slide 22 — Testing & Validation Protocol
Functional tests, reproducibility reruns, subject-independent no-leakage splits, and failure-mode analysis.
All evidence logged: W&B exports, SNR spectra, confusion matrices, full configuration records.

---

## Slide 23 — Lessons Learned
What worked: deterministic pipeline, caching, modular architecture, comprehensive logging.
What needs work: model generalization, feature engineering, subject data quality consistency.
Next phase: transfer learning, subject-specific models, time-frequency features, attention/GNN architectures.

---

## Slide 24 — Overall Project Assessment
Reproducibility 9/10, Software Quality 8/10, Usability 7/10, Predictive Performance 3/10, Documentation 9/10.
Strong engineering baseline. Limited AI performance. Platform is ready — the model is the open problem.

---

## Slide 25 — Key Takeaway
Replaced fragmented notebooks with a reproducible, structured pipeline.
Characterized failure modes clearly — they are now solvable in Phase 2.
The platform is ready for focused AI improvement. Thank you.

---

## Slide 26 — Questions & Discussion
*(pause, invite questions)*
Happy to discuss: live demo, EEGNet architecture, extending to other tasks, or Phase 2 roadmap.
