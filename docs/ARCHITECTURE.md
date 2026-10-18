# PneumoAI — System Architecture

## 1. Overview

PneumoAI is an educational deep learning research prototype for binary chest X-ray image classification. It classifies an input image into one of two classes:

- **NORMAL**
- **PNEUMONIA**

The project implements three deep learning models: Baseline CNN, ResNet50, and MobileNetV2. A Streamlit application provides the user interface for image input, model prediction comparison, model explainability through Grad-CAM, and presentation of evaluation results.

The system is intended for educational and research purposes. It is not a clinically validated diagnostic system and must not be used as a substitute for professional medical assessment.

## 2. High-Level Architecture

The system follows this general processing flow:

1. The user opens the Streamlit application.
2. The user uploads a chest X-ray image or selects an available example where the corresponding image asset exists.
3. The image is converted and preprocessed according to each model's input requirements.
4. The three trained models generate classification scores.
5. The scores are converted using the sigmoid function and classified using a threshold of 0.5.
6. Grad-CAM overlays can be generated to visualize image regions associated with each model's output.
7. The application displays predictions, explanatory visualizations, and recorded evaluation metrics.

## 3. Main Components

### 3.1 Streamlit User Interface

**Implementation:** `app.py`

The application provides eight navigation sections:

- Home
- Understanding Pneumonia
- Chest X-rays
- Project Methodology
- Model Comparison
- Model Explainability (Grad-CAM)
- Try Detection
- Limitations

The interface allows users to explore the project, upload images, compare model predictions, view explainability visualizations, and review recorded evaluation results.

The image-upload functionality accepts PNG, JPG, and JPEG files. Uploaded image information and prediction results are managed through Streamlit session state.

The application also includes error handling for prediction failures and warnings when optional example images or visualization assets are unavailable.

### 3.2 Inference Module

**Implementation:** `src/inference.py`

This module implements standalone ResNet50 inference and ResNet50 Grad-CAM generation.

Its main responsibilities are:

- Initializing the ResNet50 architecture with a single-output classification layer.
- Loading the trained checkpoint from `models/resnet50_pneumonia.pth`.
- Preprocessing input images.
- Generating classification scores and predicted labels.
- Producing a Grad-CAM heatmap overlay for an input image.

The module selects CUDA when available and otherwise uses the CPU.

The ResNet50 model is initialized with `weights=None`, meaning pretrained torchvision weights are not automatically downloaded or loaded. The trained checkpoint supplies the model parameters.

### 3.3 Multi-Model Inference Module

**Implementation:** `src/multi_model_inference.py`

This module provides the shared inference and explainability functionality for all three models.

Its main functions are:

- `load_all_models()` — initializes and loads the three model architectures and their checkpoints.
- `predict_all()` — generates predictions and sigmoid scores for all three models.
- `generate_gradcam_for_model()` — generates a Grad-CAM overlay for an individual model.
- `generate_gradcam_all()` — generates overlays for all three models.

The module checks whether each checkpoint exists before loading it. Missing checkpoints raise a `FileNotFoundError`.

The models are placed in evaluation mode before inference.

## 4. Deep Learning Models

### 4.1 Baseline CNN

The Baseline CNN is a custom convolutional neural network implemented in `src/multi_model_inference.py`.

Its feature extractor contains three convolutional blocks. Each block consists of a convolutional layer, a ReLU activation, and a max-pooling operation.

The classifier consists of:

- A flattening operation.
- A fully connected layer with 128 output features.
- A ReLU activation.
- A dropout layer with probability 0.5.
- A final linear layer producing one output score.

The model accepts single-channel grayscale images resized to 224 × 224 pixels.

### 4.2 ResNet50

ResNet50 is implemented using the torchvision model architecture. Its final fully connected layer is replaced with a linear layer producing one output for binary classification.

The model accepts three-channel RGB images resized to 224 × 224 pixels.

The implementation uses ImageNet normalization with the following channel-wise means and standard deviations:

- Mean: `[0.485, 0.456, 0.406]`
- Standard deviation: `[0.229, 0.224, 0.225]`

The trained checkpoint is stored at `models/resnet50_pneumonia.pth`.

### 4.3 MobileNetV2

MobileNetV2 is implemented using the torchvision model architecture. Its final classifier layer is replaced with a linear layer producing one output for binary classification.

The model uses the same RGB resizing and ImageNet normalization as ResNet50.

The trained checkpoint is stored at `models/mobilenetv2_pneumonia.pth`.

## 5. Image Preprocessing

The three models use different input preprocessing pipelines.

| Processing step | Baseline CNN | ResNet50 | MobileNetV2 |
|---|---|---|---|
| Color format | Grayscale | RGB | RGB |
| Image size | 224 × 224 | 224 × 224 | 224 × 224 |
| Tensor conversion | Yes | Yes | Yes |
| ImageNet normalization | No | Yes | Yes |
| Input channels | 1 | 3 | 3 |

The preprocessing transforms are defined in `src/multi_model_inference.py`. A separate RGB transform for ResNet50 is also defined in `src/inference.py`.

