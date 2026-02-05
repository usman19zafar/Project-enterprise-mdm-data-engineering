# Business Rules for Master Data Processing

This document defines the business rules applied across the Bronze → Silver → Gold pipeline for Project 3 (MDM-style master data processing). These rules ensure consistency, quality, and trust in downstream analytical outputs.

---

## 1. Entity Standardization Rules
- All master entities (Customers, Products, Orders) must follow a consistent schema.
- Attribute names must be standardized to lowercase with underscores.
- Date attributes must follow `YYYY-MM-DD` format.
- Numeric attributes must be cast to their correct types (int, long, double).

---

## 2. Mandatory Attribute Rules
Each entity must contain the following required fields:

### Customer
- `customer_id`
- `first_name`
- `last_name`
- `email`

### Product
- `product_id`
- `product_name`
- `category`

### Orders
- `order_id`
- `customer_id`
- `product_id`
- `order_date`
- `quantity`
- `unit_price`

Records missing mandatory attributes are filtered out in Silver.

---

## 3. Standardization Rules
- Trim whitespace from all string fields.
- Convert names and city/state fields to proper case.
- Convert email to lowercase.
- Convert category fields to uppercase.
- Standardize date formats using Spark/ADF expressions.

---

## 4. Derived Business Attributes
### Orders
- `total_amount = quantity * unit_price`
- `order_year = year(order_date)`
- `order_month = month(order_date)`

### Customer Metrics (Gold)
- `total_revenue = SUM(total_amount)`
- `total_quantity = SUM(quantity)`
- `order_count = COUNT(order_id)`
- `avg_order_value = total_revenue / order_count`

---

## 5. Survivorship & Deduplication Rules
- Business key for Customer: `customer_id`
- Business key for Product: `product_id`
- Business key for Orders: `order_id`
- When duplicates exist:
  - Keep the record with the latest `order_date` or `signup_date`
  - If dates match, keep the record with the highest `total_amount`
  - If still tied, keep the first record by ingestion timestamp

---

## 6. Data Quality Rules
- Null or invalid keys → drop
- Negative quantities or prices → drop
- Invalid dates → drop
- Email format must contain `@` and a domain

---

## 7. Promotion Rules
- Bronze → Silver: schema enforcement, cleansing, dedupe
- Silver → Gold: business metrics, joins, analytics preparation

These rules ensure a consistent, governed master dataset across all layers.
