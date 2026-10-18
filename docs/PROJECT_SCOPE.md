# PneumoAI — Project Scope

## 1. Project Overview

PneumoAI is an educational deep learning research prototype for classifying chest X-ray images into two categories: NORMAL and PNEUMONIA.

The project compares three models: Baseline CNN, ResNet50, and MobileNetV2. A Streamlit interface provides image-based inference, model comparison, and Grad-CAM visualizations.

The project is intended for educational and research purposes, not for clinical diagnosis.

## 2. Project Objectives

The main objectives are to:

- Implement three deep learning models for binary chest X-ray classification.
- Compare their predictions and recorded evaluation metrics.
- Provide a user interface for uploading and analyzing chest X-ray images.
- Generate Grad-CAM visualizations to inspect regions associated with model outputs.
- Provide utilities for dataset auditing, threshold analysis, and evaluation verification.
- Document the system architecture, dataset, experimental plan, and testing approach.

## 3. In-Scope Features

### 3.1 Image Classification

The implemented inference modules support classification into NORMAL and PNEUMONIA using:

- Baseline CNN
- ResNet50
- MobileNetV2

The models produce sigmoid scores and predicted classes using a threshold of 0.5.

### 3.2 Image Upload and User Interface

The Streamlit application supports PNG, JPG, and JPEG uploads through its image-detection interface.

It presents predictions from the three models and handles prediction errors through the interface.

### 3.3 Model Comparison

The application displays recorded evaluation metrics, including accuracy, precision, recall, F1-score, specificity, and ROC-AUC, alongside confusion matrices.

The displayed metrics and confusion matrices are hard-coded in the application rather than dynamically calculated by the comparison page.

### 3.4 Model Explainability

The project implements Grad-CAM generation for all three models. The generated overlays can be used to inspect image regions associated with each model's output.

Grad-CAM visualizations are approximate and do not establish that a prediction is correct or clinically meaningful.

### 3.5 Dataset and Evaluation Utilities

The repository includes scripts for dataset auditing, duplicate checking, count verification, threshold analysis, test-mismatch review, Grad-CAM review, and evaluation checks.

The presence of these scripts does not imply that every check has been run successfully.

## 4. Out-of-Scope Features

The following are outside the current project's established scope:

- Clinical diagnosis or treatment recommendations.
- Clinical deployment or integration into hospital workflows.
- Guaranteed detection of pneumonia in every patient.
- A claim of clinical validation or regulatory approval.
- Automated medical reporting or treatment planning.
- A guarantee that sigmoid scores represent calibrated clinical probabilities.

These exclusions describe the intended boundaries of the educational prototype.

## 5. Technical Scope

The implementation uses Python, PyTorch, torchvision, Streamlit, Pillow, NumPy, and OpenCV.

The primary application and inference files are:

- `app.py`
- `src/inference.py`
- `src/multi_model_inference.py`

The expected trained model checkpoints are:

- `models/baseline_cnn.pth`
- `models/resnet50_pneumonia.pth`
- `models/mobilenetv2_pneumonia.pth`

The corresponding checkpoint files must be present and compatible with the model architectures for inference to work.

## 6. Assumptions and Dependencies

The project assumes that:

- The required Python dependencies are installed.
- Compatible trained model checkpoints are available.
- Input images can be opened and converted to the required image formats.
- Dataset counts and evaluation values are checked against their original records before being reported as verified results.
- Optional example images and saved visualizations are available if those interface sections are expected to display them.

## 7. Limitations

The current prototype has several limitations:

- It performs binary classification only.
- It uses a fixed classification threshold of 0.5.
- Model scores are not necessarily calibrated probabilities.
- Reported evaluation values are displayed as recorded constants in the Streamlit interface.
- Some example images and visualization assets may be absent from the repository.
- Grad-CAM provides approximate visual explanations rather than proof of model reasoning.
- Performance on one dataset does not establish generalization to other clinical environments.

## 8. Deliverables

The project deliverables include:

- Three model inference implementations.
- A Streamlit application for prediction and model comparison.
- Grad-CAM generation functionality.
- Dataset and evaluation utility scripts.
- Project documentation covering architecture, dataset, experimental planning, scope, structure, and testing.

The completion and reproducibility of individual experiments should be established from their execution records and saved outputs.

## 9. Success Criteria

The project is considered technically demonstrable when:

- The three models can be loaded from compatible checkpoints.
- Each model can process an appropriate input image and return a prediction.
- The Streamlit interface can display model predictions.
- Grad-CAM overlays can be generated for the supported models.
- Evaluation values and their sources are documented clearly.
- The documented limitations and non-clinical intended use are explicit.

These criteria describe the intended technical demonstration; they should not be interpreted as proof that every item has been tested successfully.