# Customer Churn Prediction System

A Machine Learning project that predicts whether a bank customer is likely to **exit (churn)** or **stay** based on customer information.

The project uses a trained **Random Forest Classifier** and a **Streamlit** web interface for real-time prediction.

---

## 📌 Project Overview

### Problem Statement

The bank aims to minimize customer attrition by identifying customers who are likely to discontinue their relationship with the bank. Using historical customer data, the project develops a predictive analytics solution that can support proactive engagement and personalized retention efforts.

### Objective

The main objectives of this project are:

- Predict whether a customer is likely to leave the bank.
- Estimate the probability of customer churn.
- Estimate the probability that the customer will stay.
- Display model confidence.
- Provide a simple and attractive web interface.
- Help demonstrate how Machine Learning can support customer-retention decisions.

---

# 🧠 Machine Learning Approach

The project uses a **Random Forest Classifier**.

### Algorithm

```text
Random Forest Classification
```

The notebook creates the model with:

```python
RandomForestClassifier(
    n_estimators=100,
    criterion="gini",
    random_state=42
)
```

The model is trained on the prepared training dataset and saved as:

```text
random_forest_churn_model.pkl
```

The trained scaler is saved as:

```text
scaler.pkl
```

---

# 📊 Dataset

The project uses the `Churn_Modelling.csv` dataset.

The dataset contains **10,000 customer records** and **14 original columns**.

### Original columns

| Column | Description |
|---|---|
| RowNumber | Row identifier |
| CustomerId | Customer identifier |
| Surname | Customer surname |
| CreditScore | Customer credit score |
| Geography | Customer country |
| Gender | Customer gender |
| Age | Customer age |
| Tenure | Number of years with the bank |
| Balance | Customer account balance |
| NumOfProducts | Number of bank products used |
| HasCrCard | Whether the customer has a credit card |
| IsActiveMember | Whether the customer is an active member |
| EstimatedSalary | Estimated customer salary |
| Exited | Target variable |

The source notebook shows that the dataset contains 10,000 rows and 14 columns. It also checks for missing values. fileciteturn3file1L1037-L1063

---

# 🎯 Target Variable

The target variable is:

```text
Exited
```

### Meaning

```text
0 → Customer stays
1 → Customer exits
```

The notebook defines:

```python
y = data.Exited
```

while the input features are selected separately. fileciteturn5file0L9-L13

---

# 🔢 Model Features

The trained model uses **11 input features**:

```text
1. CreditScore
2. Age
3. Tenure
4. Balance
5. NumOfProducts
6. HasCrCard
7. IsActiveMember
8. EstimatedSalary
9. Germany
10. Spain
11. Male
```

These are the exact features selected in the training notebook. fileciteturn5file0L9-L13

---

# 🔄 Data Preprocessing

## 1. Categorical Encoding

The categorical columns `Geography` and `Gender` are converted into numerical dummy variables.

The notebook uses:

```python
Geography = pd.get_dummies(
    data.Geography,
    drop_first=True
)
```

and:

```python
Gender = pd.get_dummies(
    data.Gender,
    drop_first=True
)
```

This creates:

```text
Geography → Germany, Spain
Gender    → Male
```

The original categorical columns are then removed. fileciteturn3file1L1073-L1083 fileciteturn5file2L79-L89

---

## 2. Feature Selection

The final feature matrix contains:

```python
[
    "CreditScore",
    "Age",
    "Tenure",
    "Balance",
    "NumOfProducts",
    "HasCrCard",
    "IsActiveMember",
    "EstimatedSalary",
    "Germany",
    "Spain",
    "Male"
]
```

The target is:

```python
Exited
```

---

## 3. Train/Test Split

The notebook uses an **80/20 train-test split**:

```python
X_train, X_test, y_train, y_test = train_test_split(
    X,
    y,
    random_state=42,
    test_size=0.2
)
```

So approximately:

```text
80% → Training
20% → Testing
```

fileciteturn4file1L60-L63

