# Wearable-EEG Artifact Classification & Denoising Pipeline (BART)
### Laboratory of Wearable Biosignal Processing — Academic Year 2025-26

## 📌 Project Overview
High-amplitude physiological and motion artifacts pose a fundamental challenge for low-density, wearable electroencephalography (EEG). This repository contains a complete pipeline for multi-class artifact classification and denoising on a 4-channel frontal/temporal headset (BART) across 13 subjects, targeting seven categories: eye blinks, leftward and rightward saccades, jaw clenches, horizontal and vertical head movements, and a resting baseline.

The repository includes:
* Detailed preprocessing, digital filtering cascades, and feature engineering implementations.
* A multi-stage hierarchical classification framework benchmarking rule-based models, tree ensembles (Random Forest, XGBoost), and deep networks (1D CNN, EEGNet) under a Leave-One-Subject-Out (LOSO) cross-validation protocol.
* Comparative evaluations of multi-domain signal denoising frameworks (Wavelet transforms, ASR subspace projections, cascades, and residual autoencoders).
* End-to-end inference verification on a entirely held-out blind subject, exploratory data analysis (EDA), and post-hoc Explainable AI (XAI) transparency validation.

For in-depth mathematical formulations, electrode mapping configurations, performance evaluations, and architectural layouts, please refer to the academic paper [report](./report.pdf) (ACL 2023 format) and the companion slide deck [presentation](./presentation.pdf).

---

## 📂 Repository Structure

```text
.
├── data/
│   ├── subjects_metadata.csv      # Demographics and behavioral metadata per subject
│   └── xdf/                       # Raw .xdf recordings for 13 experimental subjects
├── notebooks/
│   ├── 01_Preprocessing.ipynb      # Filtering, outlier-resistant scaling, and feature extraction
│   ├── 02_Thresholding.ipynb       # Rule-based binary baseline (Amplitude/Gradient/Variance)
│   ├── 03_RandomForest.ipynb       # Hierarchical 4-stage Random Forest pipeline
│   ├── 04_XGBoost.ipynb            # Hierarchical 4-stage XGBoost pipeline
│   ├── 05_EEGNet.ipynb             # Deep learning raw temporal pipeline (EEGNet)
│   ├── 06_CNN.ipynb                # Deep learning raw temporal pipeline (1D CNN)
│   ├── 07_Denoising.ipynb          # Wavelet, ASR, Cascade, and Conv-Autoencoder evaluation
│   ├── 08_Full_pipeline.ipynb      # End-to-end inference execution on a held-out blind subject
│   ├── 09_Explanatory_Data_Analysis.ipynb # Spatio-temporal and spectral signal profiling
│   ├── 10_XAI.ipynb                # SHAP / Integrated Gradients model transparency check
│   └── processed_xdf/              # Intermediate artifacts and evaluation plots
│       ├── features.pkl            # 324 hand-crafted features + hierarchical labels
│       ├── windows_raw.pkl         # Raw tensor segments (n × 4 × 500) for DL models
│       ├── window_summary.csv      # Window-level trackable metadata matrix
│       └── *_plots/                # Performance curves and confusion matrices per model
├── report/                         # LaTeX report directory
├── report.pdf                      # Comprehensive academic paper (ACL 2023 format)
├── presentation.pdf                # Project summary slides
├── requirements.txt                # Python environment requirements
└── README.md                       # Project documentation
```

## 🚀 Getting Started
### Prerequisites
Ensure you have a Python 3.11+ environment configured.

### Installation
Clone this project repository, activate your virtual environment and install the required dependencies:

```Bash
python -m venv .venv
source .venv/bin/activate  # On Windows use: .venv\Scripts\activate
pip install -r requirements.txt
```

### Execution Protocol
To execute the complete framework pipeline or reproduce evaluation markers, run the notebooks sequentially:

1. **Extract Data Arrays**: Run `01_Preprocessing.ipynb` to process raw `.xdf` records and generate the intermediate feature (`features.pkl`) and raw tensor (`windows_raw.pkl`) matrices.

2. **Profile & Establish Baselines**: Check signal distributions in `09_Explanatory_Data_Analysis.ipynb`, then run `02_Thresholding.ipynb` to evaluate the rule-based threshold baseline.

3. **Train Classifiers**: Run the classical tree structures (`03_RandomForest.ipynb`, `04_XGBoost.ipynb`) followed by the deep learning models (`05_EEGNet.ipynb`, `06_CNN.ipynb`) to evaluate cross-subject metrics.

4. **Denoise & Evaluate**: Execute `07_Denoising.ipynb` to compare signal restoration filters, then run `08_Full_pipeline.ipynb` to view the end-to-end blind test verification.

## 🤝 Contact

If you have contributions, need support, have suggestions, or just want to get in touch with the authors, feel free to send an email!
* Christian Prendin - [christian.prendin@mail.polimi.it](mailto:christian.prendin@mail.polimi.it)
* Mirko Pica - [mirko.pica@mail.polimi.it](mailto:mirko.pica@mail.polimi.it)
* Jakub Rymarski - [jakub.rymarski@mail.polimi.it](mailto:jakub.rymarski@mail.polimi.it)

## License

This software is licensed under the terms of the MIT license.
See [LICENSE](LICENSE) for more details.
