# PneumoAI — Project Structure

## 1. Purpose

This document describes the current Git-tracked structure of PneumoAI. The repository contains the Streamlit application, model inference modules, dataset and evaluation utilities, project documentation, and configuration files.

## 2. Current Repository Structure

```text
PneumoAI/
├── app.py
├── analyze_thresholds.py
├── audit_dataset.py
├── batch_gradcam_review.py
├── check_dataset_duplicates.py
├── generate_gradcam_review.py
├── review_test_mismatches.py
├── verify_dataset_counts.py
├── verify_saved_model_vs_csv.py
├── verify_test_metrics.py
├── requirements.txt
├── .gitignore
├── README.md
├── FINAL_AUDIT_REPORT.md
├── data/
│   └── .gitkeep
├── docs/
│   ├── ARCHITECTURE.md
│   ├── DATASET.md
│   ├── EXPERIMENT_PLAN.md
│   ├── PROJECT_SCOPE.md
│   ├── PROJECT_STRUCTURE.md
│   └── TEST_PLAN.md
├── results/
│   └── .gitkeep
├── src/
│   ├── __init__.py
│   ├── inference.py
│   └── multi_model_inference.py
└── tests/
    └── .gitkeep
```

This tree represents files tracked by Git at the time of documentation review. Local, untracked files and ignored files are not included.

## 3. Application and Source Code

### `app.py`

Contains the Streamlit application entry point. It provides the user-facing interface for the PneumoAI workflow.

### `src/`

Contains the model inference modules:

- `inference.py` — inference implementation for ResNet50.
- `multi_model_inference.py` — inference utilities for the Baseline CNN, ResNet50, and MobileNetV2.

### Root-level analysis and verification scripts

The following scripts support dataset inspection, evaluation checks, and analysis:

- `analyze_thresholds.py` — classification-threshold analysis.
- `audit_dataset.py` — dataset auditing.
- `batch_gradcam_review.py` — batch Grad-CAM review.
- `check_dataset_duplicates.py` — duplicate-image checks.
- `generate_gradcam_review.py` — Grad-CAM review generation.
- `review_test_mismatches.py` — review of test-set mismatches.
- `verify_dataset_counts.py` — dataset-count verification.
- `verify_saved_model_vs_csv.py` — comparison of saved-model predictions against CSV records.
- `verify_test_metrics.py` — test-metric verification.

The descriptions above indicate each script's intended role based on its filename. Exact behavior and verification coverage should be confirmed from the implementation and execution results.

## 4. Data and Results Directories

- `data/` — placeholder for local dataset files. Dataset contents are not represented in the tracked tree.
- `results/` — placeholder for generated outputs, evaluation artifacts, and visualizations.

The `.gitkeep` files preserve these otherwise-empty directories in Git. Actual datasets and generated results may be excluded by `.gitignore`.

## 5. Documentation

- `README.md` — project overview, setup instructions, model requirements, and limitations.
- `FINAL_AUDIT_REPORT.md` — project audit documentation.
- `docs/ARCHITECTURE.md` — system architecture.
- `docs/DATASET.md` — dataset provenance, splits, preprocessing, and integrity checks.
- `docs/EXPERIMENT_PLAN.md` — experimental methodology and model-comparison plan.
- `docs/PROJECT_SCOPE.md` — project objectives, features, and limitations.
- `docs/PROJECT_STRUCTURE.md` — repository organization.
- `docs/TEST_PLAN.md` — planned testing and verification activities.

## 6. Configuration and Dependencies

- `.gitignore` — specifies files and directories Git should ignore.
- `requirements.txt` — lists the Python packages required by the project.
- `src/__init__.py` — initializes the `src` Python package.

## 7. Model Weights and Local Artifacts

The inference modules expect trained model checkpoints under `models/`:

- `baseline_cnn.pth`
- `resnet50_pneumonia.pth`
- `mobilenetv2_pneumonia.pth`

The `models/` directory and checkpoint files are not currently present in the Git-tracked structure. They must be supplied locally before the corresponding inference functions can load the models.

Local virtual environments, untracked backup files, datasets, and ignored artifacts are outside the tracked repository structure.

## 8. Structure Policy

The repository retains its existing organization, with analysis and verification scripts at the root level and inference modules under `src/`.

Any future structural changes should be made when justified by implementation needs. Documentation should be updated whenever the tracked repository structure changes.

## 9. Status

This document reflects the Git-tracked repository structure observed during the documentation review. It describes file organization; it does not by itself establish that every application feature, model, or verification script has been executed successfully.
