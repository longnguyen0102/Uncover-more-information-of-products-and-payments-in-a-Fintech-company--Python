# Data wrangling - Fintech - Python

Please check the coding file or access via the link below:  
https://colab.research.google.com/drive/1507TAku0hhjmkd88r-9rUP9ATtvzsPEC?authuser=1     

Author: Nguyễn Hải Long  
Date: 2025-04  
Tools Used: Python  

---

## 📑 Table of Contents  
1. [📌 Background & Overview](#-background--overview)  
2. [📂 Dataset Description & Data Structure](#-dataset-description--data-structure)  
3. [🔎 Final Conclusion & Recommendations](#-final-conclusion--recommendations)

---

## 📌 Background & Overview  

### Objective:
### 📖 This project is about using Python to analyze given dataset.

✔️ Show up data as demand: number of pageview, visits; calculate the average of money spending by customers in a period of time...

### 👤 Who is this project for?  

✔️ Data analysts & business analysts.  
✔️ Decision-makers.

---

## 📂 Dataset Description & Data Structure  

### 📌 Data Source  
- Source: 
- Size: The dataset has 3 tables: payment_report (5 columns, 919 rows), product (3 columns, 492 rows), and transactions (9 columns, 1324002 rows).
- Format: .csv

### 📊 Data Structure & Relationships  
#### 1️⃣ Table used: 
Using all 3 tables of the dataset.  

#### 2️⃣ Table Schema & Data Snapshot:  
Table 1: payment_report  

| Field Name | Data Type |
|------------|-----------|
| report_month | object |
| payment_group | object |
| product_id | object |
| source_id | int64 |
| volume | int64 |

Table 2: product  

| Field Name | Data Type |
|------------|-----------|
| product_id | int64 |
| category | object |
| team_own | object |

Table 3: transactions

| Field Name | Data Type |
|------------|-----------|
| transaction_id | int64 |
| merchant_id | int64 |
| volume | int64 |
| transType | int64 |
| transStatus | int64 |
| sender_id | float64 |
| receiver_id | float64 |
| extra_info | object |
| timeStamp | int64 |

---

## ⚒️ Main Process

### 1️⃣ EDA
#### Import libraries and dataset, copy dataset:
```
# import libraries
import pandas as pd
import numpy as np
from google.colab import drive

# import csv files
from google.colab import drive
drive.mount('/content/drive')

path_payment_report = '/content/drive/MyDrive/DAC K34/Python/Project_2/payment_report.csv'
path_product = '/content/drive/MyDrive/DAC K34/Python/Project_2/product.csv'
path_transactions = '/content/drive/MyDrive/DAC K34/Python/Project_2/transactions.csv'

payment_report = pd.read_csv(path_payment_report)
product = pd.read_csv(path_product)
transactions = pd.read_csv(path_transactions)

# copy dataset
df_payment_report = payment_report
df_product = product
df_transactions = transactions
```

#### Dataframe df_payment_report  
Understand about data type / data value
```
df_payment_report.head()

# show rows and columns count
print(f'Rows count: {df_payment_report.shape[0]}\nColums count: {df_payment_report.shape[1]}')

# show data type
df_payment_report.info()

# further checking on columns
df_payment_report.shape
df_payment_report.describe()
```
Result:  
![](https://github.com/longnguyen0102/photo/blob/main/data_wrangling-fintech-python/python_data_wrangling_df_payment_report_eda_1.png)  

Checking unique & missing values
```
# check null values
df_payment_report.isnull().sum()

# check unique values
## print the percentage of unique
num_unique = df_payment_report.nunique().sort_values()
print('---Percentage of unique values (%)---')
print(100/num_unique)

# check missing data
missing_value = df_payment_report.isnull().sum().sort_values(ascending = False)
missing_percent = df_payment_report.isnull().mean().sort_values(ascending = False)
print('')
print('---Number of missing values in each column---')
print(missing_value)
print('')
print('---Percentage of missing values (%)---')
if missing_percent.sum():
  print(missing_percent[missing_percent > 0] * 100)
else:
  print('None')

# check for duplicates
## show number of duplicated rows
print('')
print(f'Number of entirely duplicated rows: {df_payment_report.duplicated().sum()}')
## show all duplicated rows
df_payment_report[df_payment_report.duplicated()]
```
Result:  
![](https://github.com/longnguyen0102/photo/blob/main/data_wrangling-fintech-python/python_data_wrangling_df_payment_report_eda_2.png)  

Handle missing values: There are no missing values.  

Handle duplicated values: There are no duplicated values.  



## 📌 Key Takeaways:  
✔️ Understanding the basics of SQL query.  
✔️ Know how to apply Window Functions when writing queries.  
✔️ Understanding real-world requirements when using SQl to retrieve neceesary data