---

## 4. Feature Scaling

The project uses `StandardScaler`.

Training data:

```python
X_train = sc.fit_transform(X_train)
```

Testing data:

```python
X_test = sc.transform(X_test)
```

The scaler used by the application is saved as:

```text
scaler.pkl
```

fileciteturn4file2L76-L80

---

# 🌲 Random Forest Model

The model is created using:

```python
from sklearn.ensemble import RandomForestClassifier

rf_model = RandomForestClassifier(
    n_estimators=100,
    criterion="gini",
    random_state=42
)
```

The model is then trained using:

```python
rf_model.fit(X_train, y_train)
```

fileciteturn4file0L20-L23 fileciteturn5file3L94-L104

---

# 📈 Model Evaluation

The notebook evaluates the trained model using:

- Accuracy
- Confusion Matrix
- Classification Report

The recorded accuracy in the notebook is:

```text
Accuracy: 0.8665
```

That corresponds to approximately:

```text
86.65%
```

fileciteturn4file3L99-L107

The notebook also generates a confusion matrix and classification report. fileciteturn5file4L147-L167

> **Note:** The accuracy above is the value recorded in the supplied notebook. The README does not claim a newly calculated accuracy.

---

# 🖥️ Web Application

The application is built using:

```text
Streamlit
```

The current UI file is:

```text
app_same_ui_fixed.py
```

The application loads:

```python
random_forest_churn_model.pkl
scaler.pkl
```

and uses them for prediction. fileciteturn3file0L10-L27

---

# 🎨 Application UI

The application contains a colorful dashboard-style interface.

### Header

The interface contains:

- Customer Churn Prediction System
- Machine Learning
- Risk Analysis
- Customer Insights
- Random Forest Algorithm information

### Customer Information

The user can enter:

- Credit Score
- Age
- Tenure
- Account Balance
- Number of Products
- Has Credit Card
- Active Member
- Estimated Salary
- Country
- Gender

### Prediction Result

After clicking **Predict Churn**, the application displays:

- Customer Will Stay / Customer Will Exit
- Churn Probability
- Stay Probability
- Model Confidence
- Customer Snapshot

The UI code performs the same 11-feature transformation used by the trained model before calling the scaler and model. fileciteturn3file0L394-L398 fileciteturn3file0L446-L471

---

# 🗂️ Project Structure

Recommended final project structure:

```text
Customer-Churn-Prediction/
│
├── app.py
│
├── random_forest_churn_model.pkl
├── scaler.pkl
│
├── Churn_Modelling.csv
├── Python_Implementation_for_churn_prediction.ipynb
│
├── README.md
└── requirements.txt
```

### File Description

| File | Purpose |
|---|---|
| `app.py` | Main Streamlit web application |
| `random_forest_churn_model.pkl` | Trained Random Forest model |
| `scaler.pkl` | Saved feature scaler |
| `Churn_Modelling.csv` | Customer churn dataset |
| `Python_Implementation_for_churn_prediction.ipynb` | Model development, preprocessing, training and evaluation notebook |
| `README.md` | Project documentation |
| `requirements.txt` | Python dependencies |

The supplied project currently includes the dataset, notebook, model, scaler and multiple generated UI versions; use the final fixed UI version as the main `app.py`. fileciteturn2file1L7-L11 fileciteturn2file2L13-L17 fileciteturn2file3L19-L23 fileciteturn2file4L25-L29

---

# ⚙️ Technologies Used

## Programming Language

```text
Python
```

## Machine Learning

```text
Scikit-learn
Random Forest Classifier
StandardScaler
```

## Data Processing

```text
Pandas
NumPy
```

## Web Application

```text
Streamlit
```

## Model Serialization

```text
Pickle
```

---

# 📦 Installation

## Step 1: Install Python

Install Python 3.x on your system.

Check installation:

```bash
python --version
```

or:

```bash
python3 --version
```

---

## Step 2: Create Virtual Environment

### Windows

