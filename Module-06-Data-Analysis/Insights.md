# 📈 Data Analysis & Statistical Modeling: From Excel to Python & SQL

This guide documents the workflow for identifying relationships, detecting anomalies, and performing high-scale data analysis across multiple platforms.

---

## 1. Visualizing Relationships in Excel

### **Generating a Scatter Chart**
A Scatter Chart is the best way to visually "confirm" if a correlation exists before you run a mathematical test.
* **Steps:** Select two columns -> **Insert** tab -> **Recommended Charts** -> **All Charts** -> **Scatter**.
* **Insight:** We prioritize charts with stronger correlation values.
    * **High Correlation (0.84):** `new_cases` vs. `new_deaths` (Shows a tight cluster of dots moving upward).
    * **Positive Correlation:** `new_vaccinations` vs. `new_deaths` (Helps visualize the impact of medical interventions).

---

## 2. Outlier Detection: The "Math" Approach
Outliers are data points that sit outside the "normal" range. We use the **Interquartile Range (IQR)** method to find them.

### **The 15-Year-Old Version:**
Imagine a line of people sorted by height. 
1. **Quartile 1 (Q1):** The height of the person at the 25% mark.
2. **Quartile 3 (Q3):** The height of the person at the 75% mark.
3. **Interquartile Range (IQR):** The distance between Q1 and Q3.
4. **Lower/Upper Bounds:** Anything more than $1.5 \times \text{IQR}$ away from the middle is an **Outlier**.

---

## 3. Data Analysis with Python

Python allows for automated and highly precise statistical testing.

### **Data Handling with Pandas & Parquet**
We use **Parquet** files because they are faster and smaller than CSVs.
```python
import pandas as pd

# Load high-performance data
df = pd.read_parquet("transactions.parquet")

# Create a Pivot Table to compare regions and dispute types
pivot = df.pivot_table(index='Acquirer Region', 
                       columns='Dispute Type', 
                       values='Transaction ID', 
                       aggfunc='count')
```

---

## 4. Statistical Significance Testing (The "Is it Real?" Test)

### **The Concept**
In data analysis, seeing a pattern (like "Sales went up when it rained") isn't enough. It might just be a coincidence. **Statistical Significance** is a mathematical way to prove that your findings are "real" and likely to happen again, rather than just being a lucky guess.

Imagine you flip a coin 5 times and get "Heads" every time. Is the coin broken, or were you just lucky?
* **P-Value:** This is a number that tells you the probability that your result happened by pure luck.
* **The 0.05 Rule (Alpha):** Scientists generally agree that if there is less than a **5% chance (0.05)** that the result was luck, then the result is "Statistically Significant" (The coin is likely broken!).

---

### **Python Implementation (Scipy)**

We use the `scipy.stats` library to run a **Pearson Correlation Test**. This gives us two numbers: the strength of the relationship and the P-value.

```python
import scipy.stats as stats

# 1. Calculate the basic correlation
correlation = new_df['Approved'].corr(new_df['Amount'])

# 2. Perform the Significance Test (P-Value)
pearson_corr, p_value = stats.pearsonr(new_df['Approved'], new_df['Amount'])

# 3. The "0.05 Rule"
alpha = 0.05 
if p_value < alpha:
    print("The correlation is statistically significant (It's a real pattern).")
else:
    print("The correlation is not significant (Might be a coincidence).")
```

[View Full Python Notebook](https://colab.research.google.com/drive/1wEUEeF_e2SSmS9uf2-3fZJQ2kEFRnxah)

---

## 4. Data Analysis with SQL & SQLAlchemy

While Excel is limited to about 1 million rows, SQL databases can handle billions. We use **SQLAlchemy** as a "bridge" to let Python talk to these databases.

### **SQLAlchemy: The "Universal Translator"**
* **What is it?** A Python library (ORM) that allows you to connect to and query databases like MySQL, PostgreSQL, and SQLite using a unified syntax.
* **Why we need it:** Without it, you would have to write different code for every different type of database. SQLAlchemy makes your data work "portable."

### **Python Implementation (SQLAlchemy + Pandas)**
```python
import pandas as pd
import sqlalchemy as sa

# 1. Create the 'Engine' (The connection string)
# Format: "database_type+driver://username:password@host/database_name"
engine = sa.create_engine("mysql+pymysql://guest:relational@db.relational-data.org/stats")

# 2. Run a SQL query and load it directly into a Pandas DataFrame
# This counts how many total rows (posts) are in the database
df_counts = pd.read_sql('SELECT COUNT(*) FROM posts', engine)

print(df_counts)
```

[SQL Notebook](https://colab.research.google.com/drive/1j_5AsWdf0SwVHVgfbEAcg7vYguKUN41o)

---

## 5. Modern Tools: Datasette & DuckDB

As data grows beyond the capabilities of traditional spreadsheets, specialized tools are used to explore and analyze massive datasets with high efficiency.

### **Datasette: The Instant Data Explorer**
* **What is it?** An open-source tool for exploring and publishing data. It turns any SQLite database into an interactive, searchable website.
* **Why we need it:** Instead of writing complex code just to "see" what is inside a database file, you can browse tables, run SQL queries, and export results directly in your web browser.
* **The Workflow:**
    1. Create or download a sample dataset (e.g., `ecommerce.db`).
    2. Run the command: `datasette ecommerce.db`.
    3. Open the provided link in your browser to explore your data visually.

### **DuckDB: The High-Performance Analytical Engine**
* **What is it?** An "In-Process" SQL database management system. Think of it as **SQLite for Analytics**. 
* **Why we need it:** Standard databases (like MySQL) are "Row-oriented," which is slow for math. DuckDB is **"Columnar-oriented,"** meaning it only reads the specific columns needed for a calculation, making it incredibly fast for data analysis.



#### **Mixing DuckDB and Pandas**
One of DuckDB's "Superpowers" is its ability to run SQL queries directly on top of existing Pandas DataFrames as if they were SQL tables.

```python
import duckdb
import pandas as pd

# Assume 'df' is a Pandas DataFrame you already loaded
# You can run a SQL query on 'df' without any extra setup:
result = duckdb.query("SELECT Region, COUNT(*) FROM df GROUP BY Region").to_df()

print(result)
```

---

### How it is Better:
* Zero Setup: No server to install; it runs inside your Python script or terminal.

* Extreme Speed: It can process millions of rows in milliseconds on a standard laptop.

* Large File Support: It can query CSV, JSON, and Parquet files directly without "importing" them first.

---

### **The Best Use Case: When to use DuckDB?**

1.  **The "Big Data" Spreadsheet:** You have a 2GB CSV file that crashes Excel every time you try to open it.
2.  **The "Local" Data Warehouse:** You need to join three different Parquet files and a CSV to find a specific trend, but you don't want to set up a cloud database.
3.  **Fast Prototyping:** You are writing a Python script and need a database that is as easy to use as a dictionary but as powerful as a professional SQL server.

---

### 📈 Summary Comparison: Modern Data Tools

| Tool | Primary Use Case | Example |
| :--- | :--- | :-- |
| **Datasette** | Exploring/Publishing SQLite. | A "Web Browser" for your database files. |
| **DuckDB** | High-speed math on big files. | A "Super-Engine" for running SQL on top of Python. |
| **Pandas** | Detailed cleaning and modeling. | A "Swiss Army Knife" for manipulating data tables. |