# Cleaning Log

## Task 5 – Business Rules Applied

### Business Rule Decisions

| Rule Area | Required Action | Action Taken |
|------------|-------------|-------------|
| Missing Region | Fill as Unknown and flag | Replaced missing values with 'Unknown' and flagged |
| Missing Ship Mode | Fill as Unknown and flag | Replaced missing values with 'Unknown' and flagged |
| Missing Discount | Treat as 0 only if other sales fields are valid | Created cleaned_discount field and reviewed records |
| Negative Discount | Flag as invalid | Flagged in data_quality_flag |
| Discount Above Allowed Range | Flag as invalid | No such discounts in data set |
| Cancelled Orders | Exclude from completed sales summary | Excluded using sales_inclusion = No |
| Failed Payments | Exclude from completed sales summary | Excluded using sales_inclusion = No |
| Refunded Orders | Summarize separately | Separate pivot summary created |
| Ship Date Before Order Date | Flag as invalid shipping record | Flagged in data_quality_flag |
| Sales Validation | Sales must equal Quantity × Unit Price × (1−Discount) | Created calculated_sales and flagged mismatches |
| Status Validation | Order and payment statuses must follow business logic | Invalid combinations flagged |



### Business Rule Outcomes

| Issue | Count |
|------|------:|
| Missing Region | 25 |
| Missing Ship Mode | 21 |
| Invalid Discounts | 29 |
| Invalid Shipping Records | 21 |
| Sales Mismatches | 63 |
| Invalid Status Combinations | 86 |
| Cancelled Orders | 145 |
| Returned Orders | 163 |
| Refunded Payments | 71 |
| Failed Payments | 69 |

---

# Task 9 – Cleaning Log

## 1. List of Issues Found

### Duplicate Issues
- 20 identical duplicate pairs (40 records)
- 12 conflicting duplicate pairs (24 records)

### Missing Values
- 25 missing Region values
- 21 missing Ship Mode values
- 14 missing/unknown Discount values

### Invalid Values
- 15 negative discount values
- 21 records where ship_date is earlier than order_date
- 63 sales calculation mismatches (due to invalid/unknown discount and calculation error)
- 86 invalid order status and payment status combinations

### Text Quality Issues
- Leading spaces
- Trailing spaces
- Multiple spaces between words
- Inconsistent capitalization
- Category and sub-category naming inconsistencies

---

## 2. Cleaning Actions Performed

### Duplicate Handling
- Identified 20 identical duplicate pairs.
- Removed one record from each pair.
- Total records removed: 20.
- Identified 12 conflicting duplicate pairs.
- Retained conflicting records and flagged them for review.

### Example
For Order ID ORD-2024-10124:
- Three records existed.
- Two records are identical.
- One duplicate record is removed.
- Remaining conflicting records are retained and flagged.

### Date Standardization
- Standardized order_date and ship_date fields to YYYY/MM/DD.
- No invalid calendar dates are found.

### Text Standardization
Functions used:
- TRIM()
- PROPER()
- Flash Fill

Fields cleaned:
- customer_name
- segment
- region
- category
- sub_category
- ship_mode
- payment_status
- order_status

### Missing Value Handling
- Missing Region → Replaced with Unknown and flagged.
- Missing Ship Mode → Replaced with Unknown and flagged.
- Missing Discount → Flagged for review.

### Validation and Enrichment Columns Added
- order_month
- order_year
- shipping_delay_days
- cleaned_discount
- calculated_sales
- calculated_profit
- profit_margin
- sales_inclusion
- data_quality_flag

---

## 3. Business Rules Applied

### Missing Region
- Replaced missing values with Unknown.
- Flagged records for review.

### Missing Ship Mode
- Replaced missing values with Unknown.
- Flagged records for review.

### Missing Discount
- Reviewed according to business rule.
- Zero added to missing discounts with valid sales values. (18 missing discount rows having 4 valid sales values are added 0.) 

### Invalid Discounts
- 15 negative discount values flagged.
- 14 missing/unknown discount values flagged.

### Cancelled Orders
- Excluded from final completed sales reporting.

### Failed Payments
- Excluded from final completed sales reporting.

### Refunded Orders
- Reported separately in pivot summaries.

### Invalid Shipping Records
- Ship date earlier than order date.
- 21 records flagged.

### Sales Validation
Expected Formula:
Sales = Quantity × Unit Price × (1 − Discount)

- Created calculated_sales field.
- 63 mismatched records flagged.

### Status Validation
- Invalid combinations such as Returned + Pending and Returned + Failed are flagged.
- No status values are modified.

---

## 4. Assumptions Made

- Missing Region values are assigned Unknown.
- Missing Ship Mode values are assigned Unknown.
- Conflicting duplicate records are retained to preserve auditability.
- Original sales values are preserved.
- Invalid discounts are not manually corrected.
- Invalid order/payment status combinations are not automatically corrected.
- Business-rule violations are flagged rather than modified.

---

## 5. Records Removed

| Reason | Records Removed |
|----------|------:|
| Identical Duplicate Records | 20 |

No other records are removed from the dataset.

---

## 6. Records Flagged

| Issue | Count |
|------|------:|
| Missing Region | 25 |
| Missing Ship Mode | 21 |
| Invalid Discounts | 29 |
| Invalid Shipping Records | 21 |
| Sales Mismatches | 63 |
| Invalid Status Combinations | 86 |
| Conflicting Duplicate Records | 24 |

Examples of values stored in data_quality_flag:
- Clean Data
- Warning Missing Region
- Warning Missing Ship Mode
- Invalid Shipping Record
- Invalid Discount
- Sales is not equal to (quantity × unit_price × (1-discount))
- Invalid Order Status & Payment Status Combination

---

## 7. Limitations of the Cleaning Process

- Invalid status combinations are identified but not corrected.
- Sales mismatches are flagged while preserving original sales values.
- Conflicting duplicate records require manual business review.
- Missing discount values could not be reliably inferred.
- Some flagged records may require domain expert validation before operational use.

---

## Sales Inclusion Logic

A sales_inclusion field is created with values Yes and No.

Records are included (Yes) when:
- Order Status = Completed
- Payment Status = Paid

And all data quality condition as below
- Clean Data
- Warning Missing Region
- Warning Missing Ship Mode
- Sales mismatch due to calculation error rather than caused by invalid/unknown discounts.
- Invalid Shipping Record
Cancelled orders and failed payments are excluded from completed sales reporting.

---

## Final Dataset Summary

| Metric | Count |
|----------|------:|
| Raw Records | 932 |
| Identical Duplicate Records Removed | 20 |
| Final Records | 912 |

The dataset is cleaned, standardized, validated, and enriched with calculated fields while preserving an audit trail of all data quality issues through the data_quality_flag field.



