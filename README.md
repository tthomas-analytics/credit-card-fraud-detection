# 💳 Credit Card Fraud Detection

> End-to-end fraud detection system using Python, XGBoost and Power BI; identifying $58,000 in recoverable fraud with 97.4% detection rate across 284,807 transactions.

---

## 📊 Power BI Dashboard
![Fraud Detection Dashboard](Powebi%20Dashboard.jpg)
---

## 🔍 Problem Statement

Credit card fraud costs the financial industry billions annually. 
Manual detection is slow, inconsistent and impossible to scale. 
This project builds an automated machine learning pipeline to:

- Detect fraudulent transactions in real time
- Quantify the dollar value of fraud caught vs missed
- Provide actionable recommendations to reduce financial losses

---

## 📁 Project Structure

| Notebook | Description |
|---|---|
| `01_eda.ipynb` | Exploratory Data Analysis — understanding fraud patterns |
| `02_preprocessing.ipynb` | Scaling, train/test split, SMOTE for class imbalance |
| `03_modeling.ipynb` | Training and comparing 3 ML models |
| `04_business_insights.ipynb` | Business recommendations and dollar impact |
| `05_export.ipynb` | Exporting data for Power BI dashboard |

---

## 📂 Dataset

- **Source:** [Kaggle — ULB Credit Card Fraud Detection](https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud)
- **Size:** 284,807 transactions over 48 hours
- **Fraud cases:** 492 (0.17% of total)
- **Features:** V1–V28 (PCA transformed), Amount, Time, Class
- **Note:** Dataset not included due to file size. Download from Kaggle and update the file path in each notebook to match your local setup.

---

## 🔑 Key Findings

1. **Severe class imbalance**: Only 0.17% of transactions are fraud. 
   Accuracy is a misleading metric here — we use Precision, Recall and F1 instead.

2. **Card testing pattern**:  Median fraud transaction is \$9.25 vs \$22.00 
   for legitimate transactions. Fraudsters test stolen cards with small 
   purchases before escalating to larger amounts.

3. **Peak fraud hour**: 2am has the highest fraud rate at 1.713% — 
   over 6x the daily average of 0.275%. Overnight hours need extra monitoring.

4. **Highest losses in mid-range transactions**:  The \$500–\$5k bucket 
   accounts for the highest total fraud losses, followed closely by 
   the \$100–\$500 range.

---

## 🤖 Model Performance

| Model | Precision | Recall | F1 Score |
|---|---|---|---|
| Logistic Regression | 0.06 | 0.92 | 0.11 |
| Random Forest | 0.82 | 0.82 | 0.82 |
| **XGBoost** | **0.73** | **0.89** | **0.80** |

**Final Model: XGBoost**

XGBoost was selected as the final model for its highest Recall of 0.89 — 
catching 89% of all fraud cases. In fraud detection, missing fraud is more 
costly than a false alarm for a bank, making Recall the priority metric 
over overall F1 score.

---

## 💰 Business Impact

| Metric | Value |
|---|---|
| Total transactions analyzed | 284,807 |
| Total fraud cases | 492 |
| Fraud rate | 0.17% |
| Total fraud dollar amount | \$60,128 |
| Fraud caught by model | \$58,292 |
| Fraud missed by model | \$1,836 |
| **Overall detection rate** | **97.4%** |

---

## ✅ Recommendations

1. **Deploy model as real time scoring engine**:  Every transaction 
   receives a fraud probability score before approval. Auto-block 
   transactions with score above 80%.

2. **Implement velocity checks**:  Flag cards making multiple 
   transactions under \$10 in a short time window. This directly 
   targets the card testing pattern identified in the data.

3. **Increase overnight monitoring**:  Fraud rate peaks at 2am 
   at 1.713% — over 6x the daily average. Schedule additional 
   automated alerts during the 12am–4am window.

4. **Focus on high value transactions**: The \$500–\$5k range 
   accounts for the highest total fraud losses. Apply stricter 
   verification for transactions in this range.

5. **Retrain model quarterly**: Fraud patterns evolve over time. 
   Regular retraining ensures the model stays effective against 
   new fraud techniques.

---

## 🛠️ Tech Stack

- **Python** — pandas, numpy, scikit-learn, XGBoost, imbalanced-learn
- **Machine Learning** — XGBoost, Random Forest, Logistic Regression
- **Data Visualization** — Power BI dashboard
- **Imbalance Handling** — SMOTE (Synthetic Minority Oversampling)
- **Environment** — Jupyter Notebook

---

## 🚀 Running on Databricks

This project is structured for enterprise deployment on Databricks.
To run on Databricks:
1. Upload the CSV to DBFS (Databricks File System)
2. Import the notebooks into your Databricks workspace
3. Replace `pd.read_csv('/Users/mac/creditcard.csv')` with 
   `spark.read.csv('dbfs:/path/to/creditcard.csv')`
4. Preprocessing and modeling steps work as-is since pandas 
   and sklearn are available in Databricks clusters

In a production environment, Spark would handle billions of 
transactions in real time — scaling beyond what a single 
machine can handle.

---

## ⚙️ How to Run Locally
```bash
# Clone the repo
git clone https://github.com/tthomas-analytics/credit-card-fraud-detection.git

# Install dependencies
pip install -r requirements.txt

# Run notebooks in order
jupyter notebook
```

Then open and run notebooks 01 through 05 in order.

---

## 📌 Notes

- Dollar figures in the modeling notebook reflect test set performance 
  (20% of data). The Power BI dashboard reflects the full dataset. 
  Both are valid — the notebook shows model evaluation, the dashboard 
  shows full business impact.
