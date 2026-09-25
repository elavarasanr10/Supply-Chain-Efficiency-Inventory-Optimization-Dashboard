# DAX Measures

Create each of these under **Home → New Measure** (with `Supply_Chain_Data` selected in the Fields pane). Put them all into a dedicated `_Measures` table for a clean model: **Modeling → New Table**, type `_Measures = {}`, then move each measure into it via its properties pane.

## Core inventory measures

**Total Opening Stock**
```
Total Opening Stock = SUM('Supply_Chain_Data'[Opening Stock])
```

**Total Incoming Stock**
```
Total Incoming Stock = SUM('Supply_Chain_Data'[Incoming Stock])
```

**Total Units Sold**
```
Total Units Sold = SUM('Supply_Chain_Data'[Units Sold])
```

**Total Closing Stock**
```
Total Closing Stock = SUM('Supply_Chain_Data'[Closing Stock])
```
This is your **Total Inventory** KPI — the stock currently on hand across the filtered context.

## Risk and reorder measures

**Stockout Count**
```
Stockout Count = CALCULATE(COUNTROWS('Supply_Chain_Data'), 'Supply_Chain_Data'[Stockout Status] = "Yes")
```
Counts how many records hit zero or negative closing stock — the clearest sign something needs fixing right now.

**Reorder Count**
```
Reorder Count = CALCULATE(COUNTROWS('Supply_Chain_Data'), 'Supply_Chain_Data'[Reorder Status] = "Reorder Needed")
```
Counts records currently at or below their reorder level — these are the SKUs that need a purchase order soon, before they become stockouts.

## Delivery and forecast measures

**Average Lead Time**
```
Average Lead Time = AVERAGE('Supply_Chain_Data'[Lead Time (Days)])
```

**On-Time Delivery %**
```
On-Time Delivery % =
DIVIDE(
    CALCULATE(COUNTROWS('Supply_Chain_Data'), 'Supply_Chain_Data'[Delivery Status] = "On Time"),
    COUNTROWS('Supply_Chain_Data'),
    0
)
```
`DIVIDE` avoids errors when a filtered slice has zero records.

**Forecast Accuracy %**
```
Forecast Accuracy % = AVERAGE('Supply_Chain_Data'[Forecast Accuracy %])
```
Averages the row-level Forecast Accuracy % (already calculated in the Excel source) across the current filter context.

**Inventory Holding Cost**
```
Inventory Holding Cost = SUM('Supply_Chain_Data'[Inventory Holding Cost])
```

**Inventory Turnover Ratio**
```
Inventory Turnover Ratio =
DIVIDE(
    [Total Units Sold],
    DIVIDE([Total Opening Stock] + [Total Closing Stock], 2),
    0
)
```
Recomputed at the measure level (rather than just averaging the row-level ratio) so it stays mathematically correct when aggregated across many SKUs and periods — a higher ratio means inventory is moving efficiently, a lower one suggests overstocking.

## Breakdown measures

**Category-wise Inventory Performance**
```
Category-wise Inventory Performance = CALCULATE([Inventory Turnover Ratio], ALLEXCEPT('Supply_Chain_Data', 'Supply_Chain_Data'[Product Category]))
```
Forces turnover to always break down by Product Category regardless of other active slicers — powers the "best performing product category" insight.

**Supplier-wise Delivery Performance**
```
Supplier-wise Delivery Performance = CALCULATE([On-Time Delivery %], ALLEXCEPT('Supply_Chain_Data', 'Supply_Chain_Data'[Supplier Name]))
```
Same pattern applied to Supplier Name — powers the supplier delivery performance bar chart and the "best performing supplier" insight.

## Helper measures for KPI cards and insights

**Best Performing Supplier**
```
Best Performing Supplier =
VAR RankedSuppliers =
    TOPN(1, VALUES('Supply_Chain_Data'[Supplier Name]), CALCULATE([On-Time Delivery %]), DESC)
RETURN
    CONCATENATEX(RankedSuppliers, 'Supply_Chain_Data'[Supplier Name])
```

**Best Performing Product Category**
```
Best Performing Product Category =
VAR RankedCategories =
    TOPN(1, VALUES('Supply_Chain_Data'[Product Category]), CALCULATE([Inventory Turnover Ratio]), DESC)
RETURN
    CONCATENATEX(RankedCategories, 'Supply_Chain_Data'[Product Category])
```
Ranked by turnover ratio, since that's the metric that actually reflects inventory efficiency, not just sales volume.
