# DiabPredict — Explainable Diabetes Risk Prediction

[![Python](https://img.shields.io/badge/Python-3.x-3776AB?logo=python&logoColor=white)](https://www.python.org/)
[![Task](https://img.shields.io/badge/task-binary%20classification-6E40C9)](#modeling-principles)
[![Explainability](https://img.shields.io/badge/XAI-SHAP-8E44AD)](#interpretability)
[![Language](https://img.shields.io/badge/assistant-Arabic-0F766E)](#project-direction)

> A research prototype for **early diabetes-risk awareness** that prioritizes sensitivity, interpretable predictions, and Arabic-friendly communication.

## Project Scope

DiabPredict explores how machine learning can assist early risk awareness using structured health indicators such as age, BMI, HbA1c level, blood glucose level, hypertension, heart disease, and smoking history. The repository currently contains notebooks and a dataset for experimentation; it is not a production mobile application or a certified clinical diagnostic system.

The system is designed to answer three practical questions:

1. **What is the estimated diabetes risk?**
2. **Which input factors influenced the prediction?**
3. **How can the result be communicated clearly in Arabic without replacing medical advice?**

> **Medical disclaimer:** This is an educational research project. Its predictions must not be used for diagnosis, treatment, or clinical decision-making. A qualified healthcare professional and validated laboratory testing remain essential.

## Modeling Principles

Diabetes screening is a class-imbalanced and safety-sensitive problem. The project therefore emphasizes **Recall** for the positive class: missing a genuinely high-risk case can be more harmful than sending a person for additional assessment. Accuracy alone is not sufficient.

| Evaluation focus | Why it matters |
|---|---|
| Recall / sensitivity | Reduces false negatives in an early-screening setting. |
| Precision | Controls unnecessary follow-up recommendations. |
| F1 score | Balances precision and recall for model comparison. |
| ROC-AUC / PR-AUC | Compares ranking quality under class imbalance. |
| Calibration | Checks whether a reported risk percentage is meaningful. |

Reported metrics should always be recomputed from a clearly separated test set and accompanied by the decision threshold, class distribution, and confusion matrix.

## Explainability and User Output

The intended user-facing output is more informative than a binary label. A future interface should display:

- A calibrated **risk percentage** with an appropriate uncertainty statement.
- A risk category defined by a documented threshold policy.
- The most influential factors, using SHAP or an equivalent explanation method.
- A concise Arabic explanation written in plain, non-diagnostic language.
- A recommendation to seek professional evaluation when risk is elevated.

Feature importance must be interpreted carefully: an association in a predictive model is not evidence that a feature causes diabetes.

## OCR Direction

The `ocr.ipynb` notebook explores extracting laboratory values from a document or report. OCR output should be treated as untrusted input and validated against expected ranges, units, and manual confirmation before it is used by a model. Production use would also require privacy controls, consent, auditability, and clinical validation.

## Repository Contents

```text
README.md
 diabetes_prediction_dataset.csv      # Structured research dataset
diabetes_prediction_project.ipynb     # Main modeling workflow
ocr.ipynb                              # OCR experiment for laboratory values
ocr_file.pdf                           # OCR demonstration input
NN_deibates_project.ipynb              # Additional notebook work
```

## Dataset

The dataset contains the following main fields:

| Field group | Examples |
|---|---|
| Demographics | `gender`, `age` |
| Medical history | `hypertension`, `heart_disease` |
| Lifestyle | `smoking_history` |
| Measurements | `bmi`, `HbA1c_level`, `blood_glucose_level` |
| Target | `diabetes` |

Before publishing results, document the data source, sampling process, missing-value policy, class distribution, and any demographic limitations. A model trained on a public dataset should not be assumed to generalize to Gaza, Palestine, or any other population without local validation.

## Reproduce the Notebooks

The repository is notebook-based and does not currently include a dependency manifest. A clean environment should be prepared before execution:

```bash
git clone https://github.com/Ahmedosrf/DiabPredict-AI-Powered-Diabetes-Risk-Prediction.git
cd DiabPredict-AI-Powered-Diabetes-Risk-Prediction
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\\Scripts\\activate
pip install jupyter pandas numpy scikit-learn matplotlib seaborn shap
jupyter notebook
```

Run `diabetes_prediction_project.ipynb` from top to bottom. Record the random seed, train/test split, preprocessing steps, decision threshold, and all reported metrics so that results can be reproduced.

## Roadmap

The next professional improvements are to add `requirements.txt`, convert repeated notebook code into tested Python modules, implement stratified cross-validation with threshold selection, report recall-focused confidence intervals, calibrate risk probabilities, add fairness checks, and create a Streamlit interface that presents an Arabic risk explanation without exposing sensitive data.

## Maintainer



## License and Responsible Use

Review the license and provenance of the dataset before redistribution. Do not commit identifiable health records, OCR documents containing personal information, API keys, or clinical reports to this repository.
