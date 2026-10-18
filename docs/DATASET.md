# PneumoAI — Dataset Documentation

## 1. Dataset Overview

PneumoAI uses the **Chest X-Ray Images (Pneumonia)** dataset for binary chest X-ray image classification.

The two target classes are:

- **NORMAL** — chest X-ray images labelled as normal.
- **PNEUMONIA** — chest X-ray images labelled as pneumonia.

The project uses this dataset to develop and evaluate three deep learning models: Baseline CNN, ResNet50, and MobileNetV2.

## 2. Dataset Source

- **Dataset name:** Chest X-Ray Images (Pneumonia)
- **Dataset source:** Kaggle
- **Dataset identifier:** `paultimothymooney/chest-xray-pneumonia`
- **Expected dataset directory:** `chest_xray/chest_xray/`

The dataset is associated with the Kaggle dataset identifier above. The exact downloaded copy and its contents should be checked against the files available in the project environment.

## 3. Dataset Splits

The project uses training, validation, and test data.

The training portion was divided into training and validation subsets using an 80/20 split, with `random_state=42`, as described in the project's methodology.

The project records the following split sizes:

| Split | Number of images | Status |
|---|---:|---|
| Training | 4,172 | Recorded project count |
| Validation | 1,044 | Recorded project count |
| Test | 624 | Recorded project count |
| **Total** | **5,840** | **Sum of the recorded counts** |

The original test set is described as being kept separate from the training/validation split.

These figures document the counts recorded by the project. They should be confirmed against the actual dataset files and split-generation procedure before being treated as independently verified counts.

## 4. Labels and Classification Task

The project performs binary classification using the following labels:

| Label | Meaning |
|---|---|
| NORMAL | Image labelled as normal |
| PNEUMONIA | Image labelled as pneumonia |

Pneumonia is treated as the positive class when interpreting evaluation metrics.

The models produce a score through a sigmoid function. The current inference implementation uses a threshold of 0.5 to assign the predicted class.

## 5. Preprocessing

The input preprocessing depends on the model.

### Baseline CNN

- Convert the image to grayscale.
- Resize the image to 224 × 224 pixels.
- Convert the image to a tensor.
- Do not apply ImageNet normalization in the implemented inference transform.

### ResNet50 and MobileNetV2

- Convert the image to RGB.
- Resize the image to 224 × 224 pixels.
- Convert the image to a tensor.
- Apply ImageNet normalization using the channel-wise means `[0.485, 0.456, 0.406]` and standard deviations `[0.229, 0.224, 0.225]`.

These steps describe the inference preprocessing implemented in `src/inference.py` and `src/multi_model_inference.py`. The training pipeline should be checked separately to confirm that its preprocessing is consistent.

## 6. Data Integrity and Verification

The repository contains utilities for dataset and evaluation checks, including:

- `audit_dataset.py`
- `check_dataset_duplicates.py`
- `verify_dataset_counts.py`
- `verify_saved_model_vs_csv.py`
- `verify_test_metrics.py`

The existence of these scripts does not establish that every check has been run successfully.

Before declaring the dataset fully verified, confirm:

- The downloaded dataset's source and directory structure.
- The number of images in each split and class.
- Whether duplicate or overlapping images exist across splits.
- Whether the validation set was generated exclusively from the training data.
- Whether preprocessing used during training matches the expected model inputs.

## 7. Licensing and Usage

The applicable dataset license and redistribution terms have not been independently verified in this document.

Check the dataset's original source page and accompanying license information before redistributing images or claiming particular usage permissions. Do not assume that the dataset is unrestricted or that its images may be redistributed freely.

## 8. Limitations

Dataset labels and model predictions should not be interpreted as definitive clinical findings.

The dataset's composition, image quality, class distribution, and potential overlap between splits can affect evaluation results. Results obtained from this dataset alone do not establish generalization to other hospitals, populations, imaging equipment, or clinical settings.

PneumoAI is an educational research prototype and is not a clinically validated diagnostic system.
