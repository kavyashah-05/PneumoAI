# PneumoAI — System Architecture

## 1. Overview

PneumoAI follows a modular architecture that separates the user interface, model inference, explainability, and evaluation components. This structure helps keep the project organized, maintainable, and easier to test.

## 2. Main Components

### User Interface
Provides an interface for uploading a chest X-ray image, selecting a model, viewing predictions, and exploring Grad-CAM visualizations.

### Model Inference
Loads the trained Baseline CNN, ResNet50, and MobileNetV2 models and generates predictions for input images.

### Image Preprocessing
Prepares uploaded images according to the input size, color format, and normalization requirements of the selected model.

### Explainability Module
Uses Grad-CAM to produce heatmaps that help visualize image regions influencing a model's prediction.

### Evaluation Module
Calculates classification metrics, including accuracy, precision, recall, F1-score, specificity, and ROC-AUC, using labeled evaluation data.

## 3. High-Level Workflow

1. The user uploads a chest X-ray image.
2. The image is validated and preprocessed.
3. The selected trained model performs inference.
4. The application displays the predicted class and pneumonia score.
5. Grad-CAM optionally generates an explanatory heatmap.
6. Evaluation results are presented separately using labeled test data.

## 4. Planned Technology Stack

- **Programming language:** Python
- **Deep learning:** PyTorch and Torchvision
- **User interface:** Streamlit
- **Image processing:** Pillow and OpenCV
- **Data analysis:** NumPy and Pandas
- **Evaluation:** Scikit-learn
- **Visualization:** Matplotlib and Streamlit charts
- **Version control:** Git and GitHub

## 5. Project Structure

The project will be organized into separate modules for application code, inference, explainability, evaluation, tests, documentation, and supporting configuration files. The structure may evolve as implementation requirements become clearer.

## 6. Design Considerations

- Keep model-specific inference logic modular.
- Apply the correct preprocessing pipeline for each model.
- Avoid committing datasets, trained model weights, or virtual environments to GitHub.
- Keep evaluation results separate from predictions on individual uploaded images.
- Document important experimental settings for reproducibility.
- Present predictions as research outputs, not as medical diagnoses.

## 7. Architecture Status

This document describes the planned architecture. It will be updated as the implementation is developed and verified.