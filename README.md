# 📊 Customer Churn Analysis

## 📌 Project Overview

**Customer Churn Analysis** is a Python-based Exploratory Data Analysis (EDA) project focused on understanding customer behavior and identifying factors associated with customer churn.

The project analyzes customer information such as **Age, Credit Score, Geography, Gender, Balance, Estimated Salary, Tenure, Number of Products, Credit Card ownership, and Active Membership status**.

The analysis compares customers who **stayed (`Exited = 0`)** with customers who **left/churned (`Exited = 1`)** and uses statistical analysis, cross-tabulation, grouping, and data visualization to identify meaningful patterns.

The project contains **30 analytical questions**, covering data cleaning, churn analysis, financial metrics, engagement, tenure, cross-tabulation, correlation, and visualization.

---

# 🎯 Project Objectives

The main objectives of this project are:

* Understand the structure and quality of the dataset.
* Perform data cleaning and preprocessing.
* Calculate the overall customer churn rate.
* Analyze churn across gender and geography.
* Study the relationship between age and churn.
* Analyze the effect of active membership on churn.
* Compare financial characteristics of churned and retained customers.
* Study the relationship between salary and churn.
* Analyze credit score and churn behavior.
* Calculate the total balance associated with churned customers.
* Analyze tenure and customer engagement.
* Study the impact of number of products on churn.
* Analyze the relationship between credit card ownership and churn.
* Perform cross-tabulation between multiple categorical variables.
* Identify high-balance customers and their churn status.
* Analyze correlations between numerical features.
* Create meaningful visualizations for business insights.

---

# 📂 Dataset

The project uses a customer banking dataset containing demographic, financial, and account-related information.

## Important Features

| Column            | Description                              |
| ----------------- | ---------------------------------------- |
| `CustomerId`      | Unique customer identifier               |
| `Surname`         | Customer surname                         |
| `CreditScore`     | Customer's credit score                  |
| `Geography`       | Customer's country/geographical region   |
| `Gender`          | Customer gender                          |
| `Age`             | Customer age                             |
| `Tenure`          | Number of years associated with the bank |
| `Balance`         | Customer's account balance               |
| `NumOfProducts`   | Number of products held by the customer  |
| `HasCrCard`       | Whether the customer has a credit card   |
| `IsActiveMember`  | Whether the customer is an active member |
| `EstimatedSalary` | Estimated customer salary                |
| `Exited`          | Customer churn/exit status               |

### Target Variable

The `Exited` column represents customer churn:

```text
0 → Customer Stayed
1 → Customer Exited / Churned
```

---

# 🛠️ Technologies Used

* **Python**
* **Pandas**
* **NumPy**
* **Matplotlib**
* **SciPy**
* **Jupyter Notebook**
* **CSV / Excel**

---

# 📁 Project Structure

```text
Customer-Churn-Analysis/
│
├── data/
│   └── churn_dataset.csv
│
├── notebooks/
│   └── Customer_Churn_Analysis.ipynb
│
├── visualizations/
│   ├── geography_gender.png
│   ├── overall_churn.png
│   ├── churn_by_gender.png
│   ├── churn_by_geography.png
│   ├── age_distribution.png
│   ├── activity_churn.png
│   ├── balance_comparison.png
│   ├── salary_churn.png
│   ├── credit_score_churn.png
│   ├── tenure_churn.png
│   ├── products_churn.png
│   ├── credit_card_churn.png
│   ├── correlation_heatmap.png
│   ├── age_balance_scatter.png
│   ├── geography_salary.png
│   ├── credit_score_distribution.png
│   └── age_tenure_boxplot.png
│
├── README.md
├── requirements.txt
└── .gitignore
```

---

# 🔍 Project Analysis

The project is divided into six major analytical sections.

---

# 1️⃣ Basic Data Exploration & Cleaning

### 1. Dataset Structure

Analyze the total number of rows and columns and identify the data types of each feature.

