# TrustMail Email Phishing

TrustMail is an explainable hybrid ensemble framework for email phishing detection. It combines email text with phishing-oriented structural features, uses calibrated machine-learning models to classify messages, and provides local explanations for their predictions. The project studies both predictive performance and whether independent models agree on the evidence behind their decisions.

## Project overview

The primary system represents email bodies with 5,000 TF-IDF unigram and bigram features plus nine phishing-oriented structural features. A calibrated Linear Support Vector Machine (SVM) and a Random Forest provide complementary predictions, combined through weighted probability averaging. A supplementary three-model experiment adds an RBF Kernel SVM.

For explainability, model-specific SHAP explainers estimate local feature contributions. A rule-based layer maps attributions to seven human-interpretable phishing concepts and remediation advice. TrustMail measures explanation agreement with a SHAP Consistency Score (mean 44.03 on Enron) and an Explanation Evidence-Convergence Score (EECS; mean 62.97 on Enron), which combines prediction agreement, probability similarity, concept agreement, and attribution consistency.

## Evaluation highlights

Models are trained on the AVN corpus of 41,000 emails (32,800 training and 8,200 held out). The primary cross-dataset experiment evaluates them on a decontaminated Enron spam and malicious email corpus of 28,256 emails, without retraining. In this zero-shot evaluation, the two-model SVM–Random Forest ensemble reports 81.45% accuracy, 84.36% precision, 75.85% recall, and 79.88% F1-score. A reproduced PhishingGNN baseline evaluated under the same protocol reports 78.50% accuracy, 70.76% recall, and 76.17% F1-score. The supplementary Linear SVM–Kernel SVM–Random Forest ensemble achieves 78.79% accuracy on Enron.

The cross-dataset performance drop is a key finding. The mean out-of-vocabulary ratio between AVN and Enron is 40.0%, indicating substantial vocabulary mismatch that likely contributes to the drop. Enron's positive class includes messages labeled spam, phishing, or malicious, including unsolicited bulk email that may not be credential theft. Results should therefore be interpreted as evaluation on a broader spam and malicious email corpus, not a phishing-only test. The work also examines calibration, ablations, cross-validation, runtime, multi-label tactics, and preliminary adversarial vulnerability. The reported system focuses on lightweight explanations and sub-second inference, while documenting vocabulary shift and attribution disagreement as practical limitations.

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

The repository's `.gitignore` excludes local and generated files that should not be committed:

- Large preprocessed datasets: `preprocessed_dataset/final_preprocessed_dataset_nlp.csv` and `preprocessed_dataset/cleaned_nlp_dataset.csv`.
- Trained model checkpoints and directories: `*.pkl`, `*.npy`, `bert/`, `distilbert/`, `bert_saved/`, `distilbert_saved/`, and `deep_learning/`.
- Python bytecode and virtual environments: `__pycache__/`, `*.py[cod]`, `.venv/`, and `venv/`.
- Jupyter checkpoint files: `.ipynb_checkpoints/`.
- Environment variables and local IDE settings: `.env` and `.vscode/`.

