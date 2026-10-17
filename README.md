# PneumoAI

PneumoAI is an educational deep learning research project that explores the classification of chest X-ray images into two categories: **Normal** and **Pneumonia**. It compares multiple deep learning architectures and provides an interactive interface for viewing model predictions and exploring visual explanations.

The project focuses on model comparison, evaluation metrics, and Grad-CAM-based visualisation.

## Project Objectives

- Develop a custom baseline Convolutional Neural Network (CNN).
- Compare its performance with ResNet50 and MobileNetV2.
- Evaluate model performance using standard classification metrics.
- Explore Grad-CAM to visualise image regions influencing model predictions.
- Provide an interactive application using Streamlit.
- Maintain supporting scripts for dataset verification, evaluation, and result analysis.

## Models

PneumoAI includes three model architectures:

| Model | Description |
|---|---|
| Baseline CNN | A custom convolutional neural network used as a reference model. |
| ResNet50 | A residual neural network evaluated for chest X-ray classification. |
| MobileNetV2 | A lightweight convolutional neural network included for comparison. |

The models perform binary classification: Normal or Pneumonia. Pneumonia is treated as the positive class for evaluation.

## Features

- **Multi-model inference:** Load and compare predictions from the three model architectures.
- **Interactive interface:** Explore the application through Streamlit.
- **Performance evaluation:** Analyse classification metrics and model results.
- **Grad-CAM visualisation:** Examine image regions that influence selected model predictions.
- **Dataset verification tools:** Scripts support dataset auditing, duplicate checks, image-count verification, and evaluation checks.
- **Analysis utilities:** Additional scripts support threshold analysis and review of misclassified images.

Feature availability may depend on the required model weights, datasets, and generated result files being present locally.

## Evaluation Metrics

The project considers the following metrics:

- **Accuracy:** Overall proportion of correctly classified images.
- **Precision:** Proportion of predicted pneumonia cases that are actually pneumonia cases.
- **Recall (Sensitivity):** Proportion of pneumonia cases correctly identified.
- **F1-score:** Harmonic mean of precision and recall.
- **Specificity:** Proportion of normal cases correctly identified.
- **ROC-AUC:** Measures the model's ability to distinguish between the two classes across classification thresholds.

## Technology Stack

- **Language:** Python
- **Deep Learning:** PyTorch, Torchvision
- **Data Processing:** NumPy, Pandas
- **Image Processing:** Pillow, OpenCV
- **Evaluation:** Scikit-learn
- **Visualisation:** Matplotlib, Altair
- **Application:** Streamlit

## Repository Structure

```text
PneumoAI/
├── app.py
├── src/
│   ├── inference.py
│   └── multi_model_inference.py
├── scripts/
│   ├── analyze_thresholds.py
│   ├── audit_dataset.py
│   ├── batch_gradcam_review.py
│   ├── check_dataset_duplicates.py
│   ├── generate_gradcam_review.py
│   ├── review_test_mismatches.py
│   ├── verify_dataset_counts.py
│   ├── verify_saved_model_vs_csv.py
│   └── verify_test_metrics.py
├── tests/
├── data/
├── models/
├── results/
├── docs/
├── requirements.txt
├── .gitignore
└── README.md
```

Some directories may contain only placeholder files in the repository. Datasets, trained model weights, and generated results are excluded from version control where configured in `.gitignore`.

## Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/kavyashah-05/PneumoAI.git
cd PneumoAI
```

### 2. Create a virtual environment

On Windows:

```bash
python -m venv .venv
.venv\Scripts\activate
```

On macOS or Linux:

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Add the trained model weights

Create a `models/` directory in the project root if it does not already exist. Place the required checkpoint files inside it:

```text
models/
├── baseline_cnn.pth
├── resnet50_pneumonia.pth
└── mobilenetv2_pneumonia.pth
```

**Important:** These trained model weights are not included in the repository. Obtain the corresponding checkpoints separately before attempting inference. The checkpoints must match the model architectures and parameter configurations expected by the source code.

### 5. Run the application

From the project root, run:

```bash
streamlit run app.py
```

The application may also rely on optional example X-ray images, ROC curves, or Grad-CAM result images. Some visual sections may be unavailable if those generated assets are missing.

## Dataset and Reproducibility

The dataset and trained model checkpoints are not distributed through this repository. Dataset preparation, training, and evaluation depend on the data and configuration used in the research workflow.

For reproducible experiments, document the dataset source, preprocessing steps, train/validation/test split, random seeds, training configuration, checkpoint versions, and evaluation threshold used for each model.

Do not compare reported metrics unless the evaluation data and experimental settings are consistent.

## Explainability

PneumoAI includes Grad-CAM-based visualisation to explore regions of chest X-ray images associated with a model's predictions. The target convolutional layer may differ between architectures.

Grad-CAM visualisations are exploratory explanations of model behaviour. They do not establish that a prediction is medically correct or that the highlighted regions represent clinically meaningful evidence.

## Limitations and Disclaimer

PneumoAI is an **educational research prototype**, not a clinically validated diagnostic system. Its predictions may be affected by dataset limitations, image quality, class imbalance, preprocessing choices, and model bias.

A model's output score should not be interpreted as a calibrated probability of disease or a patient's clinical risk unless calibration has been independently established.

**Do not use this project or its predictions to make medical decisions.** Clinical use would require appropriate external validation, clinical evaluation, and regulatory review.

## License

No license has been specified yet. Unless a license is added to this repository, reuse and redistribution are subject to applicable copyright law.

## Author

**Kavya Shah**

GitHub: [@kavyashah-05](https://github.com/kavyashah-05)
