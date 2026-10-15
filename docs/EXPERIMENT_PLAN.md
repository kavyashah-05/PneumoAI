# PneumoAI — Experimental Plan

## 1. Objective

The objective is to compare three deep learning approaches for binary pneumonia classification using chest X-ray images.

## 2. Models Under Comparison

1. **Baseline CNN:** A custom convolutional neural network serving as the baseline.
2. **ResNet50:** A residual network evaluated using transfer learning.
3. **MobileNetV2:** A lightweight convolutional neural network evaluated using transfer learning.

The exact model configurations and training settings will be documented during implementation.

## 3. Classification Task

The models will classify each image into one of two classes:

- **NORMAL:** No pneumonia identified in the dataset label.
- **PNEUMONIA:** Pneumonia identified in the dataset label.

Pneumonia will be treated as the positive class when calculating evaluation metrics.

## 4. Dataset and Data Splits

The dataset source, image counts, class distribution, and train/validation/test split will be verified and documented before training.

- **Training set:** Used to learn model parameters.
- **Validation set:** Used for model selection and appropriate tuning decisions.
- **Test set:** Reserved for final evaluation after model development and selection.

The test set must not be used to repeatedly tune model configurations or classification thresholds.

## 5. Image Preprocessing

Image resizing, image format, normalization, and other preprocessing requirements will be documented for each model.

Any model-specific preprocessing must be applied consistently during training, validation, and inference.

Data augmentation, if used, will be applied only to the training data.

## 6. Evaluation Metrics

All three models will be evaluated using:

- Accuracy
- Precision
- Recall (Sensitivity)
- F1-score
- Specificity
- ROC-AUC

A confusion matrix will also be reported to examine false-positive and false-negative predictions.

## 7. Classification Threshold

The models' output scores and the threshold used to assign predicted classes will be documented.

Any threshold selection using validation data must be completed before final test evaluation. Output scores will not automatically be interpreted as calibrated clinical probabilities.

## 8. Explainability

Grad-CAM will be used to generate heatmap visualizations for selected predictions. The target convolutional layer will be chosen according to each model's architecture.

These visualizations will be treated as exploratory explanations, not as verified pneumonia localization or clinical evidence.

## 9. Reproducibility

The project will document relevant experimental settings, including model configuration, preprocessing, training parameters, random seeds where applicable, and evaluation procedures.

Any limitations or differences that affect a fair model comparison will be reported.

## 10. Research Limitations

Results will be interpreted in the context of the selected dataset and experimental setup. Strong performance on one dataset does not establish generalization to other hospitals, populations, or imaging systems.

## 11. Status

This is a preliminary experimental plan. Dataset details and final experimental settings will be confirmed before model training and final evaluation.