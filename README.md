# 🏗️ Microsoft Fabric Data Warehouse 

![hero](/images/warehouse-hero.gif) [web:221]

## Introduction 
I built a working Microsoft Fabric data warehouse by following the core flow of Lab 06 and documenting every step so reviewers can reproduce the warehouse, run the queries, and verify results quickly in Fabric Studio.  
The goal was to show real warehouse skills end to end: provisioning, star‑schema tables, SQL aggregations, a reusable view, a visual query demo, and an optional semantic model ready for reporting.

## Background
Fabric warehouses support full T‑SQL semantics and are designed for dimensional analytics that business teams actually use, so I chose Lab 06 because it maps closely to how consulting teams stand up analysis quickly for stakeholders.  
The lab scaffolds a compact dimensional model with FactSalesOrder and common dimensions, which is perfect to demonstrate grouping by calendar, region, and product with simple, reviewable SQL.  

## The questions I wanted to answer through my SQL queries were 
- How is SalesRevenue trending by CalendarYear and MonthName, and which periods drive the largest changes at a glance?  
- Which CountryRegion segments contribute most to SalesRevenue when I join the customer dimension and group the results for stakeholder reviews?  
- Can I encapsulate the joined aggregations in a view so downstream users can reuse a consistent definition without copying SQL around the workspace?  
- If a stakeholder asks for a quick product focus, can I merge, expand, and filter for a specific ProductName like “Cable Lock” using the Visual query experience without writing code?  

## Tools I Used 
- Microsoft Fabric Warehouse for full SQL semantics on dimensional tables to support analytic joins, aggregations, and views.  
- Fabric SQL editor to create tables, load schema, run grouped queries, and define a reusable view for downstream use.  
- Fabric Visual query to demonstrate a no‑code flow for merge, expand ProductName, and filter for a targeted product slice.  
- Optional semantic model to link FactSalesOrder to DimProduct, DimCustomer, and DimDate using many‑to‑one relationships for BI modeling.

## The Analysis 
- Workspace and warehouse: I created a Fabric workspace with capacity and provisioned a Warehouse, capturing object explorer states after each step to confirm progress.  
- Tables: I created DimProduct first with a simple CREATE and sample INSERT, then loaded the lab schema to add DimCustomer, DimDate, DimProduct, and FactSalesOrder, verifying all four tables in Explorer.  
- Aggregations: I wrote a grouped query for SalesRevenue by CalendarYear and MonthName using DimDate, then extended the query by joining DimCustomer to include CountryRegion in the rollup output.  
- View: I created vSalesByRegion from the grouped query without ORDER BY so downstream users can SELECT from a shared, governed definition for year, month, and region analysis. 
- Visual query: I built a canvas flow that merges FactSalesOrder with DimProduct on ProductKey, expands ProductName, and filters to “Cable Lock” to show a quick, code‑free stakeholder answer path.
- Optional modeling: I added a semantic model with many‑to‑one single‑direction relationships from FactSalesOrder to all dimensions so the dataset is modeling‑ready for reports if needed.  

## What I Learned 
- A small, well‑named star schema makes business questions trivial to answer with short T‑SQL and clear JOINs, which is exactly what implementation teams need in the first iteration.  
- Encapsulating aggregations in a view like vSalesByRegion avoids query drift and gives teams a stable contract for year, month, and region rollups that can be reused across analyses.
- Visual query is a great way to show non‑technical stakeholders the same logic they would ask for in a dashboard, and it keeps the SQL surface clean while they explore product‑level questions. 
- The semantic model step connects fact to dimensions for BI and governance, which mirrors how Fabric projects move from exploration to production in consulting contexts.  

## Closing Thoughts 
This portfolio focuses on the core warehouse build for Lab 06, but the Fabric learning path makes it easy to extend into loading patterns, broader querying, monitoring, and security as a natural next step for real projects. 
My next iteration will branch this repo to add monitoring notes using the companion lab and a small security note on access direction so the portfolio covers both analytics and operational awareness.  