```bash
python -m venv venv
```

Activate:

```bash
venv\Scripts\activate
```

### Linux/macOS

```bash
python3 -m venv venv
```

Activate:

```bash
source venv/bin/activate
```

---

# 📥 Step 3: Install Dependencies

Create a file named:

```text
requirements.txt
```

Recommended contents:

```text
streamlit
numpy
pandas
scikit-learn
```

Install:

```bash
pip install -r requirements.txt
```

---

# ▶️ Step 4: Run the Application

Make sure these files are in the same folder:

```text
app.py
random_forest_churn_model.pkl
scaler.pkl
```

Then run:

```bash
streamlit run app.py
```

Streamlit will provide a local address, commonly:

```text
http://localhost:8501
```

Open that address in your browser.

---

# 🔮 How Prediction Works

The prediction pipeline is:

```text
User Input
    ↓
Convert categorical values
    ↓
Create 11 model features
    ↓
Load saved scaler
    ↓
Scale input
    ↓
Load Random Forest model
    ↓
Predict 0 / 1
    ↓
Predict probability
    ↓
Display result
```

The application scales the input using the saved scaler and then calls the saved model. It also uses `predict_proba()` to display probability values. fileciteturn3file0L464-L471

---

# 🧪 Example Input

Example customer:

```text
Credit Score       = 650
Age                = 35
Tenure             = 5
Balance            = 50000
Number of Products = 2
Has Credit Card    = Yes
Active Member      = Yes
Estimated Salary   = 75000
Country            = France
Gender             = Male
```

Click:

```text
🚀 Predict Churn
```

The system returns a prediction such as:

```text
Customer Will Stay
```

or:

```text
Customer Will Exit
```

along with probability and confidence information.

---

# 🛠️ Troubleshooting

## 1. `ModuleNotFoundError: No module named 'streamlit'`

Run:

```bash
pip install streamlit
```

---

## 2. `ModuleNotFoundError: No module named 'sklearn'`

Run:

```bash
pip install scikit-learn
```

---

## 3. Model file not found

If you see an error related to:

```text
random_forest_churn_model.pkl
```

make sure the file is in the same directory as `app.py`.

---

## 4. Scaler file not found

Make sure:

```text
scaler.pkl
```

is present in the same directory.

---

## 5. Streamlit command not found

Try:

```bash
python -m streamlit run app.py
```

---

# 🔐 Important Model Compatibility Note

The application expects the saved model and scaler to match the feature order used during training.

The required order is:

```text
CreditScore
Age
Tenure
Balance
NumOfProducts
HasCrCard
IsActiveMember
EstimatedSalary
Germany
Spain
Male
```

Do not randomly change the feature order without retraining/updating the model pipeline.

---

# 📁 Dataset Information

The supplied CSV begins with the following structure:

```text
RowNumber
CustomerId
Surname
CreditScore
Geography
Gender
Age
Tenure
Balance
NumOfProducts
HasCrCard
IsActiveMember
EstimatedSalary
Exited
```

The dataset contains 10,000 customer records. fileciteturn3file1L1037-L1057

---

# 🎓 Project Learning Outcomes

By completing this project, you demonstrate knowledge of:

- Data loading
- Exploratory data understanding
- Missing-value checking
- Categorical encoding
- Feature selection
- Train/test splitting
- Feature scaling
- Random Forest classification
- Model training
- Model prediction
- Accuracy evaluation
- Confusion matrix
- Classification report
- Model serialization
- Streamlit application development
- Real-time ML prediction

---

# 💼 Real-World Use Case

A bank can use a churn prediction system to identify customers who may be at higher risk of leaving.

For example:

```text
Customer Risk Detected
        ↓
Retention Team Alert
        ↓
Customer Analysis
        ↓
Personalized Offer / Support
        ↓
Improved Customer Retention
```

The supplied project problem statement specifically focuses on proactive engagement and personalized retention efforts. fileciteturn3file1L797-L808

---

# 🚀 Future Improvements

