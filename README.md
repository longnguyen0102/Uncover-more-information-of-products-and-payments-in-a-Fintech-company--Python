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
  <summary>💾 <em>Import libraries and dataset, copy dataset, and explore tables:</em></summary>
  
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

> #### Dataframe ***df_payment_report***:  
>   1. **Structure:** The dataframe has 5 columns (`report_month`, `payment_group`, `product_id`, `source_id`, `volume`) and 919 rows.  
>   2. **Data quality:** There are no missing values and duplicated rows among columns.  
>   3. **Identified issues:** `report_month` has string datatype, it can be changed to datetime for easy analysis in time point-of-view.  
>   4. **Observations:** The percentage of unique values in each column is acceptable. No action needed. 
 
>  #### Dataframe ***df_product***:
>    1. **Structure:** The dataframe has 3 columns (`product_id`, `category`, `team_own`) and 492 rows.  
>    2. **Data quality:** There are no missing values and duplicated rows among columns.  
>    3. **Unique values:**  
>      *   `team_own` has about 3 unique values, meaning only 3 teams owning all products.  
>      *   There are about 17 unique values in `category`.  
>      *   17 categories have total 492 products (~0.2%).  
>    4. **Observations:** Dataframe has a well structure. No interfere actions needed.
 
>  #### Dataframe ***df_transactions***:
>    1. **Structure:** The dataframe has 10 columns and 1,324,002 rows.  
>    2. **Data quality:** There are no missing values and duplicated rows among columns.  
>       *   **Duplicates:** There are 28 duplicated rows, they need to be removed for the correct calculation.  
>       *   **Data type:** `timeStamp` should not be in int64 type, it needs to be changed to datetime data type same as `report_month` of ***df_payment_report***. `sender_id` and `receiver_id` should be changed to int64.  
>    3. **Missing values:**  
>       *   `extra_info` missing more than 99.5% (almost empty).
>       *   `receiver_id` missing 12.4%.
>       *   `sender_id` missing 3.7%. 
>    4. **Observations:** Most columns has low percentage of unique values except of `transaction_id` and `timeStamp` (~99.9%).

