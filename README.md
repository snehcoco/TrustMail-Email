# TrustMail Email Phishing

TrustMail is an explainable hybrid ensemble framework for email phishing detection. It combines email text with phishing-oriented structural features, uses calibrated machine-learning models to classify messages, and provides local explanations for their predictions. The project studies both predictive performance and whether independent models agree on the evidence behind their decisions.

### **Project Overview**

- **Core Architecture:** Combines 5,000 TF-IDF unigram/bigram features and nine phishing-oriented structural features using a calibrated Linear SVM and Random Forest via weighted probability averaging (with a supplementary RBF Kernel SVM option).

- **Explainability & TrustMail:** Uses model-specific SHAP explainers mapped by a rule-based layer into seven human-interpretable phishing concepts and remediation advice, measured via the SHAP Consistency Score (44.03) and Explanation Evidence-Convergence Score (EECS; 62.97) on Enron.

### **Evaluation Highlights**

- **Training & Zero-Shot Testing:** Trained on 41,000 AVN corpus emails and evaluated zero-shot on 28,256 Enron corpus emails, achieving 81.45% accuracy, 84.36% precision, 75.85% recall, and 79.88% F1-score (outperforming a PhishingGNN baseline of 78.50% accuracy and 76.17% F1-score).

- **Key Limitations & Findings:** A 40.0% out-of-vocabulary ratio between AVN and Enron contributes to a cross-dataset performance drop; results reflect evaluation on a broader spam/malicious email corpus (including unsolicited bulk email) rather than a strictly phishing-only test.
## Repository contents

- `Notebooks/` - data preparation, model training, and evaluation notebooks.
- `datasets/` - the source Enron and AVN CSV files.
- `preprocessed_dataset/` - cleaned datasets and engineered NLP features.
- `nlp_features/` - saved feature names, scalers, and vectorization artifacts.
- `results/` - evaluation tables, plots, and statistical test results.
- `phishing_explanation_kb.json` - phishing explanation knowledge base.

## Notebooks

| Notebook | Purpose |
| --- | --- |
| `Enron_preprocess_Decontimination_Optimised.ipynb` | Clean and prepare Enron data, engineer NLP features, and check for cross-corpus duplicates. |
| `nlp_model.ipynb` | Build features and train or evaluate classical, embedding-based, and transformer models. |
| `SVM_Linear_RF_2Model_Enron.ipynb` | Evaluate the linear SVM and random forest models on Enron data. |
| `SVM_Linear_Kernel_RF_3Model_Enron.ipynb` | Compare linear SVM, kernel SVM, and random forest results on Enron data. |
| `Kernel_SVM_AVN_Corpus.ipynb` | Compare held-out and cross-validation results for the kernel SVM on the AVN corpus. |
| `distilbert_enron_zeroshot.ipynb` | Evaluate an AVN-trained DistilBERT model on Enron without retraining. |

## Running the notebooks

The notebooks are set up for Google Colab. Open a notebook and run its setup cells first. 

Install cells list the packages required for that notebook.


## Files excluded from version control

The repository's `.gitignore` consists of:

- Large preprocessed datasets (excluded from this repository due to GitHub's 100 MB per-file size limit): `preprocessed_dataset/final_preprocessed_dataset_nlp.csv` and `preprocessed_dataset/cleaned_nlp_dataset.csv`.
- Trained model checkpoints and directories (excluded from this repository due to GitHub's 100 MB per-file size limit): `*.pkl`, `*.npy`, `bert/`, `distilbert/`, `bert_saved/`, `distilbert_saved/`, and `deep_learning/`.
- Python bytecode and virtual environments: `__pycache__/`, `*.py[cod]`, `.venv/`, and `venv/`.
- Jupyter checkpoint files: `.ipynb_checkpoints/`.
- Environment variables and local IDE settings: `.env` and `.vscode/`.


