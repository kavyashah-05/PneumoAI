# PneumoAI — Test Plan

## 1. Purpose

This document outlines planned checks for the PneumoAI research prototype. Tests will be added or adapted after the existing implementation is inspected.

## 2. Testing Scope

Testing will focus on:

- Image input and preprocessing.
- Loading and running the existing Baseline CNN, ResNet50, and MobileNetV2 models.
- Prediction output and class-label handling.
- Evaluation metric calculations.
- Grad-CAM generation.
- Application behavior and error handling.

## 3. Planned Test Cases

### 3.1 Image Input and Preprocessing

- Confirm that a supported chest X-ray image can be loaded.
- Check that preprocessing produces the input shape expected by the selected model.
- Confirm that invalid or unreadable image files are handled gracefully.
- Verify that preprocessing used for inference matches the relevant model's documented pipeline.

### 3.2 Model Inference

- Confirm that each existing model can be loaded from its expected weight file.
- Check that inference produces a valid output for a supported image.
- Verify that the output is interpreted consistently with the project's NORMAL/PNEUMONIA labels.
- Confirm that the application reports an understandable error if a required model or weight file is unavailable.

### 3.3 Evaluation Metrics

- Check metric calculations against a small, manually verified set of predictions and labels.
- Verify that pneumonia is treated as the positive class.
- Check that confusion-matrix values and reported metrics use consistent class ordering.
- Confirm that metric calculation handles cases where a metric may be undefined, such as when a class is absent from the evaluated sample.

### 3.4 Grad-CAM

- Confirm that Grad-CAM can be generated for each supported model using its appropriate target layer.
- Check that the resulting heatmap can be aligned with the input image for visualization.
- Verify that failures or unsupported model configurations are reported clearly.

Grad-CAM visualizations are exploratory explanations and are not treated as verified disease localization.

### 3.5 User Interface

- Check that a user can select or upload a supported image.
- Verify that the selected model's prediction is displayed.
- Check that invalid input and unavailable model files produce understandable messages.
- Confirm that any displayed evaluation summaries correspond to the documented evaluation data.

## 4. Test Data

Testing will use suitable sample images and small controlled examples. The final test dataset must remain separate from model training and tuning.

Dataset provenance and test-data handling will follow `docs/DATASET.md`.

## 5. Test Execution and Reporting

As tests are implemented and run, record:

- Test name and purpose.
- Input or test conditions.
- Expected behavior.
- Actual result.
- Pass/fail status.
- Any relevant issue or limitation.

## 6. Current Status

This is a preliminary test plan. Test code, execution results, and final coverage will be documented after the existing implementation has been inspected and verified.