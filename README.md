# 📊 SmartRetail: Next-Month Demand Prediction

## 📌 Project Overview

**SmartRetail: Next-Month Demand Prediction** is a Machine Learning project designed to predict the expected demand for a retail product during the following month.

The system uses historical retail data and current business conditions such as product information, pricing, discounts, marketing expenditure, seasonal factors, holidays, store location, and previous month's demand to generate demand predictions.

The primary goal is to support better business decisions related to:

* 📦 Inventory Planning
* 🚚 Procurement
* 🏭 Warehouse Allocation
* 📊 Retail Demand Management

---

# 🎯 Business Problem

Retail companies need to estimate future product demand to avoid:

* Overstocking products
* Stockouts
* Excess inventory costs
* Poor procurement planning

SmartRetail India Pvt. Ltd. wants to predict:

> **How many units of a specific product are expected to be demanded during the next month?**

For example:

**Current Conditions:**

| Feature               | Value       |
| --------------------- | ----------- |
| Product Category      | Electronics |
| City                  | Kochi       |
| Price                 | ₹2,500      |
| Discount              | 10%         |
| Previous Month Demand | 420 Units   |
| Marketing Spend       | ₹15,000     |
| Festival              | Yes         |

### 🎯 Model Prediction

> **Expected Next-Month Demand: 487 Units**

This prediction can help the business plan inventory and procurement activities in advance.

---

# 🧠 Machine Learning Approach

This project uses:

* **Machine Learning Type:** Supervised Learning
* **Problem Type:** Regression
* **Model:** Random Forest Regressor

The model learns from historical examples where the input conditions and actual next-month demand are already known.

---

# 📂 Dataset

The project uses a synthetic but logically connected Indian retail dataset representing **SmartRetail India Pvt. Ltd.**

Each row represents:

> **One product's business conditions during a particular month at a retail location.**

### Dataset Features

| Feature               | Description                       |
| --------------------- | --------------------------------- |
| Date                  | Current business month            |
| Product_ID            | Unique product identifier         |
| Product_Category      | Product category                  |
| City                  | Retail location                   |
| Store_Type            | Type of retail store              |
| Price                 | Product selling price             |
| Discount_Percentage   | Discount offered                  |
| Marketing_Spend       | Monthly marketing expenditure     |
| Holiday_Flag          | Indicates holiday/festival period |
| Previous_Month_Demand | Demand during the previous month  |
| Season                | Seasonal information              |
| Next_Month_Demand     | 🎯 Target variable                |

---

# 🔄 Machine Learning Pipeline

```text
Business Problem
       ↓
Data Collection
       ↓
Data Understanding
       ↓
Exploratory Data Analysis (EDA)
       ↓
Data Cleaning
       ↓
Feature Engineering
       ↓
Train-Test Split
       ↓
Data Preprocessing
       ↓
Model Training
       ↓
Model Evaluation
       ↓
Demand Prediction
       ↓
Streamlit Application
```

---

# 🔍 Exploratory Data Analysis

The dataset was analysed to understand:

* Data types
* Missing values
* Duplicate records
* Target variable distribution
* Categorical variable distributions
* Correlation between numerical variables
* Potential outliers

### Key Insights

* `Next_Month_Demand` showed a **right-skewed distribution**.
* Most observations represented low to moderate demand levels.
* A small number of high-demand observations were identified.
* `Previous_Month_Demand` showed a **very strong positive correlation (~0.92)** with `Next_Month_Demand`.
* `Price` showed a meaningful negative relationship with demand.
* Discounts showed a weak positive relationship with demand.
* Marketing spend showed a weak linear relationship with demand.

High-demand observations were retained because they may represent legitimate business situations such as festivals, promotions, or seasonal demand spikes.

---

# 🧹 Data Cleaning

The following data-cleaning operations were performed:

* Removed duplicate records
* Handled missing values
* Filled missing numerical values using the median
* Filled missing categorical city values with `Unknown`
* Converted the date column into datetime format
* Investigated potential outliers

Potential demand outliers were not automatically removed because high demand can represent genuine retail events.

---

# ⚙️ Feature Engineering

The original `Date` column was transformed into useful time-based features:

* `Year`
* `Month`
* `Quarter`

The original `Date` column was then removed.

