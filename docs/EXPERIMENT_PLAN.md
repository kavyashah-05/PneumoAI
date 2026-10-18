# PneumoAI — Experiment Plan

## 1. Objective

The objective of this project is to compare three deep learning models for binary chest X-ray classification:

- Baseline CNN
- ResNet50
- MobileNetV2

The classification task consists of predicting NORMAL or PNEUMONIA from a chest X-ray image.

Pneumonia is treated as the positive class for evaluation.

## 2. Research Questions

The experiments are intended to investigate:

1. How does the Baseline CNN perform compared with ResNet50 and MobileNetV2?
2. How do the models compare in terms of accuracy, precision, recall, F1-score, specificity, and ROC-AUC?
3. How do the models differ in their false-positive and false-negative predictions?
4. Can Grad-CAM visualizations help inspect the image regions associated with model outputs?

These questions describe the project's experimental objectives. They do not, by themselves, establish that every experiment has been completed.

## 3. Dataset and Splits

The project uses the Chest X-Ray Images (Pneumonia) dataset.

The recorded dataset split sizes are:

| Split | Images |
|---|---:|
| Training | 4,172 |
| Validation | 1,044 |
| Test | 624 |
| Total | 5,840 |

The documented methodology describes an 80/20 training-validation split using `random_state=42`, with the original test set kept separate.

These counts and split procedures should be confirmed against the actual dataset and split-generation records before being treated as independently verified.

## 4. Models Under Comparison

### 4.1 Baseline CNN

A custom convolutional neural network serves as the baseline model. It uses grayscale input images resized to 224 × 224 pixels.

### 4.2 ResNet50

ResNet50 uses an adapted final classification layer that produces one output for binary classification. Its inference pipeline uses RGB images resized to 224 × 224 pixels and ImageNet normalization.

### 4.3 MobileNetV2

MobileNetV2 uses an adapted final classification layer that produces one output for binary classification. Its inference pipeline uses RGB images resized to 224 × 224 pixels and ImageNet normalization.

The architectures and inference preprocessing are implemented in `src/multi_model_inference.py`. The exact training configurations should be documented from the training records when available.

## 5. Evaluation Metrics

The project uses the following evaluation metrics to compare model performance.

- **Accuracy:** proportion of all predictions classified correctly.
- **Precision:** proportion of predicted positive cases that are actually positive.
- **Recall (Sensitivity):** proportion of actual positive cases correctly identified.
- **F1-score:** harmonic mean of precision and recall.
- **Specificity:** proportion of actual negative cases correctly identified.
- **ROC-AUC:** area under the receiver operating characteristic curve.

With pneumonia treated as the positive class:

\[
\text{Accuracy}=\frac{TP+TN}{TP+TN+FP+FN}
\]

\[
\text{Precision}=\frac{TP}{TP+FP}
\]

\[
\text{Recall}=\frac{TP}{TP+FN}
\]

\[
F1=2\cdot\frac{\text{Precision}\cdot\text{Recall}}{\text{Precision}+\text{Recall}}
\]

\[
\text{Specificity}=\frac{TN}{TN+FP}
\]

Here, \(TP\), \(TN\), \(FP\), and \(FN\) represent true positives, true negatives, false positives, and false negatives, respectively.

The reported metrics should be tied to the evaluation scripts and results that produced them. Values displayed in the Streamlit application are hard-coded and are not recalculated dynamically by the Model Comparison page.

## 6. Classification Threshold

The implemented inference pipeline applies the sigmoid function to each model's output and classifies scores using a threshold of 0.5:

\[
\hat{y}=
\begin{cases}
\text{Pneumonia}, & p\geq0.5\\
\text{Normal}, & p<0.5
\end{cases}
\]

Threshold analysis is a separate experimental consideration. Any alternative threshold should be documented with its selection method and evaluation results rather than presented as an experiment already completed without supporting evidence.

Sigmoid scores should not automatically be interpreted as calibrated clinical probabilities.

## 7. Error Analysis

The project includes utilities for reviewing test mismatches and generating Grad-CAM visualizations.

Relevant scripts include:

- `review_test_mismatches.py`
- `generate_gradcam_review.py`
- `batch_gradcam_review.py`
- `analyze_thresholds.py`

The intended error analysis includes inspecting false positives and false negatives and examining Grad-CAM overlays for selected cases.

The presence of these scripts does not establish that all analyses have been executed, reviewed, or documented. Completed analyses should be supported by their corresponding output files or execution records.

## 8. Experiment Status and Reproducibility

The project contains model inference implementations, evaluation utilities, and a Streamlit interface for comparing model outputs.

However, a complete reproducible experimental record should also identify, where available:

- Training configurations and hyperparameters.
- Random seeds and split-generation details.
- Checkpoint provenance.
- Evaluation commands and output files.
- The source of each reported metric.
- Any threshold-selection procedure.
- The exact dataset version used.

Do not describe an experiment as completed or reproducible solely because a corresponding script exists.

## 9. Limitations

The experiment compares models on a particular chest X-ray dataset. Results may be affected by dataset composition, image quality, class distribution, duplicate images, and possible differences between training and evaluation preprocessing.

Grad-CAM visualizations provide approximate explanations and do not prove that predictions are medically correct.

The project is an educational research prototype and is not a clinically validated diagnostic system.

## 10. Summary

This experiment plan defines the models, evaluation metrics, and error-analysis methods used or intended for the PneumoAI project. Claims about completed experiments and reported performance should be supported by actual execution records and verified results.