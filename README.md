# ecommerce_lakehouse_analytics_platform_prod

# E-Commerce Lakehouse Analytics Platform

## Overview

The E-Commerce Lakehouse Analytics Platform is an end-to-end Data Engineering project built using Databricks and Delta Lake. The project demonstrates how raw e-commerce data can be transformed into a business-ready analytics platform using the Medallion Architecture (Bronze, Silver, Gold) and dimensional modeling techniques.

The solution provides insights into sales performance, customer behavior, product trends, payment analytics, and operational KPIs.

---

## Business Objective

The goal of this project is to build a scalable analytics platform that enables business users to answer key questions such as:

* What is the total revenue generated?
* Which products generate the highest sales?
* Who are the top customers?
* What is the Average Order Value (AOV)?
* Which payment methods are most popular?
* How do sales trends vary across time?
* What is the return rate of products?

---

## Technology Stack

* Databricks
* PySpark
* Delta Lake
* Unity Catalog
* Databricks Asset Bundles (DAB)
* Git & GitHub
* SQL

---

## Source Datasets

### customers.csv

| Column        |
| ------------- |
| customer_id   |
| customer_name |
| email         |
| city          |
| state         |
| signup_date   |

### products.csv

| Column       |
| ------------ |
| product_id   |
| product_name |
| category     |
| brand        |

### orders.csv

| Column         |
| -------------- |
| order_id       |
| customer_id    |
| order_date     |
| order_status   |
| payment_method |
| order_channel  |

### order_items.csv

| Column     |
| ---------- |
| order_id   |
| product_id |
| quantity   |
| unit_price |

### returns.csv

| Column        |
| ------------- |
| return_id     |
| order_id      |
| product_id    |
| return_date   |
| refund_amount |

---

## Architecture

```text
Landing Layer
      │
      ▼
Bronze Layer
(Raw Delta Tables)
      │
      ▼
Silver Layer
(Cleansed & Validated Data)
      │
      ▼
Gold Layer
(Dimensional Model)
      │
      ▼
Business KPIs & Reporting
```

---

## Medallion Architecture

### Bronze Layer

Stores raw source data without transformation.

Tables:

* bronze.customers
* bronze.products
* bronze.orders
* bronze.order_items
* bronze.returns

### Silver Layer

Performs data cleansing, standardization, and validation.

Examples:

* Remove duplicates
* Standardize date formats
* Validate mandatory fields
* Handle null values

### Gold Layer

Implements a dimensional model optimized for analytics.

---

## Dimensional Model

### Dimension Tables

#### dim_customer

* customer_key
* customer_id
* customer_name
* email
* city
* state
* signup_date

#### dim_product

* product_key
* product_id
* product_name
* category
* brand

#### dim_date

* date_key
* date
* day
* month
* quarter
* year

#### dim_order

* order_key
* order_id
* order_status
* payment_method
* order_channel

---

### Fact Table

#### fact_sales

Grain: One row per order item

Columns:

* customer_key
* product_key
* order_key
* date_key
* quantity
* unit_price
* sales_amount
* return_flag
* refund_amount

---

## Star Schema

```text
┌──────────────┐                              ┌──────────────┐
│ DIM_CUSTOMER │                              │ DIM_PRODUCT  │
└──────┬───────┘                              └──────┬───────┘
       │                                             │
       │                                             │
       ▼                                             ▼

┌──────────────┐      ┌──────────────────┐      ┌──────────────┐
│   DIM_DATE   │─────►│    FACT_SALES    │◄─────│  DIM_ORDER   │
└──────────────┘      └──────────────────┘      └──────────────┘
```

---

## Key Performance Indicators (KPIs)

### Sales KPIs

* Total Revenue
* Total Orders
* Total Units Sold
* Average Order Value (AOV)

### Customer KPIs

* Total Customers
* New Customers
* Repeat Customers
* Top Customers by Revenue

### Product KPIs

* Top Selling Products
* Revenue by Product
* Revenue by Category
* Revenue by Brand

### Order KPIs

* Orders by Status
* Revenue by Order Channel

### Payment KPIs

* Revenue by Payment Method
* Orders by Payment Method

### Return KPIs

* Return Rate %
* Revenue Lost Due to Returns
* Most Returned Products

---

## Project Structure

```text
ecommerce_lakehouse_analytics_platform

├── datasets/
├── src/
│   ├── bronze/
│   ├── silver/
│   └── gold/
├── resources/
│   └── jobs/
├── docs/
├── databricks.yml
└── README.md
```

---

## Learning Outcomes

This project demonstrates:

* End-to-End Data Engineering
* Medallion Architecture
* Delta Lake Fundamentals
* Dimensional Modeling
* Star Schema Design
* Databricks Asset Bundles (DAB)
* ETL/ELT Pipeline Development
* Business KPI Development
* Data Warehouse Design

---

## Disclaimer

This is a portfolio project created for educational and demonstration purposes. The datasets used are synthetic and do not contain real customer information.
