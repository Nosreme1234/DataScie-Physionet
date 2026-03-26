# Brugada Detection from ECG Signals

A machine learning project for detecting Brugada Syndrome from electrocardiogram (ECG) signals. Built for the **International Data Science Challenge 2026** with the theme _Mathematics for Hope in Healthcare_.

## Overview

Brugada Syndrome is a rare genetic heart disorder that can cause irregular heartbeats and potentially fatal arrhythmias. Early detection through ECG analysis is crucial for patient management. This project leverages machine learning techniques to automatically detect characteristic Brugada patterns in ECG signals, enabling faster and more reliable diagnosis.

## Project Structure

```
DataScie-Physionet/
├── README.md                          # Project documentation
├── requirements.txt                   # Python dependencies
├── features_file.csv                  # Extracted ECG features and labels
├── brugada.ipynb                      # Main model training & comparison notebook
├── brugada-EDA.ipynb                  # Exploratory data analysis
├── preprocessing.ipynb                # Data preprocessing pipeline
├── data/                              # Raw dataset
│   ├── metadata.csv                   # Patient metadata
│   ├── metadata_dictionary.csv        # Data dictionary
│   ├── RECORDS                        # File index
│   └── files/                         # ECG signal files (patient records)
└── model/                             # Trained models & configurations
    ├── brugada_model_metadata.json    # Best model performance metrics
    └── best_model/                    # Serialized model files
```

## Dataset Structure

### Source

PhysioNet Brugada Database: https://physionet.org/lightwave/?db=brugada-huca/1.0.0

### Dataset Details

- **Total samples**: 363 patient ECG recordings
- **Features**: 46 extracted ECG features from preprocessing pipeline
- **Class distribution**:
  - Negative (Normal): 287 samples (79%)
  - Positive (Brugada): 76 samples (21%)
- **Classes**: Binary classification (Normal vs. Brugada syndrome)

### ECG Features

46 features extracted including:

- ST segment characteristics (elevation, slope, curvature)
- T-wave amplitudes and features
- QRS complex measurements (duration, amplitude)
- ST-T segment ratios
- Lead-specific measurements from V1, V2, V3

### Data Dictionary

| Variable      | Description                                     |
| ------------- | ----------------------------------------------- |
| patient_id    | Unique identifier for the patient               |
| diagnosis     | Clinical diagnosis (Normal or Brugada)          |
| sudden_death  | History of sudden cardiac death                 |
| basal_pattern | Whether baseline ECG shows pathological pattern |
| brugada       | Target label for classification                 |

## Models & Results Comparison

### 1. Random Forest Classifier

**Configuration:**

- Bootstrap: False
- Number of estimators: 500
- Max depth: 10
- Criterion: Entropy
- Class weight: balanced_subsample
- Min samples leaf: 8
- Min samples split: 10
- Max features: log2

**Performance Metrics (Test Set):**
| Metric | Score |
|--------|-------|
| Accuracy | **76%** |
| Precision | 47% |
| Recall | 80% |
| F1-Score | 0.59 |
| ROC-AUC | **0.88** |

### 2. XGBoost Classifier (Best Model)

**Configuration:**

- Number of estimators: 300
- Max depth: 6
- Learning rate: 0.05
- Subsample: 0.7
- Colsample bytree: 0.8
- Min child weight: 1
- Gamma: 0.5
- Scale pos weight: 3.78 (based on class imbalance)

**Performance Metrics (Test Set):**
| Metric | Score |
|--------|-------|
| Accuracy | **89%** |
| Precision | **69%** |
| Recall | **90%** |
| F1-Score | **0.78** |
| ROC-AUC | **0.94** |

### Model Comparison Summary

XGBoost provides superior performance:

- **+13% higher accuracy** than Random Forest (89% vs 76%)
- **Better precision** (69% vs 47%) - fewer false positives
- **+10% higher recall** (90% vs 80%) - better at catching Brugada cases
- **+0.06 higher ROC-AUC** (0.94 vs 0.88) - excellent discrimination ability
- **F1-Score of 0.78** indicates excellent balance between precision and recall

