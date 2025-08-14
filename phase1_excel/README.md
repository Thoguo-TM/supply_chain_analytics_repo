# Phase 1 — Excel (Weeks 1–8)

This phase simulates being the **solo supply chain analyst** for a **Nairobi regional food distributor**.  
I will work entirely in Excel, focusing on **realistic messy data** and **decision-ready outputs**.

Dataset: [messy_sales_stock_2000.csv](../../data/raw/messy_sales_stock_2000.csv)

---

## Week 1 — Data intake & sanity checks
**Goal:** Get real-ish data in and make it usable for basic analysis.

**Mon**
- Create a new Excel workbook: `phase1_excel/workbooks/01_intake_and_sanity.xlsx`
- Import `messy_sales_stock_2000.csv` into a Table (Ctrl+T)
- Freeze panes; set data types (dates, numbers, text)

**Tue**
- Quick profiling: `COUNTBLANK`, `COUNTA`, distinct SKUs, unique suppliers, min/max dates
- Flag bad types / impossible values (negative prices, future dates)

**Wed**
- Build a “Data Quality Log” sheet: issue, count, sample row, fix-plan, owner, status

**Thu**
- Create a “Master Calendar” sheet: every date in range, week, month, quarter, ISO week

**Fri**
- Define named ranges for key columns (Dates, SKU, Qty, Price)

**Deliverables:**  
- `01_intake_and_sanity.xlsx` with clean Table  
- Data Quality Log sheet

**Read/Research:** Excel Tables, structured references, data types, Freeze Panes, Named Ranges

**KPIs:**  
- 100% columns with correct data type (cells failing validation allowed)  
- ≥10 concrete data issues documented with counts and samples

---

## Week 2 — Standardize & clean (no VBA)
**Goal:** One reliable “Cleaned” table you can build on.

**Mon**
- Normalize dates with `DATEVALUE`, `TEXTBEFORE/TEXTAFTER`, coercion (`--`) and helper column

**Tue**
- Trim/clean text: `TRIM`, `CLEAN`, `PROPER`, fix typos (e.g., “Supermaket”)

**Wed**
- Handle missing supplier names; standardize payment methods; unify branch codes

**Thu**
- Resolve negative/zero/huge quantities: create `valid_qty` and `txn_status` (OK/RETURN/OUTLIER)

**Fri**
- Build “Cleaned_View” with `FILTER` to include only OK transactions

**Deliverables:**  
- `02_cleaning.xlsx` with **All_Rows** and **Cleaned_View**  
- “Mapping” tab for corrections

**Read/Research:** IFERROR vs IFNA; TEXT functions; data validation lists; FILTER/UNIQUE/SORT

**KPIs:**  
- ≥95% rows with valid parsed date  
- ≤1% typos in categorical columns  
- All returns/outliers explicitly flagged

---

## Week 3 — Stock math & variance
**Goal:** Reconcile stock movements and flag stockouts.

**Mon**
- Compute `stock_variance = stock_on_hand_before - quantity_sold - stock_on_hand_after`

**Tue**
- SKU-day aggregates: `SUMIFS` qty, net sales, stockout counts

**Wed**
- Add reorder metrics: ROP breaches, days under ROP

**Thu**
- Create “SKU Health” sheet: per-SKU totals, avg daily sales, days of cover

**Fri**
- Conditional formatting for red-flag SKUs

**Deliverables:**  
- `03_stock_math.xlsx` with SKU Health and Daily SKU Aggregates

**Read/Research:** SUMIFS; absolute vs relative refs; conditional formatting formulas

**KPIs:**  
- Stock variance distribution charted  
- Top 20 problematic SKUs listed with reasons

---

## Week 4 — Supplier performance
**Goal:** Baseline supplier service levels and lead times.

**Mon**
- Build Supplier dimension: ID, Name, lead time, on-time rate

**Tue**
- Create Supplier Scorecard: fill rate proxy, avg lead time, variability

**Wed**
- Rank suppliers by risk

**Thu**
- “What to expedite” list (low cover + long lead time SKUs)

**Fri**
- Validate against Data Quality Log

**Deliverables:**  
- `04_supplier_scorecard.xlsx` with expedite list

**Read/Research:** RANK, PERCENTILE, STDEV; risk scoring

**KPIs:**  
- Supplier score matrix complete  
- Top 5 expedite candidates identified

---

## Week 5 — Pricing, margins & channel focus
**Goal:** Understand where money is made/lost.

**Mon**
- Compute gross margin per row: `(unit_price - unit_cost) * qty`, margin %

**Tue**
- Channel x County matrix: revenue, margin %, volume

**Wed**
- Analyze discount impact

**Thu**
- Build “Pocket Margin” view

**Fri**
- Short brief: “Where to push volume? Where to fix margin?”

**Deliverables:**  
- `05_margins_channels.xlsx` with Channel x County analysis  
- Notes tab with 1-page brief

**Read/Research:** PivotTables; calculated fields; % of column/row

**KPIs:**  
- Top 3 channels by revenue and by margin identified

---

## Week 6 — Forecasting prep
**Goal:** Clean demand signals and simple seasonal baseline.

**Mon**
- Date x SKU daily demand matrix from Cleaned_View

**Tue**
- 7-day and 28-day moving averages; volatility (CV)

**Wed**
- Seasonal index by weekday; monthly index

**Thu**
- Baseline forecast = 28-day MA × seasonal index

**Fri**
- Error backtest (MAPE/WAPE)

