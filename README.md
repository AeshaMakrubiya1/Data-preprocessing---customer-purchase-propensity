# 🛒 Customer Purchase Analysis & Feature Engineering Pipeline

<div align="center">

## 📊 Dataset Overview

| File                                                          | Description                                  | Format |
| ------------------------------------------------------------- | -------------------------------------------- | ------ |
| [`customers.csv`](customers.csv)                             | Customer demographics — age, income, region | CSV    |
| [`transactions.json`](transactions.json)                     | Transaction history with amounts & products  | JSON   |
| [`merged_data.csv`](merged_data.csv)                         | Joined customer + transaction data           | CSV    |
| [`processed_customer_data.csv`](processed_customer_data.csv) | Final ML-ready feature set                   | CSV    |

---

## 🔍 Exploratory Data Analysis

### 📈 Univariate Analysis

> Distribution of individual features — age peaks around **40–50**, stock is right-skewed, and income is broadly spread with a wide IQR.

![Univariate Analysis](images/Univariate.png)

---

### 🔗 Bivariate Analysis

> Pairplot coloured by `purchased` (🔵 0 = not purchased · 🟠 1 = purchased). No strong linear separation — motivating the need for feature engineering.

![Bivariate Analysis](images/Bivariate.png)

---

### 🌐 Multivariate Analysis

> Cross-variable relationships across age, income, amount, and price — coloured by purchase outcome to spot group-level patterns.

![Multivariate Analysis](images/Multivariate.png)

---

### 🟥 Correlation Matrix

> Heatmap of Pearson correlations across all numeric features. Most correlations are weak (< |0.15|), confirming feature independence.

![Correlation Matrix](images/correlation.png)

**Key Observations:**

- `total_purchases` ↔ `age`: **+0.15** mild positive correlation
- `income` ↔ `purchased`: **-0.15** mild negative correlation
- All other pairs near **0** → low multicollinearity ✅
- 

## ⚙️ Pipeline Stages

### 1️⃣ Data Cleaning & Missing Value Handling

| Strategy             | Applied To                       |
| -------------------- | -------------------------------- |
| 📐 Mean Imputation   | Numerical columns                |
| 📉 Median Imputation | Skewed numerical columns         |
| 🔤 Mode Imputation   | Categorical columns              |
| 🤖 KNN Imputer       | Complex missing patterns         |
| 🧬 MICE Algorithm    | Advanced multivariate imputation |

---

### 2️⃣ Outlier Handling

- 📐 **Z-score method** — removes statistically extreme values
- 📦 **IQR method** — caps values outside Q1–Q3 range
- 📉 **Percentile method** — clips at 5th / 95th percentile
- 🪣 **Winsorization** — softly caps without removing rows

---

### 3️⃣ 🛠️ Feature Engineering

```python
# ✨ New features created:
purchase_per_day           # Spending frequency metric
days_since_last_purchase   # Recency signal
year, month                # Extracted date components
frequent_buyer             # Binary flag for high-volume buyers
```

---

### 4️⃣ Encoding Techniques

| Technique           | Used For                       |
| ------------------- | ------------------------------ |
| 🏷️ Label Encoding | Binary categories              |
| 🔢 One-Hot Encoding | Nominal multi-class categories |
| 🪜 Ordinal Encoding | Ordered / ranked categories    |

---

### 5️⃣ Feature Scaling

| Scaler             | Best For                       |
| ------------------ | ------------------------------ |
| `StandardScaler` | Normally distributed features  |
| `MinMaxScaler`   | Bounded range features         |
| `RobustScaler`   | Features with outliers present |

---

### 6️⃣ Transformations

- 📊 **Log Transform** — corrects right-skewed distributions
- √ **Square Root** — moderate skew correction
- 🔄 **Yeo-Johnson (PowerTransformer)** — handles zero & negative values

---

## 🗄️ Products Database

The `products.sql` file defines **50 products** across **8 categories**:

| Category       | Count | Price Range      |
| -------------- | :---: | ---------------- |
| 📚 Books       |  10  | ₹490 – ₹2,897 |
| 👗 Clothing    |   8   | ₹103 – ₹2,847 |
| 💄 Beauty      |   7   | ₹185 – ₹1,627 |
| 🏠 Home        |   6   | ₹349 – ₹2,987 |
| 🍎 Food        |   5   | ₹386 – ₹2,283 |
| ⚡ Electronics |   6   | ₹161 – ₹2,514 |
| 🏋️ Sports    |   6   | ₹548 – ₹2,984 |

---

## 🏁 Results & Conclusions

| ✅ Achievement        | Details                                              |
| --------------------- | ---------------------------------------------------- |
| 🧹 Data Completeness  | Multi-strategy imputation removed all missing values |
| 📦 Outlier Stability  | Winsorization & IQR capping stabilised distributions |
| 🛠️ Feature Signal   | Engineered features boost predictive capability      |
| ⚖️ Balanced Scaling | All features contribute equally to ML models         |
| 🚀 ML-Ready Output    | Final dataset ready for classification/regression    |

---

## 🚀 Getting Started

```bash
# 1️⃣ Clone the repository
git clone https://github.com/your-username/customer-purchase-analysis.git
cd customer-purchase-analysis

# 2️⃣ Install dependencies
pip install -r requirements.txt

# 3️⃣ Launch the notebook
jupyter notebook feature_pipeline.ipynb
```

### 📦 Dependencies

```txt
pandas
numpy
scikit-learn
matplotlib
seaborn
scipy
jupyter
```

---

## 📂 Quick Data Access

| 📄 File        | 🔗 Link                                                   |
| -------------- | --------------------------------------------------------- |
| Raw Customers  | [customers.csv](customers.csv)                             |
| Transactions   | [transactions.json](transactions.json)                     |
| Merged Dataset | [merged_data.csv](merged_data.csv)                         |
| Processed Data | [processed_customer_data.csv](processed_customer_data.csv) |
| Products SQL   | [products.sql](products.sql)                               |

---

<div align="center">
