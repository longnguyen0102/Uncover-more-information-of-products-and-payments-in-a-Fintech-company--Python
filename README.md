# Uncover more information of products and payments in a Fintech company | Python

Please check the coding below or access via the link below:  
🔗 https://colab.research.google.com/drive/1bqe2NRXETMsebmrjdtP1TmfiAxG1UJj5?usp=sharing 🔗     

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
### 📖 What is this project about?  

- This analysis is based on a dataset consisting of three CSV files.
- The objective is to gain insights into the payment or transaction status within an e-wallet company.
- Additionally, the analysis aims to evaluate the performance of various teams in order to assess operational efficiency and identify product groups with the least contribution.
- Another key focus is to categorize different types of payment methods, enabling cost optimization and improved financial planning.  

### 👤 Who is this project for?  

✔️ Data analysts & business analysts.  
✔️ Decision-makers.

---

## 📂 Dataset Description & Data Structure  

### 📌 Data Source  
- Size: The dataset has 3 tables: payment_report (5 columns, 919 rows), product (3 columns, 492 rows), and transactions (9 columns, 1324002 rows).
- Format: .csv

### 📊 Data Structure & Relationships  
#### 1️⃣ Table used: 
Using all 3 tables of the dataset.  

#### 2️⃣ Table Schema & Data Snapshot:  

<details>
  <summary><em>Table 1: payment_report</em></summary>  
  
  *This table is monthly payment volume of products.*  
  
  | Field name | Data type |
  |------------|-----------|
  | report_month | object |
  | payment_group | object |
  | product_id | object |
  | source_id | int64 |
  | volume | int64 |
</details>

<details>
  <summary><em>Table 2: product</em></summary>  
  
  *This table shows the information of products.*  
  
  | Field name | Data type |
  |------------|-----------|
  | product_id | int64 |
  | category | object |
  | team_own | object |
</details>

<details>
  <summary><em>Table 3: transactions</em></summary>  

  *This table show the information of transactions.*  
  
  | Field name | Data type |
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
</details>

---

## ⚒️ Main Process

