# TrustMail Email Phishing

This repository contains Google Colab notebooks for exploring and classifying phishing emails. The experiments use Enron email data and the AVN corpus to compare text features and machine-learning models.

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

The notebooks are set up for Google Colab. Open a notebook and run its setup cells first. Install cells list the packages required for that notebook.

Some notebooks mount Google Drive and expect model files, datasets, or output folders at paths defined near the top of the notebook. Update those paths to match your Drive setup. In particular, the DistilBERT zero-shot evaluation needs an AVN-trained model and a preprocessed Enron dataset.

For the full workflow, prepare the Enron data before running notebooks that use the generated features or models. Outputs are saved to the paths configured in each notebook; the repository also includes previously generated files in `preprocessed_dataset/`, `nlp_features/`, and `results/`.
