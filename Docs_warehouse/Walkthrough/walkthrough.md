# Fabric Data Warehouse Walkthrough

This walkthrough shows exactly how the warehouse was built in Microsoft Fabric, where each SQL step fits, and where to place screenshots so anyone can reproduce the same result in Fabric Studio without guesswork.  

---

## How to use this file

- Open a Fabric workspace with Trial, Premium, or Fabric capacity and a new Warehouse item, then follow each step below in order, running the matching SQL files from your [SQL folder](../SQL/).  


Suggested image names:
- workspace-created.png, warehouse-provisioned.png, dimproduct-created.png, tables-after-load.png, query-year-month.png, query-year-month-region.png, view-created.png, visual-query-merge.png, visual-query-expand-productname.png, visual-query-filter-cable-lock.png, semantic-model.png[attached_file:1].  

---

## 1) Create a workspace

- Go to app.fabric.microsoft.com, sign in, and create a new workspace with Fabric capacity enabled, which ensures all Fabric items are available in this project ![New Workspace](/Image_warehouse/new-workspace.png)

---

## 2) Create a data warehouse

- In the workspace, select Create → Warehouse and give it a unique name, then wait for provisioning to complete so the Warehouse opens with the Explorer pane visible on the left. 


![Warehouse provisioned](/Image_warehouse/ready-data-warehouse.png)

---

## 3) Create DimProduct and seed rows

- In the Warehouse, open the T‑SQL editor and run your 01_create_dimproduct.sql file to create dbo.DimProduct with the expected columns and data types

- Next, run 02_insert_dimproduct.sql to insert three sample rows and then refresh the Explorer to confirm the table and row count are visible under dbo.Tables  


![DimProduct created](/Image_warehouse/dimproduct-created.png)

---

## 4) Load the core schema and data

- Create a new query and paste the MicrosoftLearning schema script that you can find it in [Raw_Data](/Docs_warehouse/Raw_Data/create-dw.txt) (or run your saved 03_create_dw_schema.sql) to create DimCustomer, DimDate, DimProduct, and FactSalesOrder with sample data, then run it and refresh the Warehouse Explorer.

- If the schema list lags, refresh the browser tab or reopen the Warehouse to reload the object list, which is normal after bulk DDL/DML in Fabric Studio. 

![Tables after schema load](/Image_warehouse/tables-after-load.png)

---

## 5) Query by year and month (time rollup)

- Open a new SQL query and run the first aggregation from your 04_queries_aggregations.sql to group SalesRevenue by CalendarYear and MonthName using DimDate, which is the most common warehouse pattern for time grouping  


![Year‑month rollup](/Image_warehouse/query-year-month.png)

---

## 6) Add sales region to the rollup

- Extend the aggregation by joining DimCustomer and grouping on CountryRegion using the second query in 04_queries_aggregations.sql, which answers the typical “period and region” question succinctly.  

![Year‑month‑region rollup](/Image_warehouse/query-year-month-region.png)

---

## 7) Create a reusable view

- Turn the joined aggregation into a warehouse view by running 05_create_view_vSalesByRegion.sql, ensuring the CREATE VIEW statement contains no ORDER BY so the view compiles correctly.

- Validate with the SELECT at the bottom of the same file to confirm expected columns, ordering, and sample values so downstream users can reuse the logic safely.  

![View created](/Image_warehouse/view-created.png)[attached_file:1]

---

## 8) Build a visual query (no‑code slice)

- Choose New visual query in the Warehouse, drag FactSalesOrder onto the canvas, then drag DimProduct; use Merge queries on ProductKey with the default left outer join to bring product attributes into the fact view.  
- Expand the new merged column to keep ProductName, then filter the ProductName column to “Cable Lock” to show a quick product slice stakeholders often ask for without writing SQL  
- Use Visualize results or Download Excel to hand off a quick result; this step mirrors how non‑technical users explore a targeted question in a demo or review  

Paste three screenshots:
- Merge configuration  
![Merge on ProductKey](/Image_warehouse/visual-query-merge.png)
- Expand ProductName  
![Expand ProductName](/Image_warehouse/visual-query-expand-productname.png) 
- Filter to Cable Lock  
![Filter Cable Lock](/Image_warehouse/visual-query-filter-cable-lock.png)

---

## 9) Optional: add a semantic model

- Create a new semantic model from the four tables, then add many‑to‑one single‑direction relationships from FactSalesOrder to DimProduct, DimCustomer, and DimDate on their key columns, which is the standard modeling step before building a report


Paste a screenshot here:
![Semantic model relationships](/Image_warehouse/semantic-model-relationships.png)


---

## Learn sources

- Analyze data in a data warehouse (Lab 06) — the official lab sequence this walkthrough follows step by step.  
- Implement a data warehouse with Microsoft Fabric — broader path with modules for loading, querying, monitoring, and securing the warehouse if you extend this project later.  
