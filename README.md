# Food Waste Management


Analyze and visualize food waste to find reduction opportunities.


## Stack
- Python, Pandas (ETL & analysis)
- SQL (SQLite by default via SQLAlchemy)
- Streamlit (dashboard)
- Ngrok (optional public URL)


## Quickstart
```bash
# 1) Create venv (optional)
python -m venv .venv && source .venv/bin/activate # Windows: .venv\Scripts\activate


# 2) Install deps
pip install -r requirements.txt


# 3) Configure DB
cp .env.example .env # edit if needed


# 4) Put your CSV at data/food_waste.csv
# Required columns: record_date, category, item_name, quantity_purchased, quantity_wasted


# 5) Run ETL (creates DB and loads data)
python -m src.etl


# 6) Launch dashboard
streamlit run app.py --server.port 8501
