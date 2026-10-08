# 🏦 Banking Customer Analytics

An end-to-end **Banking Customer Analytics project** that analyzes customer demographics, financial behavior, banking relationships, lending activity, loyalty, and risk using **Python, NumPy, Pandas, MySQL, and Power BI**.

The project follows a practical data analyst workflow:

**Raw Data → Database → Exploratory Data Analysis → Business Analysis → Dashboard Design → Power BI Dashboard**

---

## 📌 Project Overview

Banks generate large amounts of customer data across deposits, loans, accounts, credit cards, income, investments, and customer demographics.

The objective of this project is to analyze a banking customer dataset and transform raw customer-level data into meaningful business insights that can help understand:

- Customer demographics and segmentation
- Income distribution
- Customer loyalty
- Banking product usage
- Loan and deposit behavior
- Credit card usage
- Business lending
- Customer risk levels
- Banking relationship categories
- Differences across customer segments

The analysis was performed using Python for exploratory analysis, MySQL for structured data storage and querying, and Power BI for interactive business reporting.

---

## 🎯 Business Objectives

The project focuses on answering questions such as:

- What does the overall customer base look like?
- How are customers distributed across different banking segments?
- What are the major income groups?
- How are customers distributed by nationality and gender?
- Which loyalty classifications have the most customers?
- How are customers distributed across fee structures?
- How are bank loans and deposits distributed?
- What is the relationship between income and financial products?
- How are customers distributed across different risk weightings?
- Which banking segments have stronger financial activity?
- How do customer financial characteristics vary across different categories?

---

## 📊 Dataset

The dataset contains **3,000 banking customers** with **25 original attributes**.

The data includes customer demographics, banking relationships, financial information, lending information, and risk-related attributes.

### Key Columns

| Category | Columns |
|---|---|
| Customer Information | Client ID, Name, Age, Location ID |
| Banking Relationship | Joined Bank, Banking Contact |
| Demographics | Nationality, Gender |
| Customer Profile | Occupation, Fee Structure, Loyalty Classification |
| Income & Savings | Estimated Income, Superannuation Savings |
| Credit | Amount of Credit Cards, Credit Card Balance |
| Lending | Bank Loans, Business Lending |
| Deposits & Accounts | Bank Deposits, Checking Accounts, Saving Accounts, Foreign Currency Account |
| Assets | Properties Owned |
| Risk | Risk Weighting |
| Banking Segment | BRId |
| Relationship Manager | IAId |

The MySQL database contains the `customer` table with these banking attributes.

---

# 🔄 Project Workflow

```text
                 ┌─────────────────┐
                 │   Banking.csv   │
                 └────────┬────────┘
                          │
                          ▼
                 ┌─────────────────┐
                 │      MySQL      │
                 │ Database/Table  │
                 └────────┬────────┘
                          │
                          ▼
                 ┌─────────────────┐
                 │ Python EDA      │
                 │ NumPy/Pandas    │
                 └────────┬────────┘
                          │
                          ▼
                 ┌─────────────────┐
                 │ Business        │
                 │ Analysis        │
                 └────────┬────────┘
                          │
                          ▼
                 ┌─────────────────┐
                 │ Dashboard       │
                 │ Planning        │
                 │ (Canva)         │
                 └────────┬────────┘
                          │
                          ▼
                 ┌─────────────────┐
                 │    Power BI     │
                 │ Interactive     │
                 │ Dashboard       │
                 └─────────────────┘
```

---

# 🛠️ Tools & Technologies

### Python
- NumPy
- Pandas
- Matplotlib
- Seaborn
- Jupyter Notebook

### Database
- MySQL
- MySQL Connector/Python
- SQL

### Visualization & Reporting
- Power BI
- Canva

---

# 1️⃣ Data Storage & SQL

The raw banking dataset was loaded into **MySQL** to create a structured database environment.

The database used in the project is:

```text
banking_case
```

with the primary table:

```text
customer
```

The SQL database contains the customer-level banking information and was used as the structured source for analysis.