Key operations:

```python
df.shape
df.dtypes
df.info()
```

---

### 2. Missing Value Analysis

Check whether the dataset contains null or missing values and calculate the number of missing values in each column.

```python
df.isnull().sum()
```

---

### 3. Duplicate Records

Identify duplicate records and remove them from the dataset.

```python
df.duplicated().sum()

df = df.drop_duplicates()
```

---

### 4. Numerical Summary Statistics

Calculate summary statistics such as:

* Mean
* Median
* Minimum
* Maximum
* Standard Deviation

for numerical columns including:

* Age
* CreditScore
* Balance
* EstimatedSalary
* Tenure
* NumOfProducts

Example:

```python
df.select_dtypes(include='number').agg(
    ['mean', 'median', 'min', 'max', 'std']
)
```

---

### 5. Categorical Feature Analysis

Analyze the unique categories and their frequencies in:

* `Geography`
* `Gender`

```python
df['Geography'].value_counts()
df['Gender'].value_counts()
```

---

# 2️⃣ Customer Attrition & Churn Analysis

## 6. Overall Churn Rate

Calculate the percentage of customers who exited the bank.

```python
churn_rate = df['Exited'].mean() * 100

print(f"Overall Churn Rate: {churn_rate:.2f}%")
```

---

## 7. Gender-wise Churn Rate

Compare the churn rates of male and female customers.

```python
churn_by_gender = df.groupby('Gender')['Exited'].mean() * 100

print(churn_by_gender.round(2))
```

---

## 8. Geography-wise Churn Analysis

Calculate both:

* Total churn count
* Churn percentage

for each geographical region.

```python
geo_analysis = df.groupby('Geography')['Exited'].agg(
    Total_Customers='count',
    Total_Exited='sum',
    Churn_Rate='mean'
)

geo_analysis['Churn_Rate'] *= 100

print(geo_analysis.round(2))
```

---

## 9. Age Group Churn Analysis

Analyze the age distribution of churned and non-churned customers and identify age groups with different churn rates.

Example age groups:

```text
18-25
26-35
36-45
46-55
56-65
66+
```

---

## 10. Active vs Inactive Members

Compare churn rates between:

```text
IsActiveMember = 1 → Active
IsActiveMember = 0 → Inactive
```

```python
activity_churn = df.groupby(
    'IsActiveMember'
)['Exited'].mean() * 100

print(activity_churn.round(2))
```

A Chi-Square test can also be applied to examine the association between activity status and churn.

---

# 3️⃣ Financial & Performance Metrics

## 11. Average Balance of Churned vs Retained Customers

Compare the average account balance between:

```text
Exited = 1 → Churned
Exited = 0 → Retained
```

```python
avg_balance = df.groupby('Exited')['Balance'].mean()

print(avg_balance.round(2))
```

---

## 12. Salary vs Churn Rate

Group `EstimatedSalary` into salary brackets and calculate the churn rate for each group.

Example:

```text
0-25K
25K-50K
50K-75K
75K-100K
100K-150K
150K-200K
```

This helps analyze whether churn rates vary across salary levels.

---

## 13. Credit Score Analysis

Compare churn rates between:

```text
High Credit Score → CreditScore > 700
Low Credit Score  → CreditScore < 600
```

Example:

```python
high_score = df[df['CreditScore'] > 700]
low_score = df[df['CreditScore'] < 600]

print("High Credit Score Churn Rate:",
      high_score['Exited'].mean() * 100)

print("Low Credit Score Churn Rate:",
      low_score['Exited'].mean() * 100)
```

---

## 14. Total Balance Lost Due to Churn

Calculate the total account balance associated with customers who exited.

```python
total_balance_lost = df.loc[
    df['Exited'] == 1,
    'Balance'
].sum()

print(f"Total Balance Lost Due to Churn: {total_balance_lost:,.2f}")
```

---

## 15. Average Credit Score

Compare the average credit score of:

