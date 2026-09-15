# Retail Sales Performance Dashboard

A Power BI dashboard analyzing retail sales performance across regions, product categories, and time, built as a beginner end-to-end project (data import → cleaning → modeling → DAX → visualization).

## Dataset

**File:** `Retail_Sales_Dataset.xlsx` (sheet: `Sales Data`)
**Rows:** 1,500 orders | **Date range:** Jan 1, 2023 – Dec 31, 2024

| Column | Description |
|---|---|
| Order ID | Unique order identifier |
| Order Date / Ship Date | Order and shipment dates |
| Ship Mode | Shipping method used |
| Customer Name | Customer placing the order |
| Region / State | Geographic location of the order |
| Category / Sub-Category | Product classification (5 categories, 25 sub-categories) |
| Product Name | Specific product ordered |
| Quantity | Units sold |
| Unit Price | Price per unit |
| Discount | Discount applied |
| Sales | Total sale amount |
| Profit | Profit earned on the order |

## Measures Built

- **Total Sales** = `SUM('Sales Data'[Sales])`
- **Total Profit** = `SUM('Sales Data'[Profit])`
- **Profit Margin %** = `DIVIDE([Total Profit], [Total Sales])`
- **Total Orders** = `DISTINCTCOUNT('Sales Data'[Order ID])`
- **Average Order Value** = `DIVIDE([Total Sales], [Total Orders])`
- **Order Value Tier** (calculated column) = `IF('Sales Data'[Sales] > <threshold>, "High Value", "Low Value")`

A dedicated `DateTable` (built with `CALENDAR()`) supplies Year, Month, MonthName, and Quarter columns and drives all time-based filtering and trend charts.

## Key Insights

1. **Electronics is the profit engine.** Electronics leads all categories with ~₹3.58 Cr in sales and ~₹58 lakh in profit — nearly 37% of total profit — followed closely by Home Appliances (~₹3.18 Cr sales, ~₹48 lakh profit). Together these two categories generate over 68% of total profit despite representing well under half the order volume.
2. **South and Central regions drive the most profit**, despite not having the highest sales. Central region leads in profit (~₹35.5 lakh) even though South edges it out slightly in raw sales (~₹2.22 Cr vs ~₹2.09 Cr) — suggesting Central orders carry a better margin, while East trails on both sales and profit.
3. **Clothing and Office Supplies underperform on margin.** These two categories combined make up only ~7.7% of total sales and ~7.8% of total profit, with sub-categories like Women's Wear and Footwear among the lowest per-order value in the dataset — signaling limited upside from these lines without a pricing or bundling change.

*Overall: ₹9.95 Cr in total sales, ₹1.56 Cr in profit (~15.7% margin) across 1,500 orders, averaging ~₹66,366 per order.*

## Dashboard Pages

- **Main Report:** KPI cards (Total Sales, Total Profit, Total Orders) → Sales by Category (bar) & Sales Trend Over Time (line) → Sales by State (map) & Region × Category breakdown (matrix)
- **Product Tooltip:** Hover detail showing Sales/Profit at the Product Name level
- Slicers for Order Date, Region, and Category throughout

## Walkthrough Outline (3–5 min)

1. **(30s) Setup** — What the dataset covers and the business question: where are we making money, and where aren't we?
2. **(1 min) Headline numbers** — Total Sales, Profit, Margin, Orders from the KPI row.
3. **(1.5 min) Category & region story** — Electronics/Home Appliances as profit drivers; Central/South as top regions; Clothing/Office Supplies as laggards.
4. **(1 min) Trend & geography** — Point out any seasonal spikes in the line chart and the state-level hot spots on the map.
5. **(30s) Recommendation** — One suggestion this data supports (e.g., double down on Electronics inventory in Central/South, reassess pricing on low-margin Clothing sub-categories).

## Tools Used

Power BI Desktop — Power Query (cleaning), Data Modeling (star schema with Date table), DAX (measures & calculated column), and interactive visuals (cards, bar, line, map, matrix, slicers).