The SQL dump was generated from **MySQL 8.0.46** and contains the `customer` table definition and customer records.

### Python → MySQL Connection

Python was connected to MySQL using `mysql-connector-python`, allowing the customer table to be retrieved directly into a Pandas DataFrame.

```python
import mysql.connector
import pandas as pd

cnx = mysql.connector.connect(
    host="localhost",
    port=3306,
    user="root",
    password="your_password"
)

query = "SELECT * FROM banking_case.customer"

df = pd.read_sql(query, cnx)

cnx.close()
```

This created a workflow where the data could be stored and managed in MySQL and then analyzed using Python.

---

# 2️⃣ Exploratory Data Analysis

After retrieving the data, exploratory analysis was performed to understand the structure and quality of the dataset.

### Dataset Inspection

The following operations were performed:

```python
df.head()
df.shape
df.info()
df.describe()
df.describe(include="all")
df.isnull().sum()
```

The analysis confirmed a dataset of **3,000 customer records**.

The notebook also examined numerical distributions and categorical variables before creating visualizations.

---

## 📈 Numerical Analysis

The following financial variables were analyzed:

- Estimated Income
- Superannuation Savings
- Credit Card Balance
- Bank Loans
- Bank Deposits
- Checking Accounts
- Saving Accounts
- Foreign Currency Account
- Business Lending

Distribution plots were created using Seaborn to understand the spread and behavior of these financial variables.

---

## 📊 Income Segmentation

Customers were additionally grouped into income bands based on estimated income:

| Income Band | Income Range |
|---|---:|
| Low | < 100,000 |
| Medium | 100,000 – 299,999 |
| High | ≥ 300,000 |

This segmentation was created using:

```python
bins = [0, 100000, 300000, float("inf")]
labels = ["Low", "Medium", "High"]

df["Income Band"] = pd.cut(
    df["Estimated Income"],
    bins=bins,
    labels=labels,
    right=False
)
```

The resulting income groups were then visualized to understand the customer distribution.

---

# 3️⃣ Categorical Analysis

Categorical variables were analyzed to understand the composition of the customer base.

The analysis included:

- Banking Segment (`BRId`)
- Gender
- Investment/Advisor relationship (`IAId`)
- Number of Credit Cards
- Nationality
- Occupation
- Fee Structure
- Loyalty Classification
- Properties Owned
- Risk Weighting
- Income Band

Value counts and categorical visualizations were used to identify dominant customer segments and patterns.

For example:

```python
df["Nationality"].value_counts()
df["Loyalty Classification"].value_counts()
df["Fee Structure"].value_counts()
df["Risk Weighting"].value_counts()
```

---

# 4️⃣ Correlation Analysis

Correlation analysis was performed on the major numerical banking variables.

```python
numerical_cols = [
    "Estimated Income",
    "Superannuation Savings",
    "Credit Card Balance",
    "Bank Loans",
    "Bank Deposits",
    "Checking Accounts",
    "Saving Accounts",
    "Foreign Currency Account",
    "Business Lending"
]

correlation_matrix = df[numerical_cols].corr()
```

A correlation heatmap was then created to identify relationships between different financial variables.

This helps understand whether financial variables tend to move together and provides an initial basis for deeper business analysis.

---

# 5️⃣ Dashboard Planning

Before building the final dashboard, a rough dashboard structure was designed in **Canva**.

The purpose of this stage was to decide:

- Which KPIs should be highlighted
- Which charts should be used
- How information should be arranged
- Which business questions each visual should answer
- How the dashboard should be structured for easy interpretation

This helped convert the exploratory analysis into a more focused business dashboard.

---

# 6️⃣ Power BI Dashboard

The final interactive dashboard was created using **Microsoft Power BI**.

The dashboard brings together customer demographics, financial activity, customer segmentation, and risk-related information into an interactive reporting interface.

### Dashboard Areas

The dashboard focuses on areas such as:

