# Olist-Performance-Analysis
Olist Sales Analysis Dashboard --- Excel Power Query & Power Pivot

## Project Overview

This project is an interactive sales and performance analyticsdashboard built entirely in Microsoft Excel, using Power Query fordata preparation and Power Pivot for data modeling and DAX-basedanalysis.

The project was designed to answer a practical business question:

How can sales, product, seller, customer, and delivery data betransformed into actionable insights that support better commercialand operational decisions?

The dashboard combines executive KPIs, time-series analysis, geographicanalysis, product/category performance, delivery performance, customerratings, and seller performance in one interactive analytical view.

This project also reflects my transition from a Material Planningbackground toward Data Analyst / Data Visualization roles, combiningpractical business and supply-chain experience with data analytics andvisualization skills.

## Business Objective

* The dashboard is designed to help a business:

* Monitor overall revenue and order performance

* Identify high-performing sellers

* Understand revenue trends over time

* Compare revenue contribution across Brazilian states

* Identify the highest-revenue product categories

* Evaluate delivery performance

* Investigate the relationship between delivery time and customer ratings

*Compare category revenue against customer ratings

* Identify areas with strong performance and areas requiring improvement

The analysis is intended to move beyond simply reporting numbers andprovide a structure for identifying performance drivers,opportunities, and potential operational issues.

## Dashboard Highlights

The executive dashboard includes the following KPIs:

KPI                  Value shown in dashboard

Revenue                        R$ 13,541,858Orders                                 98,354AOV                                   R$ 138Avg. Rating                              4.11Avg. Delivery                         12 daysOn-Time Delivery                        89.9%

The dashboard also contains:

Revenue Trend by month and year

Seller Performance table

Delivery Performance analysis

Delivery Time vs Customer Rating scatter analysis

Top 10 States by Revenue

Top 10 Categories by Revenue

Revenue as a percentage of total

Category Performance Matrix

Interactive filters for:

Year

Month

State

Product Category

The dashboard is designed to update dynamically based on userselections.

Key Analytical Views

1. Executive KPIs

The dashboard provides a high-level overview of commercial andoperational performance through revenue, orders, average order value,customer rating, delivery time, and on-time delivery.

This allows a recruiter or business stakeholder to quickly understandthe scale and performance of the business before exploring the detailedanalysis.

2. Revenue Trend

The revenue trend visual tracks monthly revenue across 2017 and2018, helping identify changes in sales performance over time.

3. Seller Performance

The seller scorecard compares:

Revenue

Orders

Average Rating

Average Order Value

Average Delivery Days

On-Time %

This creates a multidimensional view of seller performance rather thanranking sellers by revenue alone.

For example, the dashboard shows that Seller 1014 generated R$ 222,776from 358 orders with an AOV of R$ 622 and an on-time rate of 93.0%,while Seller 0882 generated R$ 200,473 from 1,806 orders with an AOV ofR$ 111 and an on-time rate of 87.3%.

This illustrates why looking at several KPIs simultaneously can providemore useful business insight than revenue alone.

4. Delivery Performance

The dashboard separates deliveries into:

On Time

Delayed

Not Delivered

This connects commercial performance with an important operational KPI.

5. Delivery Time vs Customer Rating

The scatter analysis compares delivery days with customerrating, allowing potential relationships between logistics performanceand customer experience to be explored.

6. Geographic Revenue Analysis

The Top 10 States by Revenue visual identifies the largest geographiccontributors to sales and displays both revenue and revenuecontribution.

7. Category Performance Matrix

The category matrix compares Revenue and Rating to classifycategories into four business-performance areas:

High Revenue / High Rating --- Stars

High Revenue / Low Rating --- Improve

Low Revenue / High Rating --- Growth

Low Revenue / Low Rating --- Low Priority

This framework is intended to support prioritization rather than simplyranking categories.

Data Preparation --- Power Query

Power Query was used as the data preparation and transformationlayer.

The workflow includes preparing the source tables so that they can beloaded into a structured analytical model in Power Pivot.

Key data preparation activities include:

Cleaning and structuring source data

Preparing dimension and fact tables

Standardizing fields used for analysis

Creating summarized review data

Preparing date-related fields

Creating category groupings for dashboard analysis

Preparing fields required for relationships and DAX calculations

Loading the transformed tables into the Power Pivot Data Model

The objective was to separate data preparation from analysis andvisualization, creating a more maintainable workflow than building thedashboard directly from raw data.

Data Model / Schema --- Power Pivot

The Power Pivot model follows a fact-and-dimension structure, withFactSales acting as the central transactional table.

Schema Overview

                         Dim_Date
                            |
                            |
                            v
Dim_Product  -------->  FactSales  <-------- Dim_Seller
                            |
                            |
                 +----------+----------+
                 |                     |
                 v                     v
          Dim_Customer          Reviews_Summary


Dim_State
(standalone/reference table in
the displayed model)

Central Fact Table

FactSales

FactSales is the central sales transaction table in the model.

It contains transactional fields such as:

order_id

order_item_id

product_id

seller_id

price

freight_value

customer_id

order_status

order_purchase_timestamp

order_approved_at

order_delivered_carrier_date

order_delivered_customer_date