Possible future improvements include:

### 1. Login System

Add:

```text
Admin Login
User Login
```

### 2. Prediction History

Store previous predictions in:

```text
SQLite / MySQL / PostgreSQL
```

### 3. Customer Dashboard

Add:

```text
Total Customers
High-Risk Customers
Low-Risk Customers
Churn Rate
```

### 4. Data Visualization

Add charts for:

```text
Churn by Age
Churn by Geography
Churn by Gender
Churn by Balance
Churn by Product Count
```

### 5. Batch Prediction

Allow users to upload a CSV and generate predictions for multiple customers.

### 6. Explainable AI

Add feature-importance or explainability methods such as:

```text
Feature Importance
SHAP
```

### 7. Deployment

Possible deployment targets:

```text
Streamlit Community Cloud
Render
Railway
AWS
Azure
```

---

# 📋 Project Workflow

```text
                 ┌─────────────────────┐
                 │  Churn_Modelling.csv│
                 └──────────┬──────────┘
                            │
                            ▼
                 ┌─────────────────────┐
                 │ Data Preprocessing  │
                 └──────────┬──────────┘
                            │
                 ┌──────────▼──────────┐
                 │ Categorical Encoding│
                 └──────────┬──────────┘
                            │
                 ┌──────────▼──────────┐
                 │ Feature Selection   │
                 └──────────┬──────────┘
                            │
                 ┌──────────▼──────────┐
                 │ Standard Scaling    │
                 └──────────┬──────────┘
                            │
                 ┌──────────▼──────────┐
                 │ Random Forest       │
                 │ Classifier          │
                 └──────────┬──────────┘
                            │
                 ┌──────────▼──────────┐
                 │ Model Evaluation    │
                 └──────────┬──────────┘
                            │
                 ┌──────────▼──────────┐
                 │ Save Model + Scaler │
                 └──────────┬──────────┘
                            │
                            ▼
                 ┌─────────────────────┐
                 │ Streamlit Web App   │
                 └──────────┬──────────┘
                            │
                            ▼
                 ┌─────────────────────┐
                 │ Churn Prediction    │
                 └─────────────────────┘
```

---

# 👨‍💻 Running the Complete Project

From the project directory:

```bash
cd Customer-Churn-Prediction
```

Create environment:

```bash
python -m venv venv
```

Activate it:

### Windows

```bash
venv\Scripts\activate
```

Install packages:

```bash
pip install -r requirements.txt
```

Run:

```bash
streamlit run app.py
```

---

# 📌 Quick Start

If Python and dependencies are already installed:

```bash
streamlit run app.py
```

That's it.

---

# 📄 Project Summary

**Project Name:** Customer Churn Prediction System

**Domain:** Machine Learning / Predictive Analytics

**Problem Type:** Binary Classification

**Algorithm:** Random Forest Classifier

**Dataset:** Churn Modelling Dataset

**Target:** `Exited`

**Number of Model Features:** 11

**Train/Test Split:** 80/20

**Scaling:** StandardScaler

**Recorded Notebook Accuracy:** 86.65%

**Frontend:** Streamlit

**Model File:** `random_forest_churn_model.pkl`

**Scaler File:** `scaler.pkl`

---

# ⭐ Conclusion

The Customer Churn Prediction System demonstrates an end-to-end Machine Learning workflow:

```text
Dataset
   ↓
Preprocessing
   ↓
Feature Engineering
   ↓
Scaling
   ↓
Random Forest
   ↓
Evaluation
   ↓
Model Serialization
   ↓
Streamlit Interface
   ↓
Real-Time Churn Prediction
```

The project combines Machine Learning with an interactive web application to demonstrate how predictive analytics can be used for customer-retention scenarios.

---

## 📜 License

This project is intended for educational and project demonstration purposes.

---

## 🙌 Acknowledgement

Built as a Machine Learning project demonstrating customer churn prediction using Python, Scikit-learn, Random Forest and Streamlit.
