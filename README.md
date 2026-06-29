# Business Dashboard Design

Data Analyst Internship | Task 4

## Project Overview
This project delivers an interactive, executive-ready Power BI dashboard and presentation summary analyzing **559K vehicle sales transactions** from US car auction records across 2014–2015[cite: 2]. The primary objective is to equip business stakeholders with actionable, data-backed insights regarding revenue metrics, marketplace volume velocity, temporal trends, and regional marketplace performance to drive inventory optimization and strategic pricing initiatives.

---

## Key Business Insights & Takeaways

* **The Margin Disconnect (Strategic Risk):** While top-line gross revenue reached an impressive **\$8 Billion**, individual assets sold at an average loss of **-\$158.02 per vehicle** relative to their wholesale Manheim Market Report (MMR) benchmark. This systemic underpricing led to a net negative market margin of **-\$88 Million**. 

* **Extreme Seasonality:** Sales volume heavily peaks in **February** (~ \$2.3B) followed by a sharp drop-off into **April**. 

* **Core Geographic & Segment Engines:** **Florida (FL)** and **California (CA)** act as primary market engines, contributing over **30%** of total transaction volume. From a product standpoint, **SUVs and Sedans** dominate consumer preference, representing more than **55%** of all vehicles sold.

---

## Technical Workflow & Performance Optimization - in Power BI.

* **Data ETL & Hard Reduction (Power Query):** To ensure optimal data modeling efficiency, highly granular, non-aggregate columns with extreme cardinality (such as individual VIN numbers, detailed trim tiers, transmission, odometer, condition and unique seller text fields) were dropped prior to model ingestion. This directly optimized memory footprint and enhanced reporting cross-filter speeds.
* **Chronological Sorting Alignment:** Resolved standard Power BI alphabetical sorting limitations by creating an explicit `Month Number` mapping key in the backend data source, forcing the analytical time-series charts to render correctly from January to December.
* **DAX Measure Engineering:** Built highly lightweight, explicit calculated measures for all critical organizational indicators (`Total Sales`, `Total Units`, `Avg Sale Price`, and `Avg Profit per Car`) rather than relying on heavy calculated rows.
* **Sale Year vs. Manufacture Year Disambiguation:** The dataset contained two distinct year dimensions — `year` (vehicle manufacture year, ranging 1982–2015) and a derived `SaleYear` (extracted from `saledate`, limited to 2014–2015). These were explicitly separated to ensure the Year of Sale slicer filtered by transaction date rather than vehicle age, preventing misleading cross-filter behaviour across all visuals.
* **DAX Calculated Column for Body Grouping:** A DAX `IF/IN` calculated column (`body_grouped`) was introduced to consolidate low-frequency body types into an "Other" category, reducing donut chart visual noise from 9+ slices to 5 meaningful segments without distorting manufacturer-level filter interactions.