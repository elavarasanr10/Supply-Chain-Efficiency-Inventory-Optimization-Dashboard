# Supply Chain Efficiency & Inventory Optimization Dashboard

A Power BI dashboard that monitors inventory levels, delivery performance, and demand forecast accuracy across products, suppliers, and warehouses — built to mirror how a supply chain analyst, inventory planner, or operations team keeps stock, cost, and service levels under control.

## Objective

Build an interactive Power BI dashboard to monitor supply chain KPIs (inventory turnover, stockouts, on-time delivery, lead time, forecast accuracy) and identify optimization opportunities per SKU. Specifically, to answer:
1. Which products are at risk of stockout, and which already have?
2. Which suppliers are reliably on time, and which are dragging down delivery performance?
3. Is actual demand tracking the forecast, or are we consistently over/under-forecasting?
4. Which categories and warehouses turn inventory efficiently vs. sit on excess stock?

## Industry Relevance

Manufacturing, retail, and e-commerce teams rely on near-real-time visibility into inventory, demand, and fulfillment to lower working capital, prevent stockouts, and improve service levels. This project gives an interview-ready, end-to-end supply chain analytics solution built entirely in tools already on a business analyst's desk.

## Tools Used

- **Power BI Desktop** — data modeling, DAX, dashboard build
- **Power Query** — data cleaning and transformation
- **Microsoft Excel** — source dataset
- **DAX (Data Analysis Expressions)** — KPI and measure logic
- **GitHub** — version control and portfolio hosting

## Dataset Description

`Supply_Chain_Dataset.xlsx` contains 150 transaction-level rows (Jan 2024 – Dec 2025) with 26 columns:

| Column | Description |
|---|---|
| Date | Transaction/record date |
| Month | Month name, derived from Date |
| Quarter | Q1–Q4, derived from Date |
| Year | Calendar year |
| Product ID | SKU identifier |
| Product Name | Specific product |
| Product Category | Electronics, Home Appliances, Furniture, Apparel, FMCG |
| Supplier Name | Supplier fulfilling this order |
| Warehouse Location | Warehouse holding the stock |
| Region | Region the warehouse serves |
| Opening Stock | Stock on hand at period start |
| Incoming Stock | Stock received during the period |
| Units Sold | Units sold/shipped out during the period |
| Closing Stock | Opening Stock + Incoming Stock − Units Sold |
| Reorder Level | Stock threshold that should trigger a reorder |
| Reorder Status | "Reorder Needed" if Closing Stock ≤ Reorder Level, else "Sufficient" |
| Lead Time (Days) | Supplier's quoted lead time |
| Order Quantity | Quantity ordered from the supplier |
| Delivery Status | "Delayed" if Delivery Time > Lead Time, else "On Time" |
| Delivery Time (Days) | Actual days taken for delivery |
| Inventory Holding Cost | Cost of holding this stock for the period |
| Stockout Status | "Yes" if Closing Stock ≤ 0, else "No" |
| Demand Forecast | Forecasted demand for the period |
| Actual Demand | Demand that actually materialized |
| Forecast Accuracy % | 1 − ABS(Forecast − Actual) ÷ Actual |
| Inventory Turnover Ratio | Units Sold ÷ Average Inventory (Opening + Closing) ÷ 2 |

`Closing Stock`, `Reorder Status`, `Delivery Status`, `Stockout Status`, `Forecast Accuracy %`, and `Inventory Turnover Ratio` are all live Excel formulas, not hardcoded — open the file and click any of those cells to see exactly how each was derived.

A second file, `Raw_Dataset_Before_Cleaning.xlsx`, is the same data before cleanup — it deliberately contains null values, inconsistent text casing, extra whitespace, and duplicate rows for the Power Query cleaning walkthrough.

## Power Query Steps

See [`docs/POWER_QUERY_STEPS.md`](docs/POWER_QUERY_STEPS.md) for the full click-by-click walkthrough. Summary: remove nulls, fix casing, trim whitespace, remove duplicates, correct data types, confirm/derive Month, Quarter, Year, standardize supplier/warehouse/category text, and format currency/percentage fields.

## DAX Measures

See [`docs/DAX_MEASURES.md`](docs/DAX_MEASURES.md) for every measure with its formula and a plain-language explanation. Includes: Total Opening Stock, Total Incoming Stock, Total Units Sold, Total Closing Stock, Stockout Count, Reorder Count, Average Lead Time, On-Time Delivery %, Forecast Accuracy %, Inventory Holding Cost, Inventory Turnover Ratio, Category-wise Inventory Performance, Supplier-wise Delivery Performance.

## Dashboard Features

- **KPI cards:** Total Inventory, Stockout Count, On-Time Delivery %, Forecast Accuracy %, Inventory Turnover
- **Column chart:** Inventory by Product Category
- **Bar chart:** Supplier Delivery Performance
- **Line chart:** Monthly Units Sold / Inventory Trend
- **Donut chart:** Delivery Status distribution
- **Clustered column chart:** Demand Forecast vs. Actual Demand
- **Matrix table:** Product × Stock × Reorder Level × Lead Time × Delivery Status
- **Slicers:** Region, Supplier, Category, Warehouse, Month
- **Corporate color theme:** blue for neutral metrics, green for efficiency/on-time, orange/red for delays and stockouts

## Key Insights

*(Fill in with your actual numbers once you build the dashboard — sample structure below)*

- Which products currently show "Reorder Needed" or have already recorded a stockout
- Which suppliers have the worst on-time delivery rate, and by how much they typically miss
- Which warehouses/regions carry excess inventory (low turnover) vs. run lean (high turnover)
- Whether forecast accuracy is stronger for some categories than others
- The gap between Demand Forecast and Actual Demand — consistently over- or under-forecasting?
- Which category has the best inventory turnover ratio, and what that implies for reorder policy

## Screenshots

Add dashboard screenshots here after building in Power BI Desktop:

```
screenshots/
  01-full-dashboard.png
  02-kpi-cards.png
  03-inventory-by-category.png
  04-supplier-delivery-performance.png
  05-forecast-vs-actual.png
```

`![Dashboard Overview](screenshots/01-full-dashboard.png)`

## Repository Structure

```
supply-chain-inventory-optimization-dashboard/
├── README.md
├── Supply_Chain_Dataset.xlsx
├── Raw_Dataset_Before_Cleaning.xlsx
├── Supply-Chain-Efficiency-Inventory-Optimization-Dashboard.pbix   (add after building in Power BI Desktop)
├── docs/
│   ├── POWER_QUERY_STEPS.md
│   ├── DAX_MEASURES.md
│   ├── REPORT_BUILD_GUIDE.md
│   ├── PROJECT_OVERVIEW.md
│   ├── RESUME_DESCRIPTIONS.md
│   ├── LINKEDIN_CONTENT.md
│   └── PROJECT_CHECKLIST.md
└── screenshots/
    └── (dashboard images go here)
```

## Conclusion

This project demonstrates a full supply chain analytics workflow: messy raw data → cleaned and modeled data → DAX-driven inventory/delivery KPIs → a decision-ready dashboard. It reflects the kind of monitoring tool used by supply chain analysts, inventory planners, and operations managers to prevent stockouts, hold suppliers accountable, and control inventory cost.
