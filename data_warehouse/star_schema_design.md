# Star Schema Design Documentation – FlexiMart

## Section 1: Schema Overview

### FACT TABLE: fact_sales

**Grain:**  
One row per product per order line item.

**Business Process:**  
Sales transactions generated from customer orders.

**Measures (Numeric Facts):**
- quantity_sold: Number of units sold for a product in an order
- unit_price: Price per unit at the time of sale
- discount_amount: Discount applied on the line item
- total_amount: Final sales value  
  (quantity_sold × unit_price − discount_amount)

**Foreign Keys:**
- date_key → dim_date
- product_key → dim_product
- customer_key → dim_customer

---

### DIMENSION TABLE: dim_date

**Purpose:**  
Supports time-based analysis such as daily, monthly, quarterly, and yearly trends.

**Type:**  
Conformed dimension.

**Attributes:**
- date_key (PK): Surrogate key in YYYYMMDD format
- full_date: Actual calendar date
- day_of_week: Monday, Tuesday, etc.
- month: Numeric month (1–12)
- month_name: January, February, etc.
- quarter: Q1, Q2, Q3, Q4
- year: Calendar year (2023, 2024, etc.)
- is_weekend: Boolean flag (true/false)

---

### DIMENSION TABLE: dim_product

**Purpose:**  
Provides product-level descriptive information for sales analysis.

**Attributes:**
- product_key (PK): Surrogate key
- product_id: Business/natural product identifier
- product_name: Name of the product
- category: Product category (Electronics, Footwear, etc.)
- brand: Product brand
- price: Standard product price

---

### DIMENSION TABLE: dim_customer

**Purpose:**  
Enables customer-based analysis such as location and purchasing behavior.

**Attributes:**
- customer_key (PK): Surrogate key
- customer_id: Business/natural customer identifier
- customer_name: Full name of the customer
- email: Customer email address
- city: Customer city
- registration_date: Date when the customer registered

---

## Section 2: Design Decisions (Approx. 150 words)

The fact table is designed at the transaction line-item level to capture the most granular sales data. This granularity allows detailed analysis such as product-level revenue, discounts applied per item, and customer purchase behavior. From this level, data can easily be aggregated to higher levels like order, customer, or monthly summaries.

Surrogate keys are used instead of natural keys to ensure consistency and performance in the data warehouse. Natural keys may change over time or differ across source systems, whereas surrogate keys provide a stable and efficient way to join fact and dimension tables.

This star schema design supports drill-down and roll-up operations effectively. Analysts can drill down from yearly sales to quarterly, monthly, or daily sales using the date dimension, and roll up product-level sales into category-level or brand-level summaries. The simple structure with fewer joins improves query performance and usability for analytical reporting.

---

## Section 3: Sample Data Flow

### Source Transaction
Order #101  
Customer: John Doe  
Product: Laptop  
Quantity: 2  
Unit Price: 50,000  

---

### Data Warehouse Representation

**fact_sales**

**dim_date**

**dim_product**

**dim_customer**



**dim_date**
