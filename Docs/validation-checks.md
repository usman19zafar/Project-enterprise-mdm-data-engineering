# Data Validation & Quality Checks

This document outlines the validation checks applied across the pipeline to ensure data quality and trustworthiness.

---

## 1. Record Count Validation
- Compare Bronze vs Silver counts.
- Ensure Silver count ≤ Bronze count.
- Log discrepancies.

---

## 2. Duplicate Validation
- After deduplication:

COUNT(*) == COUNT(DISTINCT business_key)

- If mismatch → flag issue.

---

## 3. Mandatory Field Validation
Check for nulls in:
- customer_id
- product_id
- order_id
- order_date
- quantity
- unit_price

Rows failing validation are removed.

---

## 4. Data Type Validation
- Ensure numeric fields contain valid numbers.
- Ensure dates parse correctly.
- Ensure email contains `@`.

---

## 5. Referential Integrity Checks
In Gold:
- Every order must map to a valid customer.
- Every order must map to a valid product.

Unmatched rows → flagged or excluded.

---

## 6. Metric Validation
Gold metrics validated using:
- SUM(total_amount) across layers
- COUNT(order_id)
- AVG(total_amount)

---

## 7. Schema Drift Validation
- Unexpected columns → logged
- Missing expected columns → pipeline fails fast

---

## 8. Output Validation
- Confirm Delta files written
- Confirm partition folder exists
- Confirm row counts > 0

