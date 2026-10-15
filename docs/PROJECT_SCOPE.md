# PneumoAI — Project Scope

## 1. Project Overview

PneumoAI is a deep learning research project focused on detecting pneumonia from chest X-ray images. It aims to compare a custom Convolutional Neural Network (CNN) with transfer learning models and provide visual explanations of model predictions.

The project is intended for academic research and experimentation, not for clinical diagnosis.

## 2. Project Objectives

- Develop a baseline CNN for binary classification of chest X-ray images.
- Compare the baseline model with ResNet50 and MobileNetV2.
- Evaluate model performance using multiple classification metrics.
- Apply Grad-CAM to visualize image regions influencing model predictions.
- Provide an interface for exploring predictions and model comparisons.
- Maintain a reproducible and well-documented research workflow.

## 3. Classification Task

The system classifies chest X-ray images into two categories:

- **NORMAL:** No pneumonia identified in the dataset label.
- **PNEUMONIA:** Pneumonia identified in the dataset label.

Pneumonia is treated as the positive class during evaluation.

## 4. Planned Models

1. Baseline CNN — a custom convolutional neural network.
2. ResNet50 — a residual network used for transfer learning.
3. MobileNetV2 — a lightweight architecture used for transfer learning.

The models will be evaluated under documented preprocessing and evaluation settings.

## 5. Evaluation Metrics

The project will report:

- Accuracy
- Precision
- Recall (Sensitivity)
- F1-score
- Specificity
- ROC-AUC

The confusion matrix will also be used to examine classification errors.

## 6. Explainability

Grad-CAM will be used to generate heatmap overlays that highlight image regions contributing to model predictions. The target convolutional layer will be selected according to each model architecture.

These visualizations are exploratory explanations, not verified pneumonia segmentations or clinical evidence.

## 7. Intended Application Features

- Chest X-ray image input.
- Predictions from the three models.
- Display of model scores and predicted classes.
- Grad-CAM visualizations.
- Model comparison and evaluation summaries.
- Research methodology and project documentation.

The final interface and feature list will be confirmed against the implementation and current research design.

## 8. Scope Limitations

- The task is limited to binary NORMAL/PNEUMONIA classification.
- Model outputs are not assumed to be calibrated clinical probabilities.
- Performance on the selected dataset does not establish generalization to all hospitals, populations, or imaging equipment.
- The system is not intended to replace professional medical assessment.
- Dataset provenance, split integrity, preprocessing, and evaluation settings must be documented and verified.

## 9. Expected Outcome

The expected outcome is a reproducible research prototype that compares three deep learning approaches, evaluates their classification performance, and explores prediction explainability using Grad-CAM.