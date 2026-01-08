# Database Schema Documentation – FlexiMart

## 1. Entity-Relationship Description

### ENTITY: customers
**Purpose:** Stores customer information for FlexiMart.

**Attributes:**
- customer_id: Unique identifier for each customer (Primary Key)
- first_name: Customer's first name
- last_name: Customer's last name
- email: Customer's email address (unique)
- phone: Customer's contact number
- city: City where the customer resides
- registration_date: Date when the customer registered

**Relationships:**
- One customer can place MANY orders  
  (1 : M relationship with orders table)

---

### ENTITY: products
**Purpose:** Stores product details available on FlexiMart.

**Attributes:**
- product_id: Unique identifier for each product (Primary Key)
- product_name: Name of the product
- category: Product category
- price: Selling price of the product
- stock_quantity: Available stock count

**Relationships:**
- One product can appear in MANY order_items  
  (1 : M relationship with order_items table)

---

### ENTITY: orders
**Purpose:** Stores order-level information placed by customers.

**Attributes:**
- order_id: Unique order identifier (Primary Key)
- customer_id: References the customer placing the order (Foreign Key)
- order_date: Date when the order was placed
- total_amount: Total value of the order
- status: Current status of the order

**Relationships:**
- One order belongs to ONE customer (M : 1)
- One order can have MANY order items (1 : M)

---

### ENTITY: order_items
**Purpose:** Stores item-level details for each order.

**Attributes:**
- order_item_id: Unique identifier (Primary Key)
- order_id: References orders table (Foreign Key)
- product_id: References products table (Foreign Key)
- quantity: Quantity of product ordered
- unit_price: Price per unit at the time of order
- subtotal: Calculated as quantity × unit_price

---

## 2. Normalization Explanation (3NF)

The database schema is designed following Third Normal Form (3NF) to ensure data integrity and eliminate redundancy.  
Each table has a primary key, and all non-key attributes depend only on the primary key.

### Functional Dependencies:
- customer_id → first_name, last_name, email, phone, city, registration_date
- product_id → product_name, category, price, stock_quantity
- order_id → customer_id, order_date, total_amount, status
- order_item_id → order_id, product_id, quantity, unit_price, subtotal

There are no partial dependencies because all tables use single-column primary keys.  
There are no transitive dependencies because non-key attributes do not depend on other non-key attributes.

### Avoidance of Anomalies:
- **Insert Anomaly:** New customers or products can be added independently without creating orders.
- **Update Anomaly:** Customer or product details are stored once, so updates occur in only one place.
- **Delete Anomaly:** Deleting an order does not remove customer or product information.

This normalized structure improves data consistency, reduces duplication, and supports efficient querying.

---

## 3. Sample Data Representation

### customers
| customer_id | first_name | last_name | email              | city   | registration_date |
|------------|------------|-----------|--------------------|--------|-------------------|
| 1          | Rahul      | Sharma    | rahul@gmail.com    | Delhi  | 2023-01-12        |
| 2          | Anita      | Verma     | anita@gmail.com    | Mumbai| 2023-02-15        |

---

### products
| product_id | product_name | category     | price  | stock_quantity |
|-----------|--------------|--------------|--------|----------------|
| 101       | Laptop       | Electronics  | 55000  | 10             |
| 102       | Headphones   | Electronics  | 2500   | 25             I

---

### orders
| order_id | customer_id | order_date | total_amount | status     |
|---------|-------------|------------|--------------|------------|
| 1001    | 1           | 2023-03-10 | 57500        | Completed  |
| 1002    | 2           | 2023-03-12 | 2500         | Completed  |

---

### order_items
| order_item_id | order_id | product_id | quantity | unit_price | subtotal |
|--------------|----------|------------|----------|------------|----------|
| 1            | 1001     | 101        | 1        | 55000      | 55000    |
| 2            | 1001     | 102        | 1        | 2500       | 2500     |
