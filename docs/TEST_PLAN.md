# PneumoAI — Test Plan

## 1. Objective

This test plan describes the checks used to assess the functionality of PneumoAI, an educational deep learning prototype for classifying chest X-ray images as NORMAL or PNEUMONIA.

The plan covers model loading, image preprocessing, inference, Streamlit functionality, Grad-CAM generation, dataset integrity, and evaluation results.

The existence of a test or verification script does not establish that it has been executed successfully.

## 2. Testing Scope

The following areas are within the testing scope:

- Model checkpoint loading.
- Input image handling and preprocessing.
- Prediction generation for all three models.
- Classification threshold behavior.
- Grad-CAM generation.
- Dataset count and duplicate checks.
- Evaluation metric verification.
- Streamlit interface behavior and error handling.
- Availability of optional example images and visualization assets.

## 3. Model Loading Tests

**Purpose:** Verify that the trained checkpoints can be loaded into their corresponding model architectures.

Expected checkpoint files:

- `models/baseline_cnn.pth`
- `models/resnet50_pneumonia.pth`
- `models/mobilenetv2_pneumonia.pth`

**Expected behavior:**

- Each required checkpoint exists at the expected path.
- The checkpoint parameters match the corresponding model architecture.
- Successfully loaded models are placed in evaluation mode.
- Missing checkpoints produce a clear error rather than silently loading an untrained model.

The multi-model loader explicitly checks for missing checkpoint files. Successful loading still needs to be confirmed by execution.

## 4. Image Input and Preprocessing Tests

**Purpose:** Verify that supported input images can be opened and transformed into the appropriate model inputs.

Test cases:

- Valid RGB image.
- Valid grayscale image.
- PNG, JPG, and JPEG uploads through the Streamlit interface.
- Image conversion to grayscale for Baseline CNN.
- Image conversion to RGB for ResNet50 and MobileNetV2.
- Resizing to 224 × 224 pixels.
- Tensor conversion and the expected normalization for each model.
- Invalid or unreadable image input.

**Expected behavior:**

Valid images should be processed using the correct model-specific transform. Invalid inputs should be handled without causing an uncontrolled application failure.

## 5. Prediction Tests

**Purpose:** Verify that all three models can produce predictions for a valid input image.

The relevant implementation is `src/multi_model_inference.py`, particularly `predict_all()`.

Test cases:

- Run inference with each model loaded.
- Confirm that each model returns a predicted label and sigmoid score.
- Confirm that the predicted label follows the implemented threshold.
- Check that inference executes without gradient calculation during normal prediction.

The classification rule is:

\[
\hat{y}=
\begin{cases}
\text{Pneumonia}, & p\geq0.5\\
\text{Normal}, & p<0.5
\end{cases}
\]

**Expected behavior:** Each model should return a prediction of NORMAL or PNEUMONIA and a numerical score between zero and one for valid, successfully processed inputs.

The score is not necessarily a calibrated clinical probability.

## 6. Grad-CAM Tests

**Purpose:** Verify that the system can generate Grad-CAM overlays for the three supported models.

Relevant functions:

- `generate_gradcam_for_model()`
- `generate_gradcam_all()`
- `generate_gradcam()` in `src/inference.py`

Test cases:

- Generate an overlay for Baseline CNN.
- Generate an overlay for ResNet50.
- Generate an overlay for MobileNetV2.
- Confirm that the overlay has valid image dimensions and can be displayed.
- Confirm that temporary forward or backward hooks are removed after execution.
- Check error handling when Grad-CAM generation fails.

**Expected behavior:** For a valid input and compatible loaded model, the function should return a heatmap overlay in RGB image format.

A successful overlay confirms that the visualization was generated; it does not establish that the model's prediction is correct or that the highlighted region is clinically meaningful.

## 7. Dataset Integrity Tests

The repository contains the following dataset-related utilities:

- `audit_dataset.py`
- `check_dataset_duplicates.py`
- `verify_dataset_counts.py`

These utilities support checking dataset organization, image counts, and potential duplicates.

Test cases:

- Confirm that expected dataset directories exist.
- Compare observed image counts with the recorded split counts.
- Check for potential duplicate images.
- Review any detected anomalies.

**Expected behavior:** The scripts should report discrepancies or potential integrity issues for further investigation.

The results of these checks must be reviewed before declaring the dataset verified.

## 8. Evaluation Verification Tests

The repository contains:

- `verify_test_metrics.py`
- `verify_saved_model_vs_csv.py`
- `analyze_thresholds.py`
- `review_test_mismatches.py`

These utilities support evaluation verification, comparison of saved-model predictions with recorded data, threshold analysis, and test-mismatch review.

Test cases:

- Compare reported evaluation metrics with independently calculated values where the required inputs are available.
- Check confusion-matrix counts and their class ordering.
- Review false-positive and false-negative cases.
- Verify the source of the metrics displayed in the Streamlit application.
- Record any discrepancies between saved results and displayed values.

**Expected behavior:** Reported metrics should be traceable to the corresponding evaluation procedure and data.

The Streamlit Model Comparison page displays hard-coded metrics and confusion matrices. Opening that page does not independently recalculate or validate those values.

## 9. Streamlit Interface Tests

**Purpose:** Verify the main user-facing application workflow implemented in `app.py`.

Test cases:

- Open each navigation section.
- Upload a valid PNG, JPG, or JPEG image.
- Run prediction with all three models.
- Confirm that prediction labels and scores are displayed.
- Confirm that Grad-CAM overlays are displayed when generation succeeds.
- Check the behavior when model loading or inference fails.
- Check warnings for missing example images or saved visualization assets.

**Expected behavior:** The interface should present available results clearly and communicate errors or missing optional assets without implying that unavailable outputs were generated successfully.

## 10. Test Results and Reporting

Test outcomes should be recorded using one of the following statuses:

- **PASS:** The test was executed and the expected behavior was observed.
- **FAIL:** The test was executed and the expected behavior was not observed.
- **NOT RUN:** The test has not been executed or its result has not been recorded.
- **BLOCKED:** The test could not be completed because a required dependency, dataset, checkpoint, or asset was unavailable.

Do not mark a test as PASS based solely on the presence of a corresponding source file or utility script.

Record relevant execution details, observed results, and any corrective action for failed or blocked tests.

## 11. Limitations

This test plan describes checks for an educational research prototype. Passing these tests would not establish clinical validity, regulatory compliance, or suitability for medical decision-making.

The models' performance may depend on the dataset, checkpoint provenance, preprocessing consistency, and evaluation methodology. Grad-CAM visualizations do not independently validate model correctness.