An additional feature was created:

### Discounted Price

```text
Discounted Price = Price × (1 − Discount Percentage / 100)
```

This represents the effective selling price after applying the discount.

---

# 📊 Train-Test Split

Since this project involves predicting future demand, a chronological train-test split was used.

```text
2023 ─────────────── 2024 │ 2025
       TRAINING           │ TESTING
```

### Training Data

* 2023
* 2024

### Testing Data

* 2025

This approach better simulates a real-world forecasting scenario where historical data is used to predict unseen future periods.

---

# 🔧 Data Preprocessing

Categorical variables were transformed using:

### One-Hot Encoding

The preprocessing pipeline uses:

```python
OneHotEncoder(handle_unknown="ignore")
```

This ensures that the application can safely handle unseen categorical values during prediction.

Numerical features were passed directly to the model.

Feature scaling was not required because the primary model used is a **Random Forest Regressor**.

---

# 🤖 Machine Learning Model

The main model used is:

## Random Forest Regressor 🌲

Random Forest was selected because it:

* Handles nonlinear relationships
* Works well with complex feature interactions
* Is robust to different feature scales
* Does not require feature normalization
* Performs well for tabular datasets

---

# 📈 Model Evaluation

The trained model was evaluated using:

### MAE — Mean Absolute Error

Measures the average prediction error in demand units.

### RMSE — Root Mean Squared Error

Penalizes larger prediction errors more heavily.

### R² Score

Measures how much variation in demand is explained by the model.

> **Add your final MAE, RMSE, and R² scores here.**

---

# 🖥️ Streamlit Application

A Streamlit web application was developed to allow users to enter current retail conditions and generate a prediction for the following month's demand.

### User Inputs

The application accepts:

* Product ID
* Product Category
* City
* Store Type
* Product Price
* Discount Percentage
* Marketing Spend
* Holiday/Festival Status
* Previous Month Demand
* Season

### Automatic Features

The application automatically generates:

* Current Year
* Current Month
* Current Quarter
* Discounted Price

The same preprocessing pipeline used during model training is applied to the user input before generating predictions.

---

# 🚀 Running the Project

## 1️⃣ Clone the Repository

```bash
git clone <your-repository-url>
```

## 2️⃣ Navigate to the Project Folder

```bash
cd SmartRetail-Demand-Forecasting
```

## 3️⃣ Install Dependencies

```bash
pip install -r requirements.txt
```

## 4️⃣ Run the Streamlit Application

```bash
streamlit run app.py
```

---

# 📁 Project Structure

```text
SmartRetail-Demand-Forecasting/
│
├── data/
│   ├── smartretail_demand_data.csv
│   └── smartretail_cleaned.csv
│
├── notebooks/
│   ├── Data_Understanding_EDA.ipynb
│   ├── Data_Cleaning.ipynb
│   ├── Feature_Engineering.ipynb
│   └── Model_Training.ipynb
│
├── models/
│   ├── smartretail_random_forest.pkl
│   └── smartretail_preprocessor.pkl
│
├── app.py
├── requirements.txt
└── README.md
```

---

# 💼 Business Value

The demand prediction system can support retail businesses in making better decisions regarding:

### 📦 Inventory Management

Maintain appropriate stock levels and reduce the risk of stockouts.

### 🚚 Procurement Planning

Help procurement teams plan product purchases based on expected demand.

### 🏭 Warehouse Allocation

Improve warehouse space and product allocation planning.

### 💰 Cost Reduction

Reduce unnecessary inventory holding and overstocking costs.

---

# 🔮 Future Improvements

Potential improvements include:

* Adding real-world retail datasets
* Integrating weather information
* Adding competitor pricing data
* Implementing advanced time-series forecasting
* Comparing multiple machine learning models
* Hyperparameter tuning
* Deploying the Streamlit application online
* Adding demand forecasting visualizations and dashboards

---

# 🛠️ Technologies Used

* Python
* Pandas
* NumPy
* Matplotlib
* Seaborn
* Scikit-learn
* Joblib
* Streamlit

---

# 👨‍💻 Author

**Thahasin Jamal**

B.Tech Computer Science Engineering Student | Aspiring Data Professional

---

## ⭐ If you found this project interesting, feel free to star the repository!