* Churned customers
* Retained customers

```python
avg_credit_score = df.groupby('Exited')['CreditScore'].mean()

print(avg_credit_score.round(2))
```

---

# 4️⃣ Engagement & Tenure Insights

## 16. Tenure-wise Churn Analysis

Analyze the churn rate according to the number of years customers have been associated with the bank.

```python
tenure_churn = df.groupby('Tenure')['Exited'].mean() * 100

print(tenure_churn.round(2))
```

---

## 17. Number of Products vs Churn

Analyze whether the number of products held by a customer is associated with churn.

```python
product_churn = df.groupby(
    'NumOfProducts'
)['Exited'].mean() * 100

print(product_churn.round(2))
```

---

## 18. Credit Card Ownership vs Churn

Compare churn rates between customers who have and do not have a credit card.

```python
credit_card_churn = df.groupby(
    'HasCrCard'
)['Exited'].mean() * 100

print(credit_card_churn.round(2))
```

---

## 19. Customers with 3 or 4 Products

Identify customers who have 3 or 4 products and analyze their churn status.

```python
products_3_4 = df[
    df['NumOfProducts'].isin([3, 4])
]

print(products_3_4['Exited'].value_counts())
```

Their percentage can also be calculated:

```python
percentage = (
    products_3_4['Exited'].value_counts(normalize=True) * 100
)

print(percentage.round(2))
```

---

## 20. Highest Tenure Among Inactive Members

Identify customers who have the highest tenure while being inactive.

```python
inactive_customers = df[
    df['IsActiveMember'] == 0
]

max_tenure = inactive_customers['Tenure'].max()

result = inactive_customers[
    inactive_customers['Tenure'] == max_tenure
]

print(result)
```

---

# 5️⃣ Advanced Cross-Tabulation & Grouping

## 21. Geography + Gender Churn Analysis

Perform a combined analysis of `Geography` and `Gender`.

```python
geo_gender_churn = df.pivot_table(
    values='Exited',
    index='Geography',
    columns='Gender',
    aggfunc='mean'
) * 100

print(geo_gender_churn.round(2))
```

This allows churn rates to be compared across both geography and gender.

---

## 22. Top 10 Highest Balance Customers

Identify the top 10 customers with the highest account balance and check their churn status.

```python
top_balance = df.nlargest(
    10,
    'Balance'
)

print(
    top_balance[
        ['CustomerId', 'Surname', 'Balance', 'Exited']
    ]
)
```

---

## 23. Age Group Churn Analysis

Divide customers into the following age groups:

```text
<30
30-45
45-60
60+
```

Then calculate the churn rate for each group.

```python
bins = [0, 30, 45, 60, float('inf')]

labels = [
    '<30',
    '30-45',
    '45-60',
    '60+'
]

df['Age_Group_2'] = pd.cut(
    df['Age'],
    bins=bins,
    labels=labels,
    right=False
)

age_group_churn = df.groupby(
    'Age_Group_2',
    observed=True
)['Exited'].mean() * 100

print(age_group_churn.round(2))
```

---

## 24. Low Credit Score + Zero Balance

Identify customers who satisfy both conditions:

```text
CreditScore < 600
Balance = 0
```

Then calculate their total count and churn rate.

```python
low_score_zero_balance = df[
    (df['CreditScore'] < 600) &
    (df['Balance'] == 0)
]

count = len(low_score_zero_balance)

churn_rate = (
    low_score_zero_balance['Exited'].mean() * 100
)

print("Total Customers:", count)
print(f"Churn Rate: {churn_rate:.2f}%")
```

---

## 25. Salary-to-Balance Ratio

Create a new feature representing the ratio between estimated salary and account balance.

```python
df['Salary_Balance_Ratio'] = (
    df['EstimatedSalary'] /
    df['Balance'].replace(0, float('nan'))
)
```

The correlation with churn can then be examined:

```python
correlation = df[
    ['Salary_Balance_Ratio', 'Exited']
].corr()

print(correlation)
```