<details>
  <summary>💾 <em>Convert datatype and create dataframe payment_enriched:</em></summary>
 
  ```python
  # Convert timeStamp to datetime
  df_transactions['timeStamp'] = pd.to_datetime(df_transactions['timeStamp'], unit='ms')
  
  # Convert sender_id and receiver_id to Int64
  df_transactions['sender_id'] = df_transactions['sender_id'].astype('Int64')
  df_transactions['receiver_id'] = df_transactions['receiver_id'].astype('Int64')
  ```

  ```python
  # Create dataFrame payment_enriched
  payment_enriched = df_payment_report.merge(df_product, on='product_id', how='left')
  payment_enriched.info()
  ```
    
  ![](https://github.com/longnguyen0102/photo/blob/main/data_wrangling-fintech-python/python_data_wrangling_create_df_payment_enriched.png)  

</details>  

### Purpose of merging 2 dataframes:  
> Merging 2 dataframes ***df_payment_report*** and ***df_product*** for further analysis in products, team performance. The purpose of this merge is to combine the payment volume data with detailed product information. This will help further analysis with richer information.
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

> 1.  **1976** is the clear leader, with a total volume exceeding **61.7 billion**. This suggests it is likely a core service or a highly popular utility within the e-wallet ecosystem.  
> 2.  Follow up are **429** and **372** both contributing significantly with volumes around **14.6 billion** and **13.7 billion** respectively.  
> 3.  **Concentration:** There is a very large gap between the top product and the runners-up, indicating that the company's transaction volume is heavily concentrated in a few key products.  

### 2/ Given that 1 product_id is only owed by 1 team, are there any abnormal products against this rule?  
<details>
  <summary><em>Code:</em></summary>

  ```python
  # Double-check: Ensure no product_id is duplicated in the original product table
  duplicated_product_metadata = df_product[df_product.duplicated('product_id', keep=False)]
  if duplicated_product_metadata.empty:
      print('Confirmed: Each product_id exists only once in the product mapping table.')
  else:
      display(duplicated_product_metadata)
  ```
  ![](https://github.com/longnguyen0102/photo/blob/main/data_wrangling-fintech-python/python_data_wrangling_query_2_result_1.png)
 
  ```python
  df_1_product_1_team = payment_enriched.groupby('product_id')['team_own'].nunique().reset_index()  
  df_1_product_1_team[df_1_product_1_team['team_own'] != 1]
  ```
</details>  
  
![](https://github.com/longnguyen0102/photo/blob/main/data_wrangling-fintech-python/python_data_wrangling_query_2_result_2.png)  

> 1.  **Missing Mappings:** Products with id **3**, **1976**, and **10033** are owned by no team. This indicates these products are present in the `payment_report` but do not have a corresponding entry in the `product` lookup table (resulting in NaNs after the left join).  
> 2.  **No Duplicated Ownership:** There are no products with a `team_own` count greater than 1. This means the rule that 'one product is owned by only one team' is technically followed for all identified products.
> 3.  **Action:** We should investigate the metadata for products **3, 1976, and 10033** to ensure they are assigned to the correct teams, as they currently lack ownership information in our analysis.  

### 3/ Find the team has had the lowest performance (lowest volume) since Q2.2023. Find the category that contributes the least to that team.
<details>
  <summary><em>Code:</em></summary>
 
  ```python
  df_low = payment_enriched[payment_enriched['report_month'] >= '2023-04']

  team_volume = df_low.groupby('team_own')['volume'].sum().reset_index()
  lowest_performing_team = team_volume.sort_values(by='volume', ascending=True).iloc[0]
  highest_performing_team = team_volume.sort_values(by='volume', ascending=False).iloc[0]
  print(f"Lowest performing team since Q2.2023: {lowest_performing_team['team_own']} with total volume {lowest_performing_team['volume']}")
  print(f"Highest performing team since Q2.2023: {highest_performing_team['team_own']} with total volume {highest_performing_team['volume']}")
  print("")
  
  lowest_team_df = df_low[df_low['team_own'] == lowest_performing_team['team_own']]
  category_least = lowest_team_df.groupby('category')['volume'].sum().reset_index()
  least_contributing_category = category_least.sort_values(by='volume', ascending=True).iloc[0]
  
  highest_team_df = df_low[df_low['team_own'] == highest_performing_team['team_own']]
  category_most = highest_team_df.groupby('category')['volume'].sum().reset_index()
  most_contributing_category = category_most.sort_values(by='volume', ascending=False).iloc[0]
  
  print(f"Category contributing the least to {lowest_performing_team['team_own']}: {least_contributing_category['category']} with total volume {least_contributing_category['volume']}")
  print(f"Category contributing most to {highest_performing_team['team_own']}: {most_contributing_category['category']} with total volume {most_contributing_category['volume']}")
  ```
</details>  
  
![](https://github.com/longnguyen0102/photo/blob/main/data_wrangling-fintech-python/python_data_wrangling_query_3_result.png)  

> 1.   Underperformance of APS: The **APS** team stands out as having the lowest overall payment volume (**51,141,753**) compared to other teams since Q2.2023. This is a critical area for investigation. Comparing to the ASD - the highest performing team - with total volume of **31.09 billion**.  
> 2.   The **PXXXXXE** category is the weakest link, generating the lowest volume (**25,232,438**) compares to **21.3 billion** of **PXXXXXB**. This suggests that the products or services within this category might be struggling, or there might be issues with their marketing, user experience, or competitive positioning.  

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

> 1. **38** has the most volume (**36,527,454,759**) which is twice bigger than the second place (**39**) with **16,119,058,662**.
> 2. The volume of these 3 source_id has a big gap between them.
> 3.  Suggestion:
>   *   Further checking on top 3 of source_id to identify the causes of refund: system error, payment error, etc.
>   *   Compare with 'volume' to identify the percentage of refund in order to evaluate the risk and operating eficiency.

### 5/ Define type of transactions `transaction_type` for each row, given:  
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
    # Condition Bank Transfer using transType and merchant_id
    ## Run each row of transType and merchant_id
    transType = row['transType']
    merchant_id = row['merchant_id']
  
    # 3 conditions: transType = 2, transType = 8 và remaining
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
  
  # Apply to trans_type
  df_transactions['transaction_type']=df_transactions.apply(trans_type, axis=1)
  df_transactions.head()
  ```
</details>  
  
![](https://github.com/longnguyen0102/photo/blob/main/data_wrangling-fintech-python/python_data_wrangling_query_5_result_1.png)  

<detail>
  <summary><em>Summary of types of transactions</em></summary>

  ```python
  # Showing count of transaction_type and total_volume of each transaction
  transaction_summary = df_transactions.groupby('transaction_type').agg(
      count=('transaction_id', 'count'),
      total_volume=('volume', 'sum')
  ).reset_index().sort_values(by='count', ascending=False)
  
  # Count_percentage
  transaction_summary['count_percentage'] = (transaction_summary['count'] / transaction_summary['count'].sum()) * 100
  
  display(transaction_summary)
  ```

</detail>

![](https://github.com/longnguyen0102/photo/blob/main/data_wrangling-fintech-python/python_data_wrangling_query_5_result_2.png)

> 1. **Invalid Transaction** has about **21.94%**, this means there might be an error during payment process or problems with data collecting process.  
> 2. **Bank Transfer Transaction** and **Withdraw Money Transaction** are almost the same ration (**~2.86%** and **~2.54**). These numbers show the "green flag" from customers about the company.  
> 3. When looking at 'total_volume' and 'count'columns, **Bank Transger Transaction** has the most average amount for each transaction. Second place is **Top Up Money Transaction**.  

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

> 1. **Top Up Money Transacton** has the most volume with **108,606,478,829** however it is on second place of unique senders (**110,409**) and receivers (**110,409**). This is the most important activity in an e-wallet company.  
> 2. The most number is **Payment Transaction** with **398,677** transcations. It has the total volume of **71,851,515,181**. However, everyone still use this transaction the most with **139,583** of senders and **113,298** of receivers.  
> 3. **Split Bill Transaction** is the least of all with **1376** transactions, **4,901,464** of volume, **1,323** senders and **572** receivers. This function is not preferred.

## 📌 Key Takeaways:  
✔️ Understanding the basics and uses of Python in exploring and extracting data.  
✔️ This project helps the company identify which products can be considered as potential key products in the future, and which ones should be re-evaluated due to high return rates.  
✔️ Data incompleteness negatively impacts the analysis of team performance as well as the sales and revenue evaluation of products.  
✔️ Through deeper analysis, we can uncover which payment methods are most preferred by consumers, and which ones need to be optimized to minimize operational costs or maximize user adoption.
