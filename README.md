
# 🏦 CrediTrust: Loan Risk and Customer Default Analysis

# Table of Contents

- [Project Overview](#project-overview)
- [Dataset Overview](#dataset-overview)
- [Business Problem](#business-problem)
- [Project Objectives](#project-objectives)
- [Tools Used](#tools-used)
- [Data Preparation](#data-preparation)
- [Feature Engineering](#feature-engineering)
- [Executive Summary](#executive-summary)
- [Key Business Insights](#key-business-insights)
- [Business Recommendations](#business-recommendations)
- [Skills Demonstrated](#skills-demonstrated)
- [Conclusion](#conclusion)
- [Connect With Me](#connect-with-me)
---
## Project Overview

Loan defaults are a major challenge for financial institutions because they increase financial risk and reduce profitability.

This project analyses customer loan data from CrediTrust to identify patterns in borrower behaviour, uncover the key drivers of loan default, and support better lending decisions.

Using Python, the analysis transforms raw data into meaningful insights through data preparation, exploratory data analysis, customer risk segmentation, and business recommendations.

---
## Business Problem

CrediTrust is experiencing an increase in loan defaults and needs a better way to identify high-risk borrowers.

Without clear insights into the factors associated with default, lending decisions become more difficult and the risk of financial loss increases.

This project analyzes customer and loan data to identify default patterns, classify borrowers by risk level, and provide data-driven recommendations to improve credit risk management.

---
## Objectives

The primary objectives of this project are to:

- Improve data quality through cleaning and validation.
- Identify the factors associated with loan default.
- Classify borrowers into risk categories.
- Support lending decisions with data-driven insights.
- Recommend strategies to reduce default risk and improve portfolio performance.
---

## Dataset Overview

The dataset contains **150 customer loan records** across multiple variables, including age, income, loan amount, credit score, employment status, loan purpose, and repayment status.

It was provided by **Tech Studio Academy** as part of a project-based data analytics programme for credit risk analysis.

![Dataset Preview (`loan.head()` output)](images/dataset_preview.png)

---
## Tools Used

- **Python:** Used for data cleaning, exploratory data analysis, feature engineering, and customer risk segmentation.
- **Pandas:** Used for data manipulation, transformation, and analysis.
- **Jupyter Notebook:** Used to develop and document the end-to-end analytical workflow.
---
## Data Preparation

Before the analysis, the dataset was cleaned and validated to ensure reliable and accurate results.

- Checked for missing values and confirmed that all records were complete.
- Verified that there were no duplicate records.
- Validated data types to ensure numerical and categorical variables were correctly formatted for analysis.
- Created a binary target variable by converting loan default status from text (`Yes`/`No`) to numerical values (`1`/`0`) to support statistical analysis and risk calculations.

![Missing Value Check (`loan.isnull().sum()` output)](images/missing_values_check.png)

![Duplicate Record Check (`loan.duplicated().sum()` output)](images/duplicate_record_check.png)

![Dataset Structure (`loan.info()` output)](images/dataset_structure.png)

![Feature Engineering (`defaulted_numeric` column creation)](images/feature_engineering.png)

---

## Feature Engineering

To support deeper analysis and customer risk profiling, new features were created from the original dataset.

- Converted the `Defaulted` column from text (`Yes`/`No`) into a binary numerical variable (`1`/`0`) to enable default rate calculations and statistical analysis.

- Created a `Risk_Segment` feature using a rule-based classification model to categorize borrowers into **High Risk**, **Medium Risk**, and **Low Risk** groups based on their credit score and previous default history.

![Binary Target Variable (`defaulted_numeric` feature creation)](images/defaulted_numeric_feature.png)

![Rule-Based Risk Segment Feature (`Risk_Segment` column creation)](images/risk_segment_feature.png)

---
## Executive Summary

The analysis revealed a high-risk lending portfolio with a significant concentration of borrowers likely to default.

| KPI | Value |
|------|-------|
| Portfolio Default Rate | 46.67% |
| High-Risk Borrowers | 109 (72.7%) |
| Total Borrowers | 150 |
| Total Capital Deployed | $218.1M |
| Average Loan Amount | $1.45M |
| Expected Monthly Cash Inflow | $13.46M |

> **Key Finding:** Nearly **1 in every 2 borrowers** has defaulted on their loan, while **72.7% of customers** were classified as high risk. These findings suggest that the current loan portfolio is heavily exposed to credit risk and may require stricter lending criteria and risk controls.

![Executive KPI Analysis Output](images/executive_kpi_summary.png)

---
## Key Business Insights

### What is the typical financial profile of a CrediTrust borrower?

![Borrower Profile Summary](images/borrower_profile.png)

The average borrower is 40 years old, earns approximately **$264,714 per year**, and applies for a loan of about **$1.45M**. The median credit score is **579**, which falls within the subprime credit range and suggests that many borrowers already have a higher risk of default.

---

### Do borrowers who default have lower credit scores?

![Credit Score by Default Status](images/credit_score_comparison.png)

Borrowers who defaulted had an average credit score of **532**, compared to **602** for borrowers who repaid successfully. This 70-point difference shows that credit score is one of the strongest indicators of whether a borrower is likely to default.

---

### Does employment status influence default risk?

![Defaults by Employment Status](images/employment_defaults.png)

Default rates were highest among unemployed borrowers, while self-employed borrowers also showed relatively high default levels. This suggests that borrowers with less stable income may find it more difficult to keep up with loan repayments.

---

### How many borrowers fall into each risk category?

![Portfolio Risk Segmentation](images/risk_segmentation.png)

Borrowers were grouped into High, Medium, and Low risk categories using a rule-based risk model. The analysis showed that **72.7%** of borrowers fall into the High-Risk category, indicating that a large portion of the portfolio is exposed to potential credit losses.

---

### Which loan products attract the highest-risk customers?

![Risk Segment by Loan Purpose](images/risk_purpose_chart.png)

High-risk borrowers were found across all loan categories but were most concentrated in Personal and Business loans. These loan types may require stricter approval criteria and closer monitoring to reduce future defaults.

---
## 📈 4. Descriptive Analysis (Understanding the Borrower Portfolio)

### Business Question 1: What is the typical financial profile of a CrediTrust applicant?
By generating descriptive summary statistics using `loan.describe()`, I created an empirical baseline of our average customer:
* **Average Age:** 40 years old
* **Average Annual Income:** `$264,714.00`
* **Average Requested Loan Size:** `$1,454,060.16`
* **Median Credit Score:** `579` *(This falls into the subprime/borderline credit band, indicating a historically weak borrower pool)*

---

### Business Question 2: Who are our highest-exposure borrowers?
* **Objective:** Identify the top 10 borrowers who hold the largest loan amounts to locate where the company's heaviest financial risk is concentrated.

#### 💻 Code Query Used:
```python
top_10_loans = loan.sort_values(by='Loan_Amount', ascending=False).head(10)
print(top_10_loans[['customer id', 'age', 'employment status', 'loan amount']])
```

#### 📋 Printed Text Result:
```text
Customer ID   Age   Employment Status   Loan Amount
1147          53    Employed            2,998,073
1026          47    Self-Employed       2,908,283
1009          31    Self-Employed       2,889,592
1080          21    Employed            2,884,433
1025          45    Unemployed          2,845,401
1057          46    Self-Employed       2,835,505
1065          34    Employed            2,831,573
1149          47    Self-Employed       2,783,317
1098          43    Employed            2,777,618
1077          27    Unemployed          2,767,867
```

* **Insight:** Sorting the data reveals that our largest individual loans reach up to nearly \$3 Million per customer (such as Customer 1147 at \$2,998,073). Crucially, the data shows that some of these top-exposure loans were given to **unemployed** individuals. Funding multi-million dollar loans for borrowers without a reliable income source creates an extreme concentration of risk for CrediTrust.

---

### Business Question 3: Are there extreme outliers in the financial columns that could skew the analysis?
* **Objective:** Run separate boxplot visualisations for each key financial column to find any weird, impossible, or extreme numbers that could mess up our averages.

#### 📈 1. Income Column Check
##### 💻 Code Query Used:
```python
import matplotlib.pyplot as plt
import seaborn as sns

plt.figure(figsize=(5, 4))
sns.boxplot(data=loan, y='income', color='skyblue')
plt.title('Income Distribution & Outliers')
plt.show()
```
##### 📊 Visual Chart Outcome:
![](images/income_outliers.png)

#### 📈 2. Loan Amount Column Check
##### 💻 Code Query Used:
```python
plt.figure(figsize=(5, 4))
sns.boxplot(data=loan, y='loan amount', color='salmon')
plt.title('Loan Amount Distribution & Outliers')
plt.show()
```
##### 📊 Visual Chart Outcome:
![](images/loan_amount_outliers.png)

#### 📈 3. Credit Score Column Check
##### 💻 Code Query Used:
```python
plt.figure(figsize=(5, 4))
sns.boxplot(data=loan, y='credit score', color='lightgreen')
plt.title('Credit Score Distribution & Outliers')
plt.show()
```
##### 📊 Visual Chart Outcome:
![](images/credit_score_outliers.png)

#### 📈 4. Monthly Installment Column Check
##### 💻 Code Query Used:
```python
plt.figure(figsize=(5, 4))
sns.boxplot(data=loan, y='monthly installments', color='violet')
plt.title('Monthly Installment Distribution & Outliers')
plt.show()
```
##### 📊 Visual Chart Outcome:
![](images/monthly_installment_outliers.png)

* **Analytical Findings:** Looking at all four charts separately, the numbers are wide but completely realistic. There are no impossible data entry mistakes that need to be deleted or cleaned out. This confirms that the high default problem is completely driven by actual customer credit profiles, not broken data.

---

### Business Question 4: What are the primary reasons why customers request loans from CrediTrust?
* **Objective:** Map customer demand patterns to see exactly why people apply for cash.

#### 💻 Code Query Used:
```python
plt.figure(figsize=(8, 4))
sns.countplot(data=loan, x='loan purpose', order=loan['loan purpose'].value_counts().index, palette='Blues_r')
plt.title('Primary Reasons for Requesting Loans')
plt.xticks(rotation=30)
plt.show()
```

#### 📊 Visual Chart Outcome:
![](images/loan_purposes.png)

* **Insight:** Personal loans and Business loans dominate our portfolio volume. Because these two categories are typically "unsecured" product lines—meaning they lack strong concrete physical collateral like a vehicle or real estate asset—they represent the highest risk products for CrediTrust to fund without strict underwriting.

---

## 📉 5. Default Risk Analysis (Identifying Risk Drivers)

---

### Business Question 5: Do people who default have a lower average credit score?
* **Objective:** Compare the credit scores of people who successfully paid back their loans versus those who defaulted.

#### 💻 Code Query Used:
```python
print(loan.groupby('defaulted')['credit score'].mean())

plt.figure(figsize=(6, 5))
sns.barplot(data=loan, x='defaulted', y='credit score', ci=None, palette='Set2')
plt.title('Average Credit Score: Repaid (No) vs Defaulted (Yes)')
plt.xlabel('Has the Customer Defaulted?')
plt.ylabel('Average Credit Score')
plt.show()
```

#### 📊 Visual Chart Outcome:
![](images/credit_score_comparison.png)

* **Insight:** There is a clear, definitive 70-point gap between the two groups. Those who pay consistently maintain an average score of 602, while those who fail to pay fall deep into subprime territory with an average score of 532. This proves that an automated credit floor is required to screen out unsafe applicants.

---

### Business Question 6: Does a borrower's employment status affect their likelihood of defaulting?
* **Objective:** Evaluate how different employment sectors handle their financial repayment agreements.

#### 💻 Code Query Used:
```python
plt.figure(figsize=(8, 4))
sns.countplot(data=loan, x='employment status', hue='defaulted', palette='viridis')
plt.title('Defaults Across Employment Statuses')
plt.xlabel('Employment Status')
plt.ylabel('Number of Customers')
plt.legend(title='Defaulted?')
plt.xticks(rotation=15)
plt.show()
```

#### 📊 Visual Chart Outcome:
![](images/employment_defaults.png)

* **Insight:** Unemployed applicants carry the absolute highest proportional default rate due to the complete lack of a regular salary stream. However, self-employed applications also carry substantial default numbers due to irregular business cash flow cycles.

---

## 🎯 6. Rule-Based Portfolio Risk Segmentation

### Business Question 7: How many of the current borrowers fall into High, Medium, and Low risk tiers?
* **Objective:** Programmatically divide the database into actionable categories using a multi-conditional rule-based function.

#### 💻 Code Query Used:
```python
def assign_risk_level(row):
    if row['credit score'] < 600 or row['previous default'] == 'Yes':
        return 'High Risk'
    elif 600 <= row['credit score'] <= 700:
        return 'Medium Risk'
    else:
        return 'Low Risk'

loan['Risk_Segment'] = loan.apply(assign_risk_level, axis=1)
print(loan['Risk_Segment'].value_counts())

plt.figure(figsize=(6, 4))
sns.countplot(data=loan, x='Risk_Segment', order=['Low Risk', 'Medium Risk', 'High Risk'], palette='coolwarm')
plt.title('CrediTrust Portfolio Risk Breakdown')
plt.xlabel('Risk Segment Category')
plt.ylabel('Number of Borrowers')
plt.show()
```

#### 📊 Visual Chart Outcome:
![](images/risk_segmentation.png)

* **Insight:** A staggering 72.7% (109 out of 150) of the active accounts belong in the High-Risk category. This means CrediTrust is heavily exposed to subprime capital losses because the baseline approval filter has been far too lenient.

---

### Business Question 8: Which loan purposes are our high-risk customers mostly applying for?
* **Objective:** Identify which loan product categories hold the highest concentration of toxic debt.

#### 💻 Code Query Used:
```python
plt.figure(figsize=(9, 5))
sns.countplot(data=loan, x='loan purpose', hue='Risk_Segment', palette='magma')
plt.title('Loan Purposes Demanded by Each Risk Tier')
plt.xlabel('Reason for Loan')
plt.ylabel('Number of Applications')
plt.xticks(rotation=30)
plt.legend(title='Risk Tier')
plt.show()
```

#### 📊 Visual Chart Outcome:
![](images/risk_purpose_chart.png)

* **Insight:** High-risk borrowers are not isolated to a single category—they are spread heavily across all four loan purposes. However, they are most dangerous inside the Personal and Business loan segments because these accounts lack physical property collateral for the company to seize and liquidate during a default emergency.

---

## 💼 7. Data-Backed Business Recommendations

The data shows that loan defaults are predictable. CrediTrust management should take immediate action and implement the following four credit policies:

1. **Set a hard credit score floor at 600.** 
   * **Action:** Update the loan approval software to automatically reject any applicant with a credit score below 600. 
   * **The Impact:** This firm limit will instantly block the riskiest applicants, protecting our multi-million dollar loan assets.

2. **Stop giving unsecured loans to unemployed applicants.**
   * **Action:** Change company policy to require valuable collateral or a high-credit co-signer for all unemployed individuals. 
   * **The Impact:** This lowers financial exposure to zero, ensuring the company can recover its cash if the borrower cannot pay.

3. **Mandate 12-month bank statement audits for self-employed workers.**
   * **Action:** Stop approving self-employed loans based on stated income alone and verify 12 months of official bank statements.
   * **The Impact:** This catches dropping business revenues early, ensuring the company only funds self-employed workers with a stable monthly profit.

4. **Build an automated Early Warning System.**
   * **Action:** Implement software alerts that flag an account the moment a customer misses a single payment or their credit score drops.
   * **The Impact:** This allows credit officers to step in with a payment plan immediately before a total default occurs.
---

## 🏁 8. Conclusion
CrediTrust's severe **46.67% portfolio default rate** is an underwriting and asset-filtering failure, not a market anomaly. The data clearly proves that loan defaults are tightly concentrated among applicants with subprime credit profiles, previous default histories, or volatile employment positions. By shifting from a loose screening model to the automated, data-validated risk tier structures outlined in this report, CrediTrust can systematically insulate its capital reserves, steady monthly cash flows, and build a safe, profitable loan portfolio.