## 1️⃣ EDA
<details>
  <summary><em>Import libraries and dataset, copy dataset, and explore tables:</em></summary>
  
  ```python
  # import library
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

  ## Understand about data type / data value and checking unique & missing values of *df_payment_report*:    
  ``` python
  df_payment_report.head()
  
  # show rows and columns count
  print(f'Rows count: {df_payment_report.shape[0]}\nColums count: {df_payment_report.shape[1]}')
  print('')
  
  # show data type
  df_payment_report.info()
  
  # further checking on columns
  df_payment_report.shape
  df_payment_report.describe()
  
  # check null values
  df_payment_report.isnull().sum()
  
  # check unique values
  num_unique = df_payment_report.nunique().sort_values()
  print('')
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
  <img src="https://github.com/longnguyen0102/photo/blob/main/data_wrangling-fintech-python/python_data_wrangling_df_payment_report_eda.png"/>

  ## Understand about data type / data value and checking unique & missing values of *df_product*:  
   ```python
  df_product.head()
  
  # show rows and columns count
  print(f'Rows count: {df_product.shape[0]}\nColums count: {df_product.shape[1]}')
  print('')
  
  # show data type
  df_product.info()
  
  # further checking on columns
  df_product.shape
  df_product.describe()
  
  # check null values
  df_product.isnull().sum()
  
  # check unique values
  num_unique = df_product.nunique().sort_values()
  print('')
  print('---Percentage of unique values (%)---')
  print(100/num_unique)
  
  # check missing data
  missing_value = df_product.isnull().sum().sort_values(ascending = False)
  missing_percent = df_product.isnull().mean().sort_values(ascending = False)
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
  print(f'Number of entirely duplicated rows: {df_product.duplicated().sum()}')
  ## show all duplicated rows
  df_product[df_product.duplicated()]
  ```  
  <img src="https://github.com/longnguyen0102/photo/blob/main/data_wrangling-fintech-python/python_data_wrangling_df_product_eda.png"/>

  ## Understand about data type / data value and checking unique & missing values of *df_transactions*:  
  ```python
  df_transactions.head()
  
  # show rows and columns count
  print(f'Rows count: {df_transactions.shape[0]}\nColums count: {df_transactions.shape[1]}')
  print('')
  
  # show data type
  df_transactions.info()
  
  # further checking on columns
  df_transactions.shape
  df_transactions.describe()
  
  # check null values
  df_transactions.isnull().sum()
  
  # check unique values
  num_unique = df_transactions.nunique().sort_values()
  print('')
  print('---Percentage of unique values (%)---')
  print(100/num_unique)
  
  # check missing data
  missing_value = df_transactions.isnull().sum().sort_values(ascending = False)
  missing_percent = df_transactions.isnull().mean().sort_values(ascending = False)
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
  print('')
  print(f'Number of entirely duplicated rows: {df_transactions.duplicated().sum()}')
  ## show all duplicated rows
  df_transactions[df_transactions.duplicated()]
  ```  
  ![](https://github.com/longnguyen0102/photo/blob/main/data_wrangling-fintech-python/python_data_wrangling_df_transactions_eda_1.png)  
  ![](https://github.com/longnguyen0102/photo/blob/main/data_wrangling-fintech-python/python_data_wrangling_df_transactions_eda_2.png)  
  
</details>

### Briefing of dataframe:  

> Dataframe ***df_payment_report***:
> 1. **Structure:** The dataframe has 5 columns ('report_month', 'payment_group', 'product_id', 'source_id', 'volume') and 919 rows.  
> 2. **Data quality:** There are no missing values and duplicated rows among columns.  
> 3. **Identified issues:** 'report_month' has string datatype, it can be changed to datetime for easy analysis in time point-of-view.  
> 4. **Observations:** The percentage of unique values in each column is acceptable. No action needed.
> 
> Dataframe ***df_product***:
> 1. **Structure:** The dataframe has 3 columns ('product_id', 'category', 'team_own') and 492 rows.  
> 2. **Data quality:** There are no missing values and duplicated rows among columns.  
> 3. **Unique values:**  
> *   'team_own' has about 3 unique values, meaning only 3 teams owning all products.  
> *   There are about 17 unique values in 'category'.  
> *   17 categories have total 492 products (~0.2%).  
> 4. **Observations:** Dataframe has a well structure. No interfere actions needed.
> 
> Data in table ***df_transactions***:
> 1. **Structure:** The dataframe has 10 columns and 1,324,002 rows.  
> 2. **Data quality:** There are no missing values and duplicated rows among columns.  
>
> *   **Duplicates:** There are 28 duplicated rows, they need to be removed for the correct calculation.  
> *   **Data type:** *timeStamp* should not be in int64 type, it needs to be changed to datetime data type same as 'report_month' of ***df_payment_report***. 'sender_id' and *receiver_id* should be > changed to int64.  
> 3. **Missing values:**  
> *   'extra_info' missing more than 99.5% (almost empty).  
> *   'receiver_id' missing 12.4%.  
> *   'sender_id' missing 3.7%.  
> 4. **Observations:** Most columns has low percentage of unique values except of 'transaction_id' and 'timeStamp' (~99.9%).

<details>
  <summary><em>💾 Create dataframe payment_enriched:</em></summary>
 
  ```python
  payment_enriched = df_payment_report.merge(df_product, on='product_id', how='left')
  payment_enriched.info()
  ```   
    
  ![](https://github.com/longnguyen0102/photo/blob/main/data_wrangling-fintech-python/python_data_wrangling_create_df_payment_enriched.png)  

</details>  

### Purpose of merging 2 dataframes:  
> Merging 2 dataframes payment_report and product for further analysis in products, team performance. The purpose of this merge is to combine the payment volume data with detailed product information. This will help further analysis with richer information.  
## 2️⃣ Data wrangling

### 1/ Top 3 product_ids with the highest volume.  
<details>
  <summary><em>Code:</em></summary>
 
  ```python
  df_top_3 = df_payment_report.groupby('product_id')['volume'].sum().reset_index()
  
  df_top_3 = df_top_3.sort_values(by=['volume'], ascending=False)
  
  df_top_3.head(3)
  ```
</details>  
  
![](https://github.com/longnguyen0102/photo/blob/main/data_wrangling-fintech-python/python_data_wrangling_query_1_result.png)  

> Products with id "1976", "429", "372" have the highest volume. These items might be key products in the future.  

### 2/ Given that 1 product_id is only owed by 1 team, are there any abnormal products against this rule?  
<details>
  <summary><em>Code:</em></summary>
 
  ```python
  df_1_product_1_team = payment_enriched.groupby('product_id')['team_own'].nunique().reset_index()
  
  df_1_product_1_team[df_1_product_1_team['team_own'] != 1]
  ```
</details>  
  
![](https://github.com/longnguyen0102/photo/blob/main/data_wrangling-fintech-python/python_data_wrangling_query_2_result.png)  

> Product with id "3", "1976", and "10033" are not owned by any team. Lacking information might lead to challenge in accountability when issues occur, and may also impact the ability to analyze performance among teams.  

### 3/ Find the team has had the lowest performance (lowest volume) since Q2.2023. Find the category that contributes the least to that team.
<details>
  <summary><em>Code:</em></summary>
 
  ```python
  df_low = payment_enriched[payment_enriched['report_month'] >= '2023-04']
  
  
  team_volume = df_low.groupby('team_own')['volume'].sum().reset_index()
  lowest_performing_team = team_volume.sort_values(by='volume', ascending=True).iloc[0]
  
  print(f"Lowest performing team since Q2.2023: {lowest_performing_team['team_own']} with total volume {lowest_performing_team['volume']}")
  
  
  lowest_team_df = df_low[df_low['team_own'] == lowest_performing_team['team_own']]
  category_contribution = lowest_team_df.groupby('category')['volume'].sum().reset_index()
  least_contributing_category = category_contribution.sort_values(by='volume', ascending=True).iloc[0]
  
  print(f"Category contributing the least to {lowest_performing_team['team_own']}: {least_contributing_category['category']} with total volume {least_contributing_category['volume']}")
  ```
</details>  
  
![](https://github.com/longnguyen0102/photo/blob/main/data_wrangling-fintech-python/python_data_wrangling_query_3_result.png)  

> The team has lowest performance is "ASL" with the volume "39000" and the category that contributes is "PXXXXXF". "ASL" should have a plan to improve performance  

### 4/ Find the contribution of source_ids of refund transactions (payment_group = ‘refund’), what is the source_id with the highest contribution?  
<details>
  <summary><em>Code:</em></summary>
 
  ```python
  payment_report_refund = df_payment_report[payment_report.payment_group == 'refund']
  payment_report_refund = payment_report_refund[['source_id','volume']].groupby(by=['source_id']).sum().reset_index().sort_values('volume', ascending=False)
  
  payment_report_refund.head()
  ```
</details>  
  
![](https://github.com/longnguyen0102/photo/blob/main/data_wrangling-fintech-python/python_data_wrangling_query_4_result.png)

> source_id = 38 has the highest contribution, with the volume = 36,527,454,759.  

### 5/ Define type of transactions (‘transaction_type’) for each row, given:  
### - transType = 2 & merchant_id = 1205: Bank Transfer Transaction  
### - transType = 2 & merchant_id = 2260: Withdraw Money Transaction  
### - transType = 2 & merchant_id = 2270: Top Up Money Transaction  
### - transType = 2 & others merchant_id: Payment Transaction  
### - transType = 8, merchant_id = 2250: Transfer Money Transaction  
### - transType = 8 & others merchant_id: Split Bill Transaction  
### - Remained cases are invalid transactions  
<details>
  <summary><em>Code:</em></summary>
 
  ```python
  def trans_type(row):
    # condition Bank Transfer tra cứu với transType và merchant_id
    ## run each row of transType và merchant_id
    transType = row['transType']
    merchant_id = row['merchant_id']
  
    # split into 3 cases: transType = 2, transType = 8 and else.
    if transType == 2:
      if merchant_id == 1205:
        return 'Bank Transfer Transaction'
      elif merchant_id == 2260:
        return 'Withdraw Money Transaction'
      elif merchant_id == 2270:
        return 'Top Up Money Transaction'
      else:
        return 'Payment Transaction'
    elif transType == 8:
      if merchant_id == 2250:
        return 'Transfer Money Transaction'
      else:
        return 'Split Bill Transacion'
    else:
      return 'Invalid Transaction'
  
  # apply trans_type
  df_transactions['transaction_type']=df_transactions.apply(trans_type, axis=1)
  df_transactions.head()
  ```
</details>  
  
![](https://github.com/longnguyen0102/photo/blob/main/data_wrangling-fintech-python/python_data_wrangling_query_5_result.png)

> Creating a new column called "transaction_type" to segment the type of trasaction based on demand above.  

### 6/ Of each transaction type (excluding invalid transactions): find the number of transactions, volume, senders and receivers.  
<details>
  <summary><em>Code:</em></summary>
 
  ```python
  valid_transactions = df_transactions[df_transactions['transaction_type'] != 'Invalid Transaction']
  valid_transactions
  ```
  
  ![](https://github.com/longnguyen0102/photo/blob/main/data_wrangling-fintech-python/python_data_wrangling_query_6_result_1.png)  
 
  ```python
  valid_transactions.groupby(by = 'transaction_type').agg(total_transactions=('transaction_id', 'nunique'),
                                                          total_volume=('volume', 'sum'),
                                                          sender_count=('sender_id', 'nunique'),
                                                          receiver_count=('receiver_id', 'nunique'))
  ```
</details>  
  
![](https://github.com/longnguyen0102/photo/blob/main/data_wrangling-fintech-python/python_data_wrangling_query_6_result_2.png)

> These are few insights to be drawn from:  
> - "Payment Transaction" is the most frequent transaction type in terms of both transaction count and user engagement.  
> - "Top Up Money Transaction" and "Bank Transfer Transaction" lead in terms of total transaction volume, making them critical for analyzing high-value user behavior such as top-ups and large transfers.  
> - "Split Bill Transaction" has low usage frequency, suggesting it may not be a core feature or is underutilized by users.  

## 📌 Key Takeaways:  
✔️ Understanding the basics and uses of Python in exploring and extracting data.  
✔️ This project helps the company identify which products can be considered as potential key products in the future, and which ones should be re-evaluated due to high return rates.  
✔️ Data incompleteness negatively impacts the analysis of team performance as well as the sales and revenue evaluation of products.  
✔️ Through deeper analysis, we can uncover which payment methods are most preferred by consumers, and which ones need to be optimized to minimize operational costs or maximize user adoption.
