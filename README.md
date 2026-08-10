# Olist Performance Analysis — Excel, Power Query & Power Pivot

An interactive sales & delivery performance dashboard for Olist (Brazilian e-commerce) built entirely in Excel, using Power Query for data transformation, Power Pivot for data modeling, and DAX for KPIs.

## Goal

Give business stakeholders a self-service, slicer-driven view of revenue, delivery performance, and customer satisfaction — without needing SQL or Python — by turning the raw Olist tables into a proper star-schema data model inside Excel.

## Data Model

Raw Olist tables (orders, order items, products, sellers, customers, reviews) were loaded and cleaned with Power Query, then modeled in Power Pivot as a star schema: a central FactSales table linked to Dim_Date, Dim_Product, Dim_Seller, Dim_Customer, Dim_State, and a Reviews_Summary table.

## Show Image

* Key DAX Measures
* Revenue — total sales value
* Total Orders
* Average Order Value (AOV)
* Average Delivery Days
* On Time % — share of orders delivered by the estimated date
* Average Review — average customer review score

## Dashboard
The Executive Dashboard brings these measures together with interactive slicers (year, month, state, product category) driving:

* Revenue trend by year/month
* On-time vs. delayed vs. not-delivered order split
* Seller leaderboard (revenue, orders, avg. rating, AOV, delivery time, on-time %)
* Average review score and delivery time by state
* Revenue and review score by product category

## Demo
A short screen recording (Olist_Dashboard_Demo.mp4) shows the slicers and cross-filtering in action — selecting a state or category updates every chart and KPI on the dashboard live.

## Tools
Excel, Power Query, Power Pivot, DAX