### 👥 Customer Overview
- Total customers
- Customer demographics
- Gender distribution
- Nationality distribution
- Customer age distribution

### 💰 Financial Overview
- Estimated income
- Bank deposits
- Bank loans
- Business lending
- Checking accounts
- Saving accounts

### 💳 Credit Profile
- Credit card count
- Credit card balance
- Financial exposure

### ⭐ Customer Segmentation
- Loyalty classification
- Fee structure
- Banking segment
- Income bands

### ⚠️ Risk Analysis
- Risk weighting
- Financial characteristics across risk categories

### 🔎 Interactive Analysis
Power BI enables users to filter and explore the data based on different customer characteristics and financial dimensions.

---

# 📌 Key Analytical Areas

The project combines several important dimensions of banking analytics:

```text
Customer Demographics
        ↓
Income & Financial Profile
        ↓
Banking Products
        ↓
Loans & Deposits
        ↓
Customer Segmentation
        ↓
Risk Profile
        ↓
Business Insights
```

This provides a more complete view of the banking customer rather than analyzing individual financial metrics in isolation.

---

# 📁 Project Structure

```text
Banking-Customer-Analytics/
│
├── Banking.csv
│
├── banking_case.sql
│
├── Banking_Domain_Analysis.ipynb
│
├── PowerBI/
│   └── Banking_Dashboard.pbix
│
├── Dashboard_Design/
│   └── Canva_Dashboard_Design.png
│
└── README.md
```

> File names can be adjusted depending on the final repository structure.

---

# 🔍 Analysis Techniques Used

### Data Understanding
- Dataset inspection
- Shape and structure analysis
- Data type inspection
- Missing-value analysis
- Descriptive statistics

### Exploratory Analysis
- Univariate analysis
- Categorical analysis
- Numerical distributions
- Income segmentation
- Correlation analysis

### Visualization
- Bar charts
- Count plots
- Histograms
- KDE plots
- Correlation heatmap

### Business Intelligence
- KPI development
- Customer segmentation
- Financial analysis
- Risk analysis
- Interactive dashboard development

---

# 💡 Business Value

This project demonstrates how raw banking data can be transformed into a structured analytics workflow:

**Data → Database → Analysis → Visualization → Business Intelligence**

The resulting analysis can help banking stakeholders better understand:

- Customer composition
- Financial behavior
- Deposit and lending activity
- Credit exposure
- Customer loyalty
- Customer segmentation
- Risk distribution

The dashboard provides a consolidated view that can support exploratory decision-making and customer-focused analysis.

---

# 🚀 Skills Demonstrated

This project demonstrates practical experience with:

- Python for data analysis
- NumPy & Pandas
- Exploratory Data Analysis
- Data visualization
- SQL
- MySQL database management
- Python–MySQL integration
- Customer segmentation
- Financial data analysis
- Correlation analysis
- Dashboard planning
- Power BI
- Business-oriented data storytelling

---

# 📚 Project Learning Outcomes

Through this project, I practiced the complete workflow of a data analyst:

1. Understanding a raw dataset
2. Loading and storing data in a relational database
3. Connecting Python with MySQL
4. Performing exploratory data analysis
5. Identifying patterns and distributions
6. Segmenting customers
7. Analyzing financial relationships
8. Designing a dashboard layout
9. Translating analysis into business-focused visuals
10. Building an interactive Power BI dashboard

---

# 🏁 Conclusion

The **Banking Customer Analytics** project demonstrates an end-to-end approach to data analytics, combining **Python, SQL/MySQL, Canva, and Power BI**.

Rather than focusing only on individual charts, the project follows a complete analytical pipeline—from structured data storage and exploratory analysis to dashboard design and business intelligence.

It showcases how customer and financial data can be transformed into an interactive reporting solution that makes complex banking information easier to explore and understand.

---

## 👨‍💻 Author

**Sujeet Kumar**

B.Tech — Electronics & Communication Engineering

Interested in **Data Analytics, Business Intelligence, SQL, Python, and Data Visualization**.
