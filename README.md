# 🧹 Pandas Data Cleaning & Transformation Showcase

<div align="center">

![Python](https://img.shields.io/badge/Python-3.8%2B-blue?style=for-the-badge&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-2.0%2B-150458?style=for-the-badge&logo=pandas&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=for-the-badge&logo=jupyter&logoColor=white)
![Data Cleaning](https://img.shields.io/badge/Data%20Wrangling-Exploratory%20Analysis-success?style=for-the-badge)

*A comprehensive, hands-on repository demonstrating real-world data cleaning, transformation, and exploratory data analysis (EDA) techniques using **Python** and **Pandas**.*

</div>

---

## 📖 Overview

Raw real-world datasets are rarely clean. They come with inconsistent formatting, missing values, redundant columns, duplicate entries, and incorrect data types.

This repository serves as both a **practical workspace** and an **interactive reference guide** for mastering **Pandas** data manipulation workflows. Featured inside is an end-to-end cleaning pipeline applied to the **New York City Airbnb Dataset** (~100,000+ listings), transforming messy raw data into analytics-ready structured datasets exported in both **CSV** and **Excel** formats.

---

## 🚀 Key Techniques & Workflows Covered

### 1️⃣ Data Inspection & Profiling
- Initial schema assessment using `.head()`, `.info()`, and `.columns`.
- Inspecting column data types, memory footprint, and identifying mixed-type warnings.

### 2️⃣ Dimensionality Reduction & Redundancy Filtering
- **Filtering Columns (Whitelist Approach):** Retaining essential analytical attributes (`NAME`, `host id`, `lat`, `long`, `price`, etc.).
- **Dropping Redundant Columns (Blacklist Approach):** Removing sparse or irrelevant metadata (`license`, `house_rules`, `reviews per month`, etc.).

### 3️⃣ Standardizing Column Naming Conventions
- Renaming raw column headers for consistent casing, spacing, and readability across data pipelines.

### 4️⃣ Deduplication
- Detecting duplicate rows and redundant host records using `.duplicated().sum()`.
- Removing exact and subset duplicates while preserving data integrity (`.drop_duplicates()`).

### 5️⃣ Handling Missing & Null Values (`NaN`)
- Profiling null distributions across features.
- Cleaning and treating missing entries using targeted filtering and `.dropna()`.

### 6️⃣ String Parsing & Data Type Transformations
- **Currency Clean-up:** Stripping special symbols (e.g., `$` signs) from text columns (`price`, `service fee`) using Pandas string methods (`.str.replace()`).
- **Type Casting:** Converting clean numeric strings into native integer/floating-point types (`int64` / `float64`) ready for statistical operations and aggregation.
- **Categorical Normalization:** Standardizing text labels (e.g., `VERIFIED` vs `UNCONFIRMED`).

### 7️⃣ Multi-Format Data Export
- Exporting cleaned DataFrames to production-ready formats:
  - **CSV:** `Cleaned_Data.csv` via `.to_csv(index=False)`
  - **Excel Spreadsheet:** `excel_cleaned_data.xlsx` via `.to_excel(index=False)` utilizing `openpyxl`.

---

## 📂 Repository Structure

```text
Pandas_Data_Cleaning/
│
├── Airbnb_Dataset/
│   ├── Airbnb.csv                   # Raw, uncleaned dataset (~100k+ rows)
│   ├── Notebook.ipynb               # Step-by-step Pandas data cleaning notebook
│   ├── Cleaned_Data.csv             # Cleaned & transformed dataset (CSV output)
│   └── excel_cleaned_data.xlsx      # Cleaned dataset exported to Excel (.xlsx)
│
└── README.md                        # Project documentation & cheat sheet
```

---

## 🛠️ Quick Start

### 1. Clone the Repository
```bash
git clone https://github.com/Imhs14/Pandas_Data_Cleaning.git
cd Pandas_Data_Cleaning
```

### 2. Set Up a Virtual Environment & Install Dependencies
```bash
python3 -m venv .venv
source .venv/bin/activate   # On Windows: .venv\Scripts\activate
pip install --upgrade pip
pip install pandas openpyxl jupyter
```

### 3. Launch the Jupyter Notebook
```bash
cd Airbnb_Dataset
jupyter notebook Notebook.ipynb
```

---

## 💡 Quick Pandas Data Cleaning Cheat Sheet

Below are practical Pandas snippets demonstrated in this repository:

```python
import pandas as pd

# 1. Load data
df = pd.read_csv("Airbnb.csv", low_memory=False)

# 2. Drop unwanted columns
columns_to_drop = ['id', 'reviews per month', 'review rate number', 'license']
df = df.drop(columns=columns_to_drop)

# 3. Check and drop duplicate rows
print("Duplicate rows count:", df.duplicated().sum())
df = df.drop_duplicates()

# 4. Clean currency strings and convert to integer
df['price'] = df['price'].str.replace('$', '', regex=False)
df['price'] = pd.to_numeric(df['price'], errors='coerce')

# 5. Remove rows with critical missing values
df = df.dropna(subset=['price', 'NAME'])

# 6. Export cleaned data
df.to_csv("Cleaned_Data.csv", index=False)
df.to_excel("excel_cleaned_data.xlsx", index=False)
```

---

## 🤝 Contributing

Feel free to fork this repository, add new datasets or cleaning recipes (e.g., handling outlier detection, regex parsing, date-time feature engineering), and submit a Pull Request!
