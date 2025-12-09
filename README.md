# Exploratory Data Analysis using Time Series

This repository contains a complete product-level sales analysis, including data validation, margin-based strategic segmentation, trend detection, price-change impact analysis, and forecasting using time-series models. The analysis integrates sales with inventory, costs, trends, and forecasted demand to support data-driven decision making.

---

## Project Overview

### **1. Data validation and cleaning**
- Check for products in sales data that do not exist in inventory.
- Validate consistency between units sold × unit price and total sales.
- Detect and report missing values per column.
- Identify days without sales and fill them using interpolation when appropriate.

---

### **2. General behavior analysis**
- Explore date ranges and dataset coverage.
- Identify monthly trends and possible seasonality.
- Combine sales with unit costs for margin calculations.

---

### **3. Brand, category, and product behavior**
- Compute brand-level properties and distributions.
- Analyze strategic category distribution.
- Perform detailed product-level evaluation:
  - Margins
  - Trends (growing, declining, stable, insufficient data)
  - Loss-generating products

---

### **4. Margin-based strategic product grouping**

Products are segmented into five groups based on cumulative margin contribution:

| Group | Description |
|-------|-------------|
| **1. High-value** | Top ~50% of total margin |
| **2. Medium-value** | Next 25% (cumulative 75%) |
| **3. Low-contribution** | Next 15% (cumulative 90%) |
| **4. Marginal** | Next 5% (cumulative 95%) |
| **5. Residual** | Final 5% of accumulated margin |

Additionally, products with **negative margin** are identified.

---

### **5. Price-change impact analysis**

Each product is classified according to its sales response to price variations:

- Sold more products when the price increased  
- Sold fewer products when the price increased  
- Sold fewer products when the price decreased  
- No change in product sales  

Visualizations show the distribution of effects across products.

---

### **6. Sales forecasting**

Because many products show extended periods with zero daily sales, sales are aggregated **weekly**.

Forecasts are generated for:
- **1 week**
- **1 bi-week (15 days)**
- **1 month**

Three forecasting approaches were used:

| Condition | Model |
|----------|--------|
| More than 6 data points and fewer than 40% zeros | **Prophet** |
| More than 6 data points and more than 40% zeros | **Croston** |
| 6 or fewer data points | **Simple average** |

Evaluation metrics:
- **MAE**
- **RMSE**

_Remember: forecasts are computed for weekly sales, not daily sales._

---

### **7. Final dataset integration**

A final dataframe is created combining:

- Forecast results
- Evaluation metrics
- Selected model
- Product trend
- Margin-based strategic group
- Price-change effect
- Current inventory
- Stock sufficiency indicator (`sufficient`, `insufficient`)

The results are exported as a CSV file.

---

## Project Structure

```
project/
│
├── data/                 # Input data (kept via .gitkeep)
├── output/               # Exported results (kept via .gitkeep)
├── scripts/
    │
    ├── Sales_Analysis.ipynb # Main analysis notebook
└── README.md
```