**Decision threshold**: 0.5 (tunable based on clinical requirements)

## Installation & Setup

### Prerequisites

- Python 3.8 or higher
- pip or conda package manager

### Installation Steps

1. **Clone the repository**

   ```bash
   git clone https://github.com/Nosreme1234/DataScie-Physionet.git
   cd DataScie-Physionet
   ```

2. **Create and activate virtual environment**

   ```bash
   # Using venv
   python -m venv .venv

   # On Linux/Mac:
   source .venv/bin/activate

   # On Windows:
   .venv\Scripts\activate
   ```

3. **Install dependencies**

   ```bash
   pip install -r requirements.txt
   ```

4. **Download dataset from PhysioNet** (Optional - if not already present)
   ```bash
   wget -r -N -c -np https://physionet.org/files/brugada-huca/1.0.0/
   ```

## Usage

### Running the Notebooks

1. **Exploratory Data Analysis**

   ```bash
   jupyter notebook brugada-EDA.ipynb
   ```

   - Explore class distribution
   - Visualize feature distributions
   - Analyze ECG patterns

2. **Data Preprocessing**

   ```bash
   jupyter notebook preprocessing.ipynb
   ```

   - Extract ECG features from raw signals
   - Generate `features_file.csv`

3. **Model Training & Evaluation**

   ```bash
   jupyter notebook brugada.ipynb
   ```

   - Train Random Forest and XGBoost models
   - Compare performance metrics
   - Generate confusion matrices and feature importance visualizations

## Dependencies

Main Python packages:

- **pandas** (3.0.1) - Data manipulation
- **numpy** (2.4.2) - Numerical computing
- **scikit-learn** - Machine learning algorithms
- **xgboost** - XGBoost classifier
- **imbalanced-learn** - Handling class imbalance
- **matplotlib** (3.10.8) - Data visualization
- **seaborn** - Statistical data visualization
- **jupyter** - Interactive notebooks

See `requirements.txt` for complete list with versions.

## Model Performance Summary

### Data Split

- **Training Set**: 317 samples (87.3%)
- **Test Set**: 46 samples (12.7%)
- **Total Dataset**: 363 samples with 46 features

### Class Distribution

- **Training**: Proportional to overall distribution
- **Test**: Stratified split to maintain class balance
- **Imbalance Ratio**: 3.78:1 (287 negative vs 76 positive)

### Recommended Model: XGBoost

| Aspect                   | Details                                 |
| ------------------------ | --------------------------------------- |
| **Overall Accuracy**     | 89% on test set                         |
| **Sensitivity (Recall)** | 90% - catches most Brugada cases        |
| **Specificity**          | High precision (69%) - few false alarms |
| **ROC-AUC**              | 0.94 - excellent discrimination         |
| **Benchmark vs RF**      | +13% better accuracy                    |

### Model Interpretability

- Feature importance analysis using SHAP values
- Confusion matrix visualization
- Classification reports for precision/recall/F1
- ROC-AUC curves comparing models

## Future Improvements

- Implement deep learning models (CNN, LSTM) for raw ECG signals
- Add cross-validation for more robust evaluation
- Optimize threshold for specific clinical sensitivity/specificity requirements
- Develop API for real-time prediction
- Integration with clinical workflow systems

## References

- **PhysioNet Database**: https://physionet.org/lightwave/?db=brugada-huca/1.0.0
- **Brugada ECG Patterns**: https://litfl.com/brugada-syndrome-ecg-library/
- **ECG Basics**: https://en.wikipedia.org/wiki/Electrocardiography

## Contributors

Developed for International Data Science Challenge 2026

## License

Dataset source: PhysioNet (Credits to HUCA Hospital)

---

**Last Updated**: March 2026
