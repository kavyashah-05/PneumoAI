# PneumoAI — Dataset Documentation

## 1. Purpose

This document records the dataset used for PneumoAI's pneumonia classification experiments. Dataset details must be verified against the actual data and project records before training or final evaluation.

## 2. Dataset Source

- **Dataset name:** To be verified.
- **Original source or repository:** To be recorded.
- **Access date or version:** To be recorded.
- **License and permitted use:** To be verified and documented.

## 3. Classification Labels

The project uses two image classes:

- **NORMAL:** Image labeled as normal in the dataset.
- **PNEUMONIA:** Image labeled as pneumonia in the dataset.

Pneumonia is treated as the positive class for evaluation.

## 4. Dataset Splits

The dataset's training, validation, and test splits will be recorded after checking the actual dataset and its accompanying documentation.

| Split | Image count | NORMAL count | PNEUMONIA count |
|---|---:|---:|---:|
| Training | To verify | To verify | To verify |
| Validation | To verify | To verify | To verify |
| Test | To verify | To verify | To verify |

Counts must be checked against the data actually used in the experiments.

## 5. Data Integrity Checks

Before model training, the project should verify:

- Image counts and class distribution for each split.
- Whether images can be opened and processed.
- Whether duplicate or overlapping images exist across splits.
- Whether the provided split organization is preserved.
- Whether any preprocessing or filtering changes the dataset counts.

## 6. Preprocessing

The image size, color-channel handling, normalization, and any other preprocessing steps will be documented once verified from the actual model pipelines.

Training-only augmentation, if used, will be recorded separately.

## 7. Data Limitations

Dataset composition, labeling quality, collection setting, and representativeness may affect model performance. Results should be interpreted in the context of the dataset used and should not be assumed to generalize to every clinical setting.

## 8. Verification Status

Dataset source, license, split counts, and integrity checks remain to be verified against the project data and supporting records. This document will be updated when those checks are complete.