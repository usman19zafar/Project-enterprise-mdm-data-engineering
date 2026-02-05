# Deduplication & Survivorship Logic

This document defines the deduplication strategy used in the Silver layer for all master entities.

---

## 1. Business Keys
- Customer: `customer_id`
- Product: `product_id`
- Orders: `order_id`

Duplicates are defined as multiple records sharing the same business key.

---

## 2. Deduplication Strategy

### Step 1 — Partition by Business Key
Use a window function:

```code
ROW_NUMBER() OVER (
PARTITION BY business_key
ORDER BY last_updated DESC, ingestion_timestamp DESC
)
```

### Step 2 — Survivorship Rules
Keep the record with:
1. The latest `last_updated` or `order_date`
2. If tied → highest `total_amount`
3. If tied → earliest ingestion timestamp

### Step 3 — Filter
Keep only:
row_number = 1


---

## 3. Why This Logic Works
- Ensures deterministic output  
- Handles late-arriving data  
- Preserves the most accurate record  
- Eliminates duplicates without losing lineage  

---

## 4. Applied In
- Silver Customer
- Silver Product
- Silver Orders

