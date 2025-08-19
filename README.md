# Food Waste Management System

A data-driven project aimed at analyzing and managing food waste efficiently using **Python, Pandas, SQL, Streamlit, and Ngrok**.  
This project demonstrates how data analytics and interactive dashboards can help in reducing food waste and improving sustainability.

---

## Features
- **Data Analysis**: Clean, preprocess, and analyze food waste datasets using **Pandas**.  
- **SQL Integration**: Perform data storage, retrieval, and queries for structured insights.  
- **Visualization**: Generate meaningful graphs and charts to identify waste patterns.  
- **Interactive Dashboard**: Built with **Streamlit** for user-friendly interaction.  
- **Ngrok Deployment**: Share the dashboard publicly via secure tunnels.  

---

## Tech Stack
- **Programming Language**: Python  
- **Libraries**: Pandas, Matplotlib/Seaborn (if used), Streamlit  
- **Database**: SQL  
- **Deployment**: Ngrok  

---

## Install required libraries
- pip install pandas
- pip install streamlit
- pip install numpy

## Import libraries
- import pandas as pd
- import numpy as np
- import sqlite3
- from datetime import datetime

## Read the files
```
providers_path = "providers_data.csv"
receivers_path = "receivers_data.csv"
food_path      = "food_listings_data.csv"
claims_path    = "claims_data.csv"

# Read the files using 'pd.read_csv'
providers  = pd.read_csv(providers_path)
receivers  = pd.read_csv(receivers_path)
food       = pd.read_csv(food_path)
claims     = pd.read_csv(claims_path)

```
## Get the glimpse of file
```
# Peek
for name, df in [("providers", providers), ("receivers", receivers), ("food", food), ("claims", claims)]:
    print(f"\n=== {name.upper()} ===")
    print(df.shape)
    print(df.head(3))

```

## Clean and Standardise the dataset
##### Here we will clean the dataset such change the format of date columns from object to datetime. Also we will have to normalize the status values
```
# Clean and standardise the datatype
# Strip spaces in object columns
def strip_obj_cols(df):
    obj_cols = df.select_dtypes(include="object").columns
    df[obj_cols] = df[obj_cols].apply(lambda s: s.str.strip())
    return df

providers = strip_obj_cols(providers)
receivers = strip_obj_cols(receivers)
food = strip_obj_cols(food)
claims = strip_obj_cols(claims)

# Parse dates
# food['Expiry_Date'] is in string so now we will convert it to date (yyyy-mm-dd)
food['Expiry_Date'] = pd.to_datetime(food['Expiry_Date'], errors='coerce').dt.date

# claims['Timestamp'] is in string so we will also convert it to proper datetime
claims['Timestamp'] = pd.to_datetime(claims['Timestamp'], errors='coerce')

# Normalize Status values
valid_status = {"Pending","Completed","Cancelled"}
claims['Status'] = claims['Status'].str.title().where(claims['Status'].str.title().isin(valid_status), other="Pending")

# Quick null checks
for name, df in [("providers", providers), ("receivers", receivers), ("food", food), ("claims", claims)]:
    print(f"{name}: nulls\n", df.isna().sum())
```

## Create a sql database 
##### Now we will create a sql database to store the various data files
```
# create sqlite database
db_path = "food.db"
conn = sqlite3.connect(db_path)
conn.execute("PRAGMA foreign_keys = ON;")  # enforce FK
conn.execute("PRAGMA journal_mode = WAL;") # safer writes

# Write to staging (drops if exist)
providers.to_sql("stg_providers", conn, if_exists="replace", index=False)
receivers.to_sql("stg_receivers", conn, if_exists="replace", index=False)
food.to_sql("stg_food", conn, if_exists="replace", index=False)
claims.to_sql("stg_claims", conn, if_exists="replace", index=False)

print("Staging tables created.")

```

## Insights
- Identify which type of food contributes most to waste.
- Track waste trends over time (daily/weekly/monthly).
- Suggest preventive actions for restaurants, households, and NGOs.

## Impact
This project promotes sustainable development by helping organizations and individuals:

- Reduce food waste
- Save costs
- Contribute to environmental conservation





