# Power Query Steps (Beginner-Friendly, Click-by-Click)

Follow every step in order. If you want the full cleaning practice, load `Raw_Dataset_Before_Cleaning.xlsx`; otherwise load `Supply_Chain_Dataset.xlsx` directly (already clean) and skip to Step 8.

## Step 1 — Open Power BI Desktop and load the file

1. Open **Power BI Desktop**.
2. On the Home ribbon, click **Get Data → Excel workbook**.
3. Browse to and select your chosen file.
4. Click **Open**.
5. In the Navigator window, tick the checkbox next to the data sheet (**Raw_Data** or **Supply_Chain_Data**).
6. Click **Transform Data** (not "Load") to open the Power Query Editor.

## Step 2 — Remove null values

The raw file has a few blank cells in **Region** and **Incoming Stock**.

1. Click the **Region** column header.
2. Right-click → **Remove Empty**. A missing region breaks every region-based visual, so that row is dropped.
3. Click the **Incoming Stock** column header.
4. Right-click → **Replace Values** → leave "Value To Find" blank, type `0` in "Replace With" → **OK**. This keeps the row (the rest of the record is still valid) with a safe default instead of a gap.

## Step 3 — Fix inconsistent text casing

Some **Region** values came in lowercase (e.g. `west` instead of `West`).

1. Click the **Region** column header.
2. Go to **Transform → Format → Capitalize Each Word**.

## Step 4 — Trim extra whitespace

Some **Supplier Name** values have extra spaces (`"  Apex Logistics "`).

1. Click the **Supplier Name** column header.
2. Go to **Transform → Format → Trim**.

## Step 5 — Remove duplicate rows

1. Select all columns (click the top-left corner or press **Ctrl+A** in the column header area).
2. Go to **Home → Remove Rows → Remove Duplicates**. Power Query only removes a row if every column matches exactly, which correctly catches the accidental duplicate records in the raw file.

## Step 6 — Change data types

Check each column's type icon in the header and correct any that were guessed wrong:

- **Date** → Date
- **Opening Stock, Incoming Stock, Units Sold, Closing Stock, Reorder Level, Lead Time (Days), Order Quantity, Delivery Time (Days), Demand Forecast, Actual Demand** → Whole Number
- **Inventory Holding Cost** → Fixed Decimal Number
- **Forecast Accuracy %** → Percentage
- **Inventory Turnover Ratio** → Decimal Number
- **Everything else** (Product ID, Product Name, Product Category, Supplier Name, Warehouse Location, Region, Reorder Status, Delivery Status, Stockout Status, Month, Quarter) → Text

Click the type icon on the left of each column header, or use **Transform → Data Type**.

## Step 7 — Confirm/derive Month, Quarter, Year

Already included as columns in this dataset, but if you're working from a raw date-only source:

1. Click the **Date** column header.
2. **Add Column → Date → Month → Name of Month** → adds `Month`.
3. Click **Date** again → **Add Column → Date → Quarter → Quarter of Year** → adds a numeric Quarter; optionally wrap it with **Add Column → Custom Column** using `"Q" & Text.From([Quarter])` to match the "Q1" style used in this dataset.
4. Click **Date** again → **Add Column → Date → Year → Year** → adds `Year`.

## Step 8 — Standardize supplier names, locations, and categories

Real supply chain data often has the same supplier or warehouse typed inconsistently (e.g. "Apex Logistics" vs "Apex Logistics Pvt Ltd" vs "apex logistics"). To standardize:

1. Click the column (e.g. **Supplier Name**) → **Transform → Format → Capitalize Each Word** (handles casing).
2. For genuinely different spellings of the same supplier, use **Transform → Replace Values** to manually map variants to one canonical name — review the column's distinct values first via the **Column Distribution** view (**View tab → Column distribution**) to spot near-duplicates.
3. Repeat the same casing/trim/replace approach for **Warehouse Location** and **Product Category** if your own raw data has similar inconsistencies. This sample dataset's clean file already uses standardized names throughout.

## Step 9 — Rename columns and format number/currency/percentage fields

Keep names business-friendly, matching the style already used in this dataset (full words, title case — e.g. `Lead Time (Days)`, not `LT_days`). Data type (Step 6) is what matters functionally; visual-level currency/percentage formatting is applied later in Report view via the **Format** pane, or globally on the column in **Model view** (`$ English (United States)` for Inventory Holding Cost, `Percentage` for Forecast Accuracy %).

## Step 10 — Add calculated columns where needed

`Closing Stock`, `Reorder Status`, `Delivery Status`, `Stockout Status`, `Forecast Accuracy %`, and `Inventory Turnover Ratio` already exist as formula-driven columns in the Excel source. If you're rebuilding from a different raw file, add them in Power Query as custom columns, or — preferably — build them as **DAX measures** instead (see `DAX_MEASURES.md`), since measures recalculate dynamically as slicers filter the report while Power Query columns are fixed at refresh time.

## Step 11 — Close & Apply

1. Go to **Home → Close & Apply**.
2. Power BI loads the cleaned table into the data model. Move on to `DAX_MEASURES.md`.