---

# 6️⃣ Correlation & Data Visualization

## 26. Correlation Heatmap

Calculate correlations among numerical features and visualize them using a heatmap.

```python
import matplotlib.pyplot as plt

correlation_matrix = df.select_dtypes(
    include='number'
).corr()

plt.figure(figsize=(12, 8))

plt.imshow(
    correlation_matrix,
    cmap='coolwarm',
    aspect='auto'
)

plt.colorbar()

plt.xticks(
    range(len(correlation_matrix.columns)),
    correlation_matrix.columns,
    rotation=90
)

plt.yticks(
    range(len(correlation_matrix.columns)),
    correlation_matrix.columns
)

plt.title('Correlation Heatmap')

plt.tight_layout()
plt.show()
```

The correlation with `Exited` can be examined to identify numerical features with stronger linear association with churn.

---

## 27. Age vs Balance Scatter Plot

Create a scatter plot between `Age` and `Balance` and distinguish churned and retained customers using color.

```python
plt.figure(figsize=(9, 6))

for status, group in df.groupby('Exited'):
    label = 'Churned' if status == 1 else 'Retained'

    plt.scatter(
        group['Age'],
        group['Balance'],
        label=label,
        alpha=0.6
    )

plt.title('Age vs Account Balance')
plt.xlabel('Age')
plt.ylabel('Balance')
plt.legend()

plt.tight_layout()
plt.show()
```

---

## 28. Geography-wise Total Estimated Salary

Calculate the total estimated salary for each geographical region and visualize it using a bar chart.

```python
geo_salary = df.groupby(
    'Geography'
)['EstimatedSalary'].sum()

plt.figure(figsize=(8, 5))

bars = plt.bar(
    geo_salary.index,
    geo_salary.values
)

plt.title('Total Estimated Salary by Geography')
plt.xlabel('Geography')
plt.ylabel('Total Estimated Salary')

for bar, value in zip(bars, geo_salary.values):
    plt.text(
        bar.get_x() + bar.get_width() / 2,
        bar.get_height(),
        f'{value:,.0f}',
        ha='center',
        va='bottom'
    )

plt.tight_layout()
plt.show()
```

---

## 29. Credit Score Distribution

Analyze the distribution of `CreditScore` for both churned and retained customers using histograms.

```python
plt.figure(figsize=(9, 6))

plt.hist(
    df[df['Exited'] == 0]['CreditScore'],
    bins=20,
    alpha=0.6,
    label='Retained'
)

plt.hist(
    df[df['Exited'] == 1]['CreditScore'],
    bins=20,
    alpha=0.6,
    label='Churned'
)

plt.title('Credit Score Distribution: Churned vs Retained')
plt.xlabel('Credit Score')
plt.ylabel('Number of Customers')
plt.legend()

plt.tight_layout()
plt.show()
```

---

## 30. Age vs Tenure Box Plot Analysis

Analyze the distribution of `Tenure` across different `Age Groups` using a **Box Plot**. The visualization helps identify differences in tenure distribution, variability, and potential outliers across age groups.

Example age groups:

```text
<30
30-45
45-60
60+
```

Example implementation:

```python
plt.figure(figsize=(9, 6))

df.boxplot(
    column='Tenure',
    by='Age_Group_2'
)

plt.title('Tenure Distribution Across Age Groups')
plt.suptitle('')
plt.xlabel('Age Group')
plt.ylabel('Tenure (Years)')

plt.tight_layout()
plt.show()
```

This visualization can help identify unusual tenure values and understand how tenure is distributed across different customer age groups.

---

# 📊 Analysis Categories

The 30 questions in this project cover the following areas:

