# 🕵️‍♀️ Identity Fraud Detection

Author: Sravya Kakarlapudi
Type: Machine Learning Project (Classification)
Goal: Detect fraudulent transactions using real-world identity fraud data through advanced preprocessing, model tuning, and ensemble learning.

# 🎯 Objective

The objective of this project is to build and evaluate a machine learning model capable of identifying fraudulent transactions within a highly imbalanced, anonymized dataset.
This work mirrors real-world fraud analytics challenges where data dictionaries are unavailable, and insights must be derived from anonymized numerical and categorical variables.

# 📂 Dataset Overview

The dataset is derived from a real-world identity fraud detection challenge and includes:

File	Description
train_transaction.csv	Transaction-level features and the target variable (isFraud)
train_identity.csv	Identity-related attributes for a subset of transactions

Both datasets were merged using the TransactionID key.

Because the data is anonymized (e.g., variables like V1, C1, id_12, etc.), the exact meaning of each feature is unknown — simulating realistic industry scenarios where privacy or proprietary concerns obscure feature names.

# ⚙️ Data Preprocessing & Feature Engineering

Merging & Missing Value Handling

Performed a left join on TransactionID to retain all transactions.

Dropped columns with more than 75% missing values.

Imputed:

Numerical columns with the mean.

Categorical columns with the mode.

Feature Engineering

missing_ratio_row: proportion of missing values per record.

TransactionAmt_card1_interaction: interaction between amount and card ID.

TransactionAmt_per_TransactionDT: transaction amount normalized by time.

Encoding & Splitting

Applied Label Encoding for categorical features.

Split into training (80%) and testing (20%) sets using stratification.

⚖️ Handling Imbalanced Data

Fraudulent transactions were underrepresented.

Used RandomUnderSampler from imblearn to balance the classes.

This significantly improved Recall for the fraud class while trading off some Precision — a common and acceptable compromise in fraud detection where missing fraud is costlier than false positives.

# 🤖 Model Development
1. Baseline Model

Algorithm: Random Forest Classifier

ROC-AUC: 0.8661

Recall (Fraud): 0.20

Precision (Fraud): 0.89

2. Balanced Model (Undersampling)

Recall (Fraud): 0.77

Precision (Fraud): 0.15

ROC-AUC: 0.8773

Undersampling greatly improved fraud detection sensitivity (Recall), though it introduced more false positives.

3. Hyperparameter Tuned Random Forest

ROC-AUC: 0.9308

Precision (Fraud): 0.20

Recall (Fraud): 0.84

F1-Score (Fraud): 0.33

Tuning significantly boosted all performance metrics and improved the model’s ability to separate fraud from legitimate transactions.

4. LightGBM Model

ROC-AUC: ~0.92

Performed competitively with the tuned Random Forest but with slightly lower precision and recall.

5. Ensemble Model (Voting Classifier)

Combined Tuned Random Forest and LightGBM using soft voting.

ROC-AUC: 0.9335 (highest overall)

Balanced precision-recall tradeoff with robust generalization.

# 📊 Evaluation Metrics
Metric	Description
Precision	How many predicted frauds are actually frauds
Recall (Sensitivity)	How many actual frauds are correctly detected
F1-Score	Harmonic mean of precision and recall
ROC-AUC	Overall ability to discriminate between fraud and non-fraud

In fraud detection, Recall and ROC-AUC are often prioritized to minimize undetected fraud.

# 📈 Key Results Summary
Model	Precision (Fraud)	Recall (Fraud)	F1-Score	ROC-AUC
Random Forest (Baseline)	0.89	0.20	0.33	0.8661
Random Forest (Balanced)	0.15	0.77	0.25	0.8773
Random Forest (Tuned)	0.20	0.84	0.33	0.9308
LightGBM	0.19	0.82	0.31	0.92
Ensemble (RF + LGBM)	0.21	0.83	0.33	0.9335
# 💡 Insights

Balancing the data improved fraud recall substantially.

Hyperparameter tuning achieved the best tradeoff between sensitivity and overall discrimination (ROC-AUC).

Ensembling further improved performance marginally and increased model robustness.

# 🧠 Learnings

Real-world fraud data often comes anonymized and heavily imbalanced.

Proper handling of imbalance (undersampling, tuning, ensembling) is critical for effective fraud detection.

The cost of false negatives (missed fraud) outweighs false positives in most financial applications.

# 🧰 Tech Stack

Python

Pandas, NumPy, Scikit-learn, Imbalanced-learn

LightGBM

Matplotlib, Seaborn

Jupyter Notebook
