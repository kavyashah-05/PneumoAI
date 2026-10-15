# PneumoAI — Project Structure

## 1. Purpose

This document describes the organization of the PneumoAI repository. The structure is intended to keep source code, documentation, tests, data placeholders, and generated results organized.

## 2. Current Repository Structure

```text
PneumoAI/
├── data/
│   └── .gitkeep
├── docs/
│   ├── ARCHITECTURE.md
│   ├── EXPERIMENT_PLAN.md
│   ├── PROJECT_SCOPE.md
│   └── PROJECT_STRUCTURE.md
├── results/
│   └── .gitkeep
├── src/
│   └── __init__.py
├── tests/
│   └── .gitkeep
├── .gitignore
└── requirements.txt
```

## 3. Directory Responsibilities

- **`docs/`** — Project scope, architecture, experimental methodology, and other technical documentation.
- **`src/`** — Python source modules for the application and model-related functionality.
- **`tests/`** — Automated tests for verifying project functionality.
- **`data/`** — Local dataset location; dataset contents are excluded from version control.
- **`results/`** — Location for generated evaluation results and outputs; generated contents are excluded from version control.

## 4. Root Files

- **`.gitignore`** — Excludes virtual environments, temporary files, datasets, trained model weights, and generated outputs.
- **`requirements.txt`** — Lists the Python dependencies required by the project.
- **`src/__init__.py`** — Marks `src` as a Python package.

## 5. Structure Policy

The repository will evolve incrementally as existing implementation requirements are verified. New modules and directories will be introduced only when needed.

The structure must remain compatible with the intended PneumoAI implementation and its existing model, inference, evaluation, and Grad-CAM components.