**Deliverables:**  
- `06_forecast_baseline.xlsx` with forecast per SKU and error sheet

**Read/Research:** AVERAGE; OFFSET/INDEX; MAPE/WAPE

**KPIs:**  
- Forecast for ≥90% SKUs  
- Global WAPE baseline recorded

---

## Week 7 — Replenishment mini-playbook
**Goal:** Turn forecasts into reorder advice.

**Mon**
- Compute lead-time demand and safety stock

**Tue**
- EOQ ballpark and MOQ awareness

**Wed**
- Reorder Qty recommendation per SKU

**Thu**
- Build “Buy List” table with filters

**Fri**
- Manual review of Buy List

**Deliverables:**  
- `07_replenishment.xlsx` with Buy List

**Read/Research:** Safety stock; EOQ; z-scores

**KPIs:**  
- Buy List covers ≥80% SKUs with clear quantities

---

## Week 8 — Executive snapshot & SOPs
**Goal:** One-click Excel dashboard + documented process.

**Mon**
- Build Pivot-driven dashboard: revenue, margin, stockouts, supplier OTIF, forecast error

**Tue**
- Add slicers & timelines

**Wed**
- Record “Refresh SOP” checklist inside workbook

**Thu**
- Stress test with fresh dataset copy

**Fri**
- Exec Summary tab with next-week decisions

**Deliverables:**  
- `08_excel_dashboard.xlsx` with embedded SOPs

**Read/Research:** Slicers; Pivot charts; documentation best practices

**KPIs:**  
- Dashboard refresh <30s; slicers instant  
- Exec Summary lists 5 next-week decisions

---

<!--
# Phase 1 – Excel Foundations (Weeks 1–8)

**Goal:** Master Excel for supply chain analytics, from basics to advanced functions, building real-world portfolio projects.

---

## Week 1: Excel Basics + Understanding SCM Data
**Day 1:** Install Excel / LibreOffice, open Week1 datasets, explore layout.  
**Day 2:** Learn cell types, data entry rules, fix data formats.  
**Day 3:** Practice navigation, freezing panes, filtering.  
**Day 4:** Format SCM tables (currency, dates, %, text wrap).  
**Day 5:** Conditional formatting for stock levels (low stock red).  
**Day 6:** Shortcuts + efficiency tricks.  
**Day 7:** Mini-project: Clean & format Week1 datasets for reporting.

## Week 2: Basic Formulas
**Day 8:** SUM, AVERAGE, MIN, MAX — calculate daily sales.  
**Day 9:** COUNT, COUNTA, COUNTIF — count product SKUs sold.  
**Day 10:** ROUND, ROUNDUP, ROUNDDOWN — clean unit price formatting.  
**Day 11:** CONCAT/CONCATENATE, TEXTJOIN — create SKU labels.  
**Day 12:** Practice formulas on messy SCM dataset.  
**Day 13:** Create simple dashboard using only Excel formulas.  
**Day 14:** Mini-project: Sales Summary workbook.

## Week 3: Lookup & Reference
**Day 15:** VLOOKUP to match sales with inventory.  
**Day 16:** HLOOKUP on supplier data.  
**Day 17:** INDEX & MATCH for flexible lookups.  
**Day 18:** XLOOKUP for modern Excel workflows.  
**Day 19:** Absolute vs relative references — why stock updates break.  
**Day 20:** Create “Stock Update” formula linking sales to inventory.  
**Day 21:** Mini-project: Automated stock tracker.

## Week 4: Logical Functions
**Day 22:** IF statements — flagging restock items.  
**Day 23:** Nested IF — tiered pricing logic.  
**Day 24:** AND, OR — combined logic for supplier reliability.  
**Day 25:** IFERROR — handle missing SKU lookups.  
**Day 26:** Practice on supplier compliance dataset.  
**Day 27:** Conditional restock recommendation tool.  
**Day 28:** Mini-project: Restock decision sheet.

## Week 5: Date & Text Functions
**Day 29:** TODAY, NOW, DAY, MONTH, YEAR — date-based reporting.  
**Day 30:** NETWORKDAYS for lead time calculations.  
**Day 31:** TEXT for formatting order IDs.  
**Day 32:** LEFT, RIGHT, MID for SKU parsing.  
**Day 33:** TRIM, CLEAN — remove messy data artifacts.  
**Day 34:** Practice on historical orders dataset.  
**Day 35:** Mini-project: Lead time analysis sheet.

## Week 6: Pivot Tables
**Day 36:** Create first pivot table on sales data.  
**Day 37:** Group by dates and product categories.  
**Day 38:** Add calculated fields.  
**Day 39:** Filter by supplier region.  
**Day 40:** Combine pivot tables with slicers.  
**Day 41:** Build pivot chart dashboard.  
**Day 42:** Mini-project: Multi-sheet pivot dashboard.

## Week 7: Advanced Excel Features
**Day 43:** Data validation for clean input.  
**Day 44:** Named ranges in formulas.  
**Day 45:** What-If Analysis — Scenario Manager.  
**Day 46:** Goal Seek for cost optimization.  
**Day 47:** Solver add-in for inventory optimization.  
**Day 48:** Practice advanced tools on replenishment dataset.  
**Day 49:** Mini-project: Inventory optimization model.

## Week 8: Phase Project
**Day 50–56:**  
**Project:** Build a fully automated Excel dashboard for a fictional retailer:  
- Auto-updating stock  
- Restock alerts  
- Monthly sales & profit charts  
- Supplier performance report


-->