| Category                          | Questions | Focus                                       |
| --------------------------------- | --------: | ------------------------------------------- |
| Basic Data Exploration & Cleaning |       1–5 | Dataset structure and quality               |
| Customer Churn Analysis           |      6–10 | Churn patterns                              |
| Financial & Performance Metrics   |     11–15 | Balance, salary and credit score            |
| Engagement & Tenure               |     16–20 | Customer engagement                         |
| Advanced Grouping                 |     21–25 | Cross-tabulation and derived features       |
| Correlation & Visualization       |     26–30 | Statistical relationships and visualization |

---

# 📈 Key Insights

The project investigates several important customer churn dimensions:

### Customer Demographics

* Geography
* Gender
* Age

### Financial Characteristics

* Account Balance
* Estimated Salary
* Credit Score

### Engagement

* Active Membership
* Number of Products
* Credit Card Ownership
* Tenure

### Churn

* Overall churn rate
* Gender-wise churn
* Geography-wise churn
* Age-wise churn
* Salary-wise churn
* Tenure-wise churn
* Product-wise churn

The actual numerical findings are generated directly from the dataset and presented in the Jupyter Notebook.

---

# 💡 Business Insights

The analysis can help organizations understand:

* Which customer segments have different churn rates.
* How demographic characteristics relate to churn.
* Whether customer engagement is associated with retention.
* How financial characteristics vary between churned and retained customers.
* Which customer groups may require further investigation for retention strategies.
* Which numerical variables show stronger associations with the churn indicator.

> **Note:** Correlation or group-level differences do not by themselves establish causation. Further statistical testing and predictive modeling would be required to investigate causal relationships or build a churn prediction system.

---

# 🚀 Future Improvements

This project can be extended into a complete customer churn prediction system by adding:

### Machine Learning

* Logistic Regression
* Decision Tree
* Random Forest
* XGBoost
* Gradient Boosting

### Model Evaluation

* Accuracy
* Precision
* Recall
* F1-Score
* ROC-AUC
* Confusion Matrix

### Advanced Analytics

* Feature Importance
* Customer Segmentation
* Clustering
* Churn Probability
* Customer Risk Scoring

### Dashboard

The analysis can also be converted into an interactive dashboard using:

* Power BI
* Tableau
* Streamlit
* Plotly

---

# ⚙️ Installation

Clone the repository:

```bash
git clone https://github.com/Abdul720R/Customer-churn-Analysis.git
```

Navigate to the project:

```bash
cd Customer-churn-Analysis
```

Install the required libraries:

```bash
pip install -r requirements.txt
```

---

# ▶️ How to Run

1. Clone the repository.
2. Install the required Python libraries.
3. Place the dataset inside the `data/` folder.
4. Open the Jupyter Notebook from the `notebooks/` folder.
5. Run the notebook cells sequentially.
6. Review the generated tables, statistical results, and visualizations.

---

# 📦 Requirements

The main dependencies are:

```text
pandas
numpy
matplotlib
scipy
jupyter
openpyxl
```

Install all dependencies using:

```bash
pip install -r requirements.txt
```

---

# 📌 Project Status

**Status:** Completed — Exploratory Data Analysis

The project currently focuses on data cleaning, exploratory analysis, statistical analysis, grouping, and visualization.

Machine learning-based churn prediction can be added as a future enhancement.

---

# 👨‍💻 Author

## Abdul Rahman

**BCA (Hons) | Data Analyst | Python Developer**

### Skills

* Python
* SQL
* Pandas
* NumPy
* Matplotlib
* Power BI
* Data Analysis
* Data Visualization
* Machine Learning

---

# ⭐ Conclusion

The **Customer Churn Analysis** project demonstrates how raw customer data can be transformed into meaningful insights using Python and exploratory data analysis techniques.

By analyzing customer demographics, financial attributes, engagement levels, tenure, and churn behavior, the project provides a structured understanding of patterns associated with customer retention and attrition.

The project also demonstrates practical skills in **data cleaning, statistical analysis, feature engineering, grouping, cross-tabulation, correlation analysis, and data visualization**.

---

## 📜 License

This project is created for educational and portfolio purposes.
