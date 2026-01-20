# 💳 Credit Card Fraud Detection (Unsupervised Learning)

## 🎯 Objective
Build an **Unsupervised Machine Learning model** capable of detecting fraudulent transactions in highly imbalanced credit card data.
The project focuses on **Anomaly Detection** using the **Isolation Forest** algorithm to identify "weird" patterns without needing labeled training data.

---

## ❓ Problem
This is an **Anomaly Detection task**.

The dataset contains transactions made by credit cards in September 2013 by European cardholders.
- **Challenge:** The dataset is highly imbalanced. Out of 284,807 transactions, only **492** are frauds (0.172%).
- **Features:** 28 anonymized PCA components (`V1` to `V28`), `Time`, and `Amount`.

The goal is to flag:
- **1 (Normal) → Safe Transaction**
- **-1 (Anomaly) → Potential Fraud**

---

## 🛠 Tech Stack

- **Language:** Python 3.10+
- **Data Manipulation:** Pandas, NumPy
- **Machine Learning:** Scikit-Learn
  - Isolation Forest (Unsupervised)
  - StandardScaler / RobustScaler
- **Visualization:** Matplotlib, Seaborn
- **Model Persistence:** Joblib

---

## 📂 Project Structure
*Note: The `data` folder is not included in this repository due to size limits.*

```text
credit_card_fraud_project/
├── notebook/              # Jupyter Notebooks
│   └── Anomaly_detection.ipynb
├── .gitignore             # Excludes large data files
├── credit_card_model.pkl  # Saved Production Model
├── LICENSE                # MIT License
├── README.md              # Project documentation
└── requirements.txt       # Python dependencies
```

## 🚀 How to Run
1. Clone the Repository
```bash

git clone [https://github.com/Ahmxd-ui/credit_card_fraud_project.git](https://github.com/Ahmxd-ui/credit_card_fraud_project.git)
cd credit_card_fraud_project
```

2. Install Dependencies
```Bash

pip install -r requirements.txt
```
3. Setup Data (Crucial Step)

Since the dataset is large, it is not hosted in this repository.

    Download creditcard.csv from Kaggle.

    Create a new folder named data/ in the project root.

    Place the creditcard.csv file inside that data/ folder.

(Your code expects the path: data/creditcard.csv)
4. Run the Notebook

Open notebook/Anomaly_detection.ipynb in VS Code or Jupyter to run the pipeline.
## 📋 Examples

Input Data (Anonymized):
V1	V2	...	V28	Amount
-1.35	-0.07	...	-0.02	149.62
1.19	0.26	...	0.01	2.69

Model Output:
Transaction ID	Anomaly Score	Prediction
001	-0.15	-1 (Fraud)
002	0.65	1 (Safe)

## 🧩 Machine Learning Pipeline

This project follows an Unsupervised Learning workflow:
Code snippet
```powershell
graph TD;
    A[Raw Data] --> B[Data Scaling (StandardScaler)];
    B --> C[Isolation Forest Model];
    C --> D[Anomaly Scoring];
    D --> E[Threshold Tuning (Contamination)];
    E --> F[Final Fraud Predictions];
```
## 🧪 Tests & Evaluation

Since fraud is rare, Accuracy is not a good metric. We optimized for Recall (catching thieves) while monitoring Precision (avoiding false alarms).

Evaluation Strategy:

    We tuned the contamination parameter to balance the trade-off.

    Winner Parameter: contamination=0.018

## 📊 Model Performance
Metric	Score	Interpretation
Recall	65.2%	We caught 65% of all frauds without ever seeing a label.
Precision	6.3%	For every 100 alerts, ~6 are real fraud (acceptable for a first-pass filter).
F1-Score	0.114	The harmonic mean of Precision and Recall.
## 💡 Key Takeaways

    Unsupervised Power: Successfully detected majority of fraud cases without "knowing" what fraud looked like beforehand.

    Handling Imbalance: Used Isolation Forest to isolate outliers instead of trying to classify them.

    Hyperparameter Tuning: Found the "sweet spot" (0.018) where we catch the most fraud without flagging too many innocent users.

    Scalability: The model is saved (.pkl) and ready for deployment.

## 🔐 Authentication

No authentication required. This is a standalone local machine learning project.
## 📜 License

This project is licensed under the MIT License. See the LICENSE file for more details.