# Feature Engineering & Selection

**Author:** Ethan Davis · University of Washington

A graduate-level lab notebook on feature engineering and selection for machine learning, using motor-imagery EEG (MI-EEG) classification as a running example. The lab traces the evolution of feature engineering for brain-computer interfacing (BCI) — from classical time/frequency-domain signal processing, to spatial filtering (Common Spatial Patterns), to Riemannian-geometry methods, to modern deep learning — and shows how each approach affects downstream model performance.

## Contents

- **[FeatureEngineering.ipynb](FeatureEngineering.ipynb)** — the main deliverable. A self-contained Jupyter notebook with narrative, code, visualizations, and references.
- **[FeatureEngineering.pdf](FeatureEngineering.pdf)** — supplementary material with a mathematically motivated explanation of Common Spatial Patterns (CSP) and Riemannian geometry for symmetric positive definite (SPD) covariance matrices, referenced from within the notebook.
- **[assets/](assets/)** — figures embedded in the notebook (bias-variance tradeoff, EEG experiment design, motor cortex/homunculus, frequency bands, SPD manifold, ShallowFBCSPNet architecture).
- **[requirements.txt](requirements.txt)** — full pip freeze of the environment the notebook was developed in (originally Google Colab). It's a reference snapshot, not a minimal dependency list — see Setup below for the practical install path.

## What the lab covers

1. **Introduction** — feature engineering vs. model selection, and the bias-variance tradeoff.
2. **Data exploration** — the [BNCI2014_001](https://moabb.neurotechx.com/docs/generated/moabb.datasets.BNCI2014_001.html) MI-EEG dataset ("BCI Competition IV Dataset 2a") accessed via [MOABB](https://moabb.neurotechx.com/docs/index.html), covering EEG experiment structure (sessions/runs/trials), channel montages, and raw signal inspection.
3. **Time & frequency domain features** — power/energy in frequency bands and Hjorth parameters via [MNE-Features](https://mne.tools/mne-features/api.html), plus PCA for dimensionality reduction.
4. **Common Spatial Patterns (CSP)** — the spatial-filtering breakthrough that let simple classifiers dramatically outperform earlier hand-engineered features, using [PyRiemann](https://pyriemann.readthedocs.io/en/latest/).
5. **State of the art: Riemannian geometry** — classification directly on the manifold of SPD covariance matrices.
6. **Active research: deep learning** — ShallowFBCSPNet via [BrainDecode](https://braindecode.org/stable/index.html), and why DL doesn't yet dominate BCI research the way it does other domains.
7. **Conclusion** — a discussion of feature/hyperparameter search strategies (grid search, genetic algorithms, Bayesian optimization with Optuna) and directions for future work.

Model pipelines are benchmarked within MOABB's within-session evaluation and compared by AUROC, so students can see quantitatively how each feature engineering approach changes classification performance on the same left-vs-right hand imagery task.

## Setup

The notebook was written for Google Colab (it installs packages inline and writes cached data to `/content`) but runs in any Jupyter environment.

1. Open `FeatureEngineering.ipynb` in Jupyter or Colab.
2. Run the first code cell, which installs the core packages the rest of the notebook needs:
   ```
   %pip install moabb
   %pip install mne-features
   %pip install braindecode "pandas==2.2.2"
   ```
3. If not running in Colab, replace the `/content` cache paths used for dataset downloads (e.g. `dataset.get_data(cache_config=dict(path="/content", ...))`) with a local directory.
4. Run cells top to bottom. The first run downloads the BNCI2014_001 dataset via MOABB, which may take a few minutes.

`requirements.txt` documents the exact environment used to produce the notebook's outputs, for anyone who wants to reproduce results precisely.

## Prerequisites

This lab assumes familiarity with introductory ML concepts (train/test evaluation, linear classifiers, PCA) and basic signal processing terminology. No prior EEG/BCI background is required — the notebook introduces the necessary domain concepts as they arise.

## References

Full citations for all claims and figures are listed at the end of the notebook.