During multi-model inference, the uploaded image is converted separately for the grayscale and RGB pipelines so that each model receives its expected input format.

## 6. Prediction Workflow

For each model, the network produces a single output score, also called a logit.

The sigmoid function converts the logit into a score between zero and one:

\[
p = \sigma(z) = \frac{1}{1+e^{-z}}
\]

where:

- \(z\) is the model's output logit.
- \(p\) is the resulting sigmoid score.

The application uses a threshold of 0.5:

\[
\hat{y} =
\begin{cases}
\text{Pneumonia}, & p \geq 0.5\\
\text{Normal}, & p < 0.5
\end{cases}
\]

The predictions from Baseline CNN, ResNet50, and MobileNetV2 are returned separately so that their outputs can be compared.

**Interpretation note:** The sigmoid output is displayed as a pneumonia score in the application. It should not automatically be interpreted as a calibrated clinical probability or as a measure of diagnostic certainty.

## 7. Model Explainability Using Grad-CAM

Grad-CAM is implemented to generate visual overlays highlighting image regions associated with a model's pneumonia output.

The implementation performs a forward pass, calculates gradients with respect to the model output, averages the gradients across spatial dimensions, and uses the resulting weights to combine feature maps. A ReLU operation and normalization are then applied to produce the heatmap.

The heatmap is resized to the original image dimensions, colored using OpenCV's JET color map, and blended with the original image.

The target layers used by the implementation are:

| Model | Grad-CAM target layer |
|---|---|
| Baseline CNN | `baseline.features[6]` |
| ResNet50 | `resnet.layer4[-1].conv3` |
| MobileNetV2 | `mobilenet.features[-1]` |

The resulting overlays are returned for display in the Streamlit interface.

Grad-CAM is an approximate visualization of model sensitivity to image regions. It does not establish causality, guarantee that highlighted regions are medically meaningful, or validate the prediction.

## 8. Model Evaluation and Comparison

The Model Comparison section of `app.py` presents recorded evaluation metrics and confusion matrices for the three models. The application also attempts to display a saved ROC curve comparison image.

The displayed metrics include:

- Accuracy
- Precision
- Recall
- F1-score
- Specificity
- ROC-AUC

The confusion matrices use actual classes as rows and predicted classes as columns, ordered as Normal and Pneumonia.

The metrics and confusion matrices are hard-coded in the Streamlit application. They are not recalculated dynamically by the Model Comparison page when it is opened.

The ROC curve is loaded from `results/roc_curve_comparison.png` when that file is available. The presence of the displayed values or a referenced image does not, by itself, verify the underlying evaluation procedure or reproduce the reported results. Those details should be checked against the project's evaluation scripts and saved results.

## 9. Model and Visualization Artifacts

The expected trained model checkpoints are:

- `models/baseline_cnn.pth`
- `models/resnet50_pneumonia.pth`
- `models/mobilenetv2_pneumonia.pth`

These files are required for the corresponding trained models to be loaded for inference.

The application also references optional image assets, including:

- `results/xray_examples/normal_example.jpeg`
- `results/xray_examples/pneumonia_example.jpeg`
- `results/roc_curve_comparison.png`
- `results/gradcam/resnet50_false_positive_gradcam.png`
- `results/gradcam/resnet50_false_negative_gradcam.png`

These assets are separate from the model checkpoints. Their availability depends on whether the files are present in the local project environment.

## 10. Limitations

The current implementation has the following limitations:

- The system performs binary classification only.
- Prediction results depend on the trained checkpoints being available and compatible with the model architectures.
- The application uses a fixed classification threshold of 0.5.
- Sigmoid scores are not necessarily calibrated probabilities.
- Evaluation values displayed in the application are hard-coded rather than recomputed by the comparison page.
- Optional example images, ROC curves, and saved Grad-CAM case studies may be unavailable.
- Grad-CAM visualizations are approximate explanations and do not establish clinical correctness.
- The application is an educational research prototype and has not been established as clinically validated.

## 11. Source Files

The principal implementation files relevant to the architecture are:

| File | Responsibility |
|---|---|
| `app.py` | Streamlit interface, image upload, prediction display, model comparison, and explainability pages |
| `src/inference.py` | Standalone ResNet50 inference and Grad-CAM generation |
| `src/multi_model_inference.py` | Three-model loading, preprocessing, prediction, and Grad-CAM generation |
| `analyze_thresholds.py` | Threshold analysis utility |
| `audit_dataset.py` | Dataset auditing utility |
| `batch_gradcam_review.py` | Batch Grad-CAM review utility |
| `check_dataset_duplicates.py` | Dataset duplicate-checking utility |
| `generate_gradcam_review.py` | Grad-CAM review generation utility |
| `review_test_mismatches.py` | Test-mismatch review utility |
| `verify_dataset_counts.py` | Dataset count verification utility |
| `verify_saved_model_vs_csv.py` | Saved-model versus CSV verification utility |
| `verify_test_metrics.py` | Test metric verification utility |

The presence of a verification or analysis script does not imply that it has been executed successfully or that its results have been independently validated.
