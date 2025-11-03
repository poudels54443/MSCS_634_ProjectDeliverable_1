# MSCS 634 – Deliverable 1 (Walmart Sales Forecasting)

**Author:** Safal Poudel  
**Course:** MSCS 634 – Advanced Big Data and Data Mining  
**Instructor:** Prof. Satish Penmatsa  

**Data Collection, Cleaning, and Exploration**

## Dataset Summary
- **Source:** Kaggle – Walmart Sales Forecasting family (e.g., competition: *Walmart Recruiting – Store Sales Forecasting*; community mirrors by various authors)
- **files:** `train.csv` (Store, Dept, Date, Weekly_Sales, IsHoliday), `features.csv` (Temperature, Fuel_Price, CPI, Unemployment, IsHoliday), `stores.csv` (Store, Type, Size)
- **Why appropriate:** ≥500 records and ≥8–10 attributes with a clear business target (`Weekly_Sales`). Numeric + categorical mix supports feature engineering, regression, classification, clustering, and association rules later.

## Major Steps
1. **Load & Unify Schema:** Read available CSVs, standardize column names, parse dates, merge `features`/`stores` into `train` by keys.
2. **Quality Audit:** Missingness table, duplicate count, basic type checks.
3. **Cleaning:**
   - Date → `datetime`; extracted `year`, `month`, `weekofyear`.
   - Numeric columns (`temperature`, `fuel_price`, `cpi`, `unemployment`, `size`) → median imputation where needed.
   - Categorical columns (`type`, `dept`, others) → mode imputation; `isholiday` normalized to 0/1.
   - Target `weekly_sales`: rows with missing target dropped.
4. **EDA (matplotlib):**
   - Histograms & boxplots for numeric features.
   - Bar charts for top categoricals.
   - Correlation heatmap for numeric fields.
   - Seasonality lines: average `weekly_sales` by month/week if `date` present.

## Key Early Insights
- Seasonality around holiday weeks is pronounced 
- Store-level attributes (`Type`, `Size`) correlate with sales 
- Macroeconomic drivers (CPI/Unemployment) may be weak short-term predictors but can improve stability when aggregated.
- Sales distributions are typically right-skewed 

## Challenges & Decisions
- **Schema variance** across different Kaggle mirrors (column names, file names) → handled via flexible renaming.
- **Missingness** in `features.csv` → median/mode imputations documented.
- **Target NaNs** → dropped.


## How to Run
```bash
python -m pip install pandas matplotlib
# Put your downloaded Kaggle CSVs into ./data/
jupyter notebook Deliverable1_Walmart.ipynb
```
