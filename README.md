Inventory Forecasting & Reorder-Point Dashboard

A Power BI dashboard that models demand forecasting and reorder-point logic across a 30-SKU retail catalog — flagging which products need to be reordered before they run out, based on demand volatility and supplier lead time rather than gut feel.
What it does
Star-schema data model — a Demand fact table (2 years of weekly sales, 3,120 rows) related to a SKU_Master dimension table (cost, price, supplier, lead time, current stock) on SKU_ID.
Trailing demand statistics — DAX measures calculate each SKU's average weekly demand and demand volatility (standard deviation) over the most recent 12 weeks, so replenishment decisions reflect current behavior, not two-year-old averages.
Reorder-point model — implements the standard inventory formula used in real supply-chain planning:
  Safety Stock   = Z × Demand Std Dev × √(Lead Time in weeks)
  Reorder Point  = (Avg Weekly Demand × Lead Time in weeks) + Safety Stock

where Z = 1.65, corresponding to a 95% service level.

Automatic reorder flagging — every SKU is compared against its own reorder point and flagged "Reorder Now" or "OK," conditionally color-coded red/green in the report.
12-week demand forecast — a per-product trend chart with Power BI's built-in forecasting engine (52-week seasonality), so you can see projected demand and a confidence interval, not just history.
Category-level inventory value breakdown — a sorted bar chart showing which product categories tie up the most working capital.
Result

Across 30 SKUs and $105K in tracked inventory value, the model flags 6 SKUs currently below their reorder point — each one identifiable before it becomes a stockout, using only sales history and lead time data.

Tools

Power BI Desktop (Power Query, data modeling, DAX measures), Excel (source data prep).

About the data

The dataset (Inventory_Forecasting_Data.xlsx) is synthetic — built to mirror realistic retail replenishment patterns (trend, seasonality, promotional spikes, demand noise) across 5 categories and 30 SKUs, so the forecasting and reorder-point logic could be demonstrated end-to-end without proprietary company data. The two tables (Demand, SKU_Master) are structured as a fact/dimension pair, matching how this kind of data is modeled in production BI tools.

Files
File	Description
Inventory_Forecasting_Dashboard.pbix	The Power BI report — data model, DAX measures, and all visuals
Inventory_Forecasting_Data.xlsx	Source data (Demand + SKU_Master tables)
dashboard_screenshot.png	Static preview of the finished dashboard
Author

Mohamed Seddik Nakbi linkedin.com/in/mohamed-seddik-nakbi-74640035b
