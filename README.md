# 📊 BPS Labour Force – August Time Series Analysis (2010–2024)

This project is inspired by a Tableau course exercise on **unemployment time-series visualisation**, adapted to the Indonesian context.  
Instead of using U.S. Bureau of Labor Statistics data, here we process and visualise the **Badan Pusat Statistik (BPS) Labour Force August releases** from **2010–2024**.  

The goal is to create a structured, reproducible pipeline that cleans BPS raw CSVs and prepares them for **time-series analysis and visualisation**. With the cleaned data, we can replicate charts such as:

- 📈 Unemployment trends by **age group**  
- ⚖️ Gender disparities in unemployment  
- 🔎 Focused view on **25–34 year olds**, often most sensitive to labour market shocks  
- 📉 Time-series highlighting major events (e.g., Global Financial Crisis 2008, COVID-19 impact)  

🛠️ **Status**: cleaning completed, visualisation in progress  
🔒 **Repo**: Private  

---

## 📌 Project Goals

- **Reproduce a Tableau-style unemployment time series by age group** using Indonesian BPS data  
- Build a **data cleaning pipeline** to handle BPS CSV quirks: header rows, unnamed columns, totals  
- Standardise column names and convert values to numeric for time-series analysis  
- Split into **detail datasets** (age group breakdowns) and **total datasets** (aggregated)  
- Export cleaned tables for further use in **Python, R, or Tableau**  
- Enable visualisation of **unemployment trends by age** across 2010–2024  
---

## 🗂️ Project Structure

- [README.md](README.md) – Project overview and documentation  
- [notebooks/](notebooks/) – Jupyter Notebooks for cleaning & transformation  
  - `01_data_cleaning.ipynb` – Loop-based cleaning (2010–2024)  
  - `02_total_extraction.ipynb` – Extraction of yearly totals  
- [Data/](Data/) – Datasets  
  - `Raw/` – Original BPS CSVs (excluded from repo)  
  - `Cleaned/` – Timestamped cleaned exports  
    - `bps_all_detail_2010_2024_<timestamp>.csv`  
    - `bps_total_detail_2010_2024_<timestamp>.csv`  
- [.gitignore](.gitignore) – Ensures raw data and large files are not committed  


--- 

### 🗂️ Folder Tree

```
root/
├── README.md
├── .gitignore
├── Data/
│ ├── Raw/ (excluded)
│ └── Cleaned/
│ ├── bps_all_detail_2010_2024_<timestamp>.csv
│ └── bps_total_detail_2010_2024_<timestamp>.csv
├── notebooks/
│ ├── 01_data_cleaning.ipynb
│ └── 02_total_extraction.ipynb
```
---


---

## 📊 Dataset Overview

- Source: Badan Pusat Statistik (BPS) – Labour Force August releases  
- Coverage: **2010–2024**  
- Observations: population aged 15+ segmented by age groups  
- Format: CSV, annual (August release)  

---

## 🧹 Cleaning & Processing Summary

- Dropped **top 3 header rows** in each CSV  
- Dropped redundant `"Unnamed: 3"` column  
- Renamed:  
  - `"Unnamed: 1"` → `February`  
  - `"Unnamed: 2"` → `August`  
  - `"year"` → `Year`  
- Converted `February` and `August` to numeric (`Int64`), stripped symbols/commas  
- Computed `Yearly_sum = February + August`  
- Split rows into:  
  - **Detail**: all age groups except `"Total"`  
  - **Total**: `"Total"` only (one row per year)  
- Concatenated buckets into two master DataFrames → exported as CSV  

---

## ✨ Outputs

- ✅ `bps_all_detail_2010_2024_<timestamp>.csv`  
  - Age group breakdowns (no “Total”)  
  - Columns: `Age Group, February, August, Year, Yearly_sum`  

- ✅ `bps_total_detail_2010_2024_<timestamp>.csv`  
  - Yearly totals only  
  - Columns: `Year, February, August`  

---

## 🛡️ Disclaimer

- This project uses **publicly available BPS data** from official August Labour Force releases.  
- Original raw CSVs are excluded from the repository due to licensing and storage.  
- Cleaning procedures (dropping rows, renaming, numeric conversion) are documented in notebooks.  