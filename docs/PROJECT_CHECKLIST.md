# GitHub Setup and Final Checklist

## Repository name and description

**Repository name:** `supply-chain-inventory-optimization-dashboard`

**One-line description:** Power BI dashboard monitoring inventory levels, supplier delivery performance, and demand forecast accuracy across products, categories, and warehouses.

## GitHub upload steps (beginner-friendly)

1. Go to **github.com** and create a free account if you don't already have one.
2. Click the **+** icon in the top-right corner → **New repository**.
3. In **Repository name**, type `supply-chain-inventory-optimization-dashboard`.
4. In **Description**, paste the one-line description above.
5. Select **Public**.
6. Leave "Add a README file" unchecked if you're uploading the one already prepared in this project; check it only if you plan to write your own from scratch.
7. Click **Create repository**.
8. On the new repository's page, click **Add file → Upload files**.
9. Drag and drop: `README.md`, `Supply_Chain_Dataset.xlsx`, `Raw_Dataset_Before_Cleaning.xlsx`, the entire `docs` folder, the `screenshots` folder (once you have images), and your `.pbix` file once it's built.
10. Scroll down, type a commit message such as "Initial commit: Supply Chain Efficiency & Inventory Optimization Dashboard".
11. Click **Commit changes**.

## Files to upload to GitHub

- [ ] `Supply-Chain-Efficiency-Inventory-Optimization-Dashboard.pbix` (save from Power BI Desktop after building — File → Save As)
- [ ] `Supply_Chain_Dataset.xlsx` (clean dataset — already included)
- [ ] `Raw_Dataset_Before_Cleaning.xlsx` (optional but shows you can clean real data — already included)
- [ ] `README.md` (already included)
- [ ] `docs/` folder — Power Query steps, DAX measures, report build guide, project overview, resume/LinkedIn content (already included)
- [ ] Dashboard screenshots (create/populate the `screenshots/` folder after building)
- [ ] Optional: PDF export of the dashboard (**File → Export → Export to PDF** in Power BI Desktop)
- [ ] Optional: a one-page project summary for recruiters who won't open the full README

## Adding screenshots to the README

1. In Power BI Desktop, once your dashboard looks finished, go to **File → Export → Export to Image**, or use a screenshot tool.
2. Save your images into the `screenshots` folder (already included, empty, in this zip) with clear names, e.g. `01-full-dashboard.png`.
3. Upload that folder to GitHub the same way as everything else.
4. In `README.md`, reference an image with Markdown syntax:
   `![Dashboard Overview](screenshots/01-full-dashboard.png)`
5. This renders the actual image directly on your repo's front page.

## Final checklist before publishing

- [ ] Dataset loads cleanly into Power BI with no Power Query errors
- [ ] All DAX measures return correct, non-error values (spot-check against the `KPI_Summary` sheet in the Excel file)
- [ ] Every visual has a clear title and correctly formatted currency/percentage values
- [ ] All five slicers (Region, Supplier, Category, Warehouse, Month) are tested — filtering by each one updates every visual correctly
- [ ] Dashboard is visually consistent — one font, one color theme, aligned and evenly spaced visuals
- [ ] README.md is complete and every link to a file in `docs/` works
- [ ] Screenshots are uploaded and displaying correctly on the GitHub repo page
- [ ] Repository visibility is set to **Public**
- [ ] LinkedIn post drafted, with the GitHub link ready to paste into the first comment
