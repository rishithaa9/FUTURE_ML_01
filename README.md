

# FUTURE_ML_01 – AI‑Powered Sales Forecasting Dashboard

## Project Overview

This repository contains **Machine Learning Task 1 – AI‑Powered Sales Forecasting Dashboard**. The objective is to forecast future sales using historical transaction data and to present the results using an interactive analytics dashboard suitable for business stakeholders.
## Dataset

- **Name**: Superstore sales dataset  
- **Domain**: Retail / e‑commerce transactional data  
- **Granularity**: Individual orders with order date, region, category, sub‑category, and sales amount  
- **Key columns used**:
  - `Order Date` – date of each order  
  - `Sales` – revenue amount per order  
  - `Region`, `Category`, and other fields for drill‑down analysis  

For modeling, sales are aggregated to **daily level** and renamed to the Prophet‑compatible columns `ds` (date) and `y` (daily sales). The processed forecast output is stored in `Sales_Forecast_Output.csv` with forecast values and confidence intervals.

## Approach

1. **Data Preparation**  
   - Loaded the Superstore dataset (CSV).  
   - Converted `Order Date` to a proper datetime field and handled any invalid dates.  
   - Aggregated sales to daily level using `groupby` on date and summed `Sales`.  
   - Cleaned the series by dropping missing dates and keeping only positive sales values.

2. **Time Series Forecasting with Prophet**  
   - Reformatted the data to Prophet format:
     - `ds`: daily date  
     - `y`: total sales on that date  
   - Trained a **Prophet** model with suitable hyperparameters (e.g., `interval_width` and `changepoint_prior_scale`) to control seasonality and trend flexibility.  
   - Generated a **future dataframe** extending the historical series by additional days (e.g., 365 days) and predicted:
     - `yhat` – point forecast  
     - `yhat_lower`, `yhat_upper` – prediction interval bounds.  
   - Exported the final forecast dataset as `Sales_Forecast_Output.csv` with columns:
     - `Order Date`, `Forecast`, `Lower Bound`, `Upper Bound`.

3. **Feature Engineering for Dashboard**  
   - Joined or related the forecasted values with historical sales for the same date range.  
   - Calculated total and average sales metrics for use in KPI cards.  
   - Prepared region and category level aggregations for bar charts in the dashboard.

## Power BI Dashboard

The **Power BI dashboard** (e.g., `Reports/Task 1.pbix`) is built on the historical Superstore data and the `Sales_Forecast_Output.csv` file. It includes:

- **Sales Forecast Trend (Year‑wise)**  
  - Line chart showing forecasted sales by year/time, highlighting expected growth over the forecast horizon.

- **Sum of Forecast vs Sum of Sales**  
  - Combined line chart comparing historical **Sum of Sales** and future **Sum of Forecast**, with tooltips for specific months/quarters.  

- **KPI Cards**  
  - **Average of Sales** – average historical sales.  
  - **Total Forecast Sales** – total forecasted revenue over the prediction window.  
  - **Total Sales** – total historical revenue.  
  - **Peak Forecast Value** – maximum predicted daily/period sales value.

- **Sales by Region**  
  - Bar chart showing total sales across regions (e.g., West, East, Central, South), helping identify top‑performing geographies.

- **Average of Sales by Category**  
  - Bar chart of average sales per product category (Technology, Furniture, Office Supplies, etc.), supporting product‑mix decisions.

These visuals together form an AI‑powered sales forecasting dashboard that aligns with the official Task 1 description (forecast model + trend visualization + business breakdowns).

## Key Insights

From the model and dashboard analysis:

- Forecasted sales show an **upward trend** over the forecast horizon, indicating growth potential in the coming periods.  
- Certain **regions** (e.g., West or East) contribute a higher share of total sales compared to others, highlighting priority markets.  
- Among categories, **Technology** typically exhibits higher average sales than Furniture and Office Supplies, suggesting strong demand and higher ticket sizes.  
- The **peak forecast values** may align with specific months or seasons, indicating possible seasonal effects that can guide inventory and marketing planning.

(You can refine these bullets with precise numbers or month names from your dashboard.)

## Business Recommendations

Based on the forecast and segment analysis:

- **Plan inventory and logistics** to support the months with expected high forecasted demand, reducing stockouts and lost revenue.  
- **Prioritize high‑performing regions** with dedicated campaigns and improved service levels to capture additional market share.  
- **Invest in high‑value categories** such as Technology during forecasted peak periods with targeted promotions or bundle offers.  
- Use the forecast intervals (`Lower Bound`, `Upper Bound`) to perform **best‑/worst‑case planning** for budgeting and resource allocation.

## Repository Structure

A suggested structure for this repository:

```text
FUTURE_ML_01/
├─ Dataset/
│  ├─ Superstore.csv
│  └─ Sales_Forecast_Output.csv
├─ Notebooks/
│  └─ Salestore.ipynb
├─ Reports/
│  └─ Sales_Forecasting_Dashboard.pbix
├─ Screenshots/
│  └─ sales_dashboard_overview.png
├─ README.md
└─ Requirements.txt
```

- The notebook contains the end‑to‑end pipeline: loading data, aggregation, Prophet modeling, forecasting, and export of `Sales_Forecast_Output.csv`.  
- The Power BI file reproduces the dashboard seen in the screenshots.  
- Screenshots are used both in this README and in the LinkedIn task‑completion post.

## How to Run

1. Install dependencies:

```bash
pip install pandas numpy prophet matplotlib
```

2. Open `Notebooks/Salestore.ipynb` in Jupyter/VS Code and run all cells to:  
   - Load and aggregate Superstore data.  
   - Fit the Prophet model.  
   - Generate future forecasts and save `Sales_Forecast_Output.csv`.

3. Open **Power BI Desktop**, load the historical sales data and `Sales_Forecast_Output.csv`, and open `Reports/Sales_Forecasting_Dashboard.pbix` to view or adjust the dashboard.

***
