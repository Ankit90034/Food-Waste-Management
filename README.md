# 🍽️ Food Waste Management System

A data-driven project aimed at analyzing and managing food waste efficiently using **Python, Pandas, SQL, Streamlit, and Ngrok**.  
This project demonstrates how data analytics and interactive dashboards can help in reducing food waste and improving sustainability.

---

## 🚀 Features
- 📊 **Data Analysis**: Clean, preprocess, and analyze food waste datasets using **Pandas**.  
- 🗄️ **SQL Integration**: Perform data storage, retrieval, and queries for structured insights.  
- 📈 **Visualization**: Generate meaningful graphs and charts to identify waste patterns.  
- 🌐 **Interactive Dashboard**: Built with **Streamlit** for user-friendly interaction.  
- 🔗 **Ngrok Deployment**: Share the dashboard publicly via secure tunnels.  

---

## 🛠️ Tech Stack
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
bash ```providers_path = "providers_data.csv"
receivers_path = "receivers_data.csv"
food_path      = "food_listings_data.csv"
claims_path    = "claims_data.csv"

# Read the files using 'pd.read_csv'
providers  = pd.read_csv(providers_path)
receivers  = pd.read_csv(receivers_path)
food       = pd.read_csv(food_path)
claims     = pd.read_csv(claims_path)

```bash