This table provides the transactional foundation for revenue, orders,delivery, seller, product, and customer analysis.

Dimension Tables

Dim_Date

The date dimension provides the time structure used for trend analysisand filtering.

Fields visible in the model include:

Year_Month

Month_Sort

Month_Name

Month_Year

Date (Year)

Date (Quarter)

Date (Month)

Hierarchy1

The hierarchy contains:

Year
  └── Month

This allows the model to support year/month analysis and chronologicalsorting.

Dim_Product

The product dimension contains descriptive attributes used for productand category analysis.

Fields visible in the model include:

product_id

product_category_name

product_name_lenght

product_description_lenght

product_photos_qty

product_weight_g

product_length_cm

product_height_cm

The product dimension supports category-level revenue analysis and theCategory Performance Matrix.

Dim_Seller

The seller dimension contains seller-level attributes and rankinginformation.

Fields visible in the model include:

seller_id

seller_city

seller_state

StateName

seller_rank

This dimension supports seller performance analysis and seller ranking.

Dim_Customer

The customer dimension contains customer-level attributes.

Fields visible in the model include:

customer_id

customer_unique_id

customer_city

customer_state

StateName

Unique Customers

This dimension supports customer-related analysis and geographicfiltering.

Reviews_Summary

Reviews_Summary contains summarized review information at order level.

Fields visible in the model include:

order_id

avg_review_score

review_count

review_type

The table is connected to FactSales through order_id and supportsthe customer-rating analysis used throughout the dashboard.

Dim_State

Dim_State contains:

StateCode

StateName

In the displayed Power Pivot model, this table appears as a standalonetable without a visible relationship line to FactSales.

Therefore, it should not be described as an active filtering dimensionin the current model unless a relationship is added. The currentdashboard can instead rely on the state fields already present in theseller/customer dimensions.

Model Relationships

The displayed model shows FactSales as the central table connected to:

Dim_Date

Dim_Product

Dim_Seller

Dim_Customer

Reviews_Summary

Conceptually:

                 1
             Dim_Date
                 |
                 *
                 |
1  Dim_Product -- FactSales -- Dim_Seller  1
                 |
                 *
                 |
            Dim_Customer  1

                 |
                 *
                 |
          Reviews_Summary  1

The model separates descriptive attributes from transactional salesdata, which makes it easier to build reusable measures and interactivereports.

Power Pivot / DAX

Power Pivot was used to create analytical measures and calculations forthe dashboard.

The model supports calculations such as:

Total Revenue

Total Orders

Average Order Value

Average Rating

Average Delivery Days

On-Time %

Revenue % of Total

Seller ranking

Category performance

Delivery performance

The use of measures allows dashboard calculations to respond to filtersand slicers instead of relying on hard-coded values.

Interactivity

One of the main objectives of the project is to demonstrateinteractive data visualization, rather than creating a static Excelreport.

Users can filter the dashboard by:

Year

Month

State

Product Category

The visuals and KPIs update based on the selected filter context.

This demonstrates the use of Excel as a self-service analytical tool andshows how a structured Power Pivot model can support an interactivedashboard.

Analytical Skills Demonstrated

Data Preparation

Power Query

Data cleaning

Data transformation

Data structuring

Data summarization

Data Modeling

Power Pivot

Fact and dimension tables

Relationships

Date dimension

Data model design

Data Analysis

KPI development

Revenue analysis

Trend analysis

Seller performance analysis

Geographic analysis

Category analysis

Delivery performance

Customer rating analysis

Performance segmentation

Data Visualization

Interactive Excel dashboards

KPI cards

Trend charts

Bar charts

Scatter plots

Performance matrices

Slicers

Dynamic filtering

Business / Supply Chain Perspective

My background in material planning provides a practical businessperspective when interpreting operational data. This project appliesthat mindset to a broader analytical context by connecting commercialperformance with delivery, seller, customer, and product-level metrics.

Why I Built This Project

I am developing my career from a material planning and supply-chainbackground toward Data Analyst and Data Visualization roles.

Rather than treating data analytics as purely technical work, I want tocombine:

Business & Supply Chain Experience



Data Analysis & Visualization

to solve practical business problems.

This project demonstrates my ability to take structured business data,prepare it, model it, analyze it, and communicate the results through aninteractive dashboard.

Tools Used

Microsoft Excel

Power Query

Power Pivot

DAX

Data Modeling

Data Visualization

Project Structure

Olist-Excel-Analytics/
│
├── README.md
│
├── dashboard/
│   └── Olist_Sales_Dashboard.xlsx
│
├── screenshots/
│   └── dashboard-preview.png
│
└── video/
    └── dashboard-demo.mp4

Portfolio Value

This project demonstrates more than Excel chart creation. It shows an end-to-end analytical workflow:

Raw Data
   ↓
Power Query
   ↓
Data Cleaning & Transformation
   ↓
Power Pivot Data Model
   ↓
DAX Measures
   ↓
Interactive Dashboard
   ↓
Business Insights

The goal is to demonstrate how I approach data as an analyst: structure it correctly, create reusable calculations, visualize the right KPIs, and turn the results into information that can support business decisions.



Excel / Power Query / Power Pivot
