# Retail Orders Data Cleaning & Analytics Project

## 1. Problem Summary

This project focuses on cleaning, validating, and analyzing a retail orders dataset. The objective was to improve data quality, apply business rules, generate analytical summaries using Pivot Tables, and produce business insights that can support decision-making.

The project includes:
- Data cleaning and standardization
- Duplicate handling
- Date validation
- Business rule implementation
- Data quality assessment
- Pivot-based business analysis
- Documentation of cleaning decisions and assumptions

---

## 2. Dataset Description

### Source Files
- `raw_orders.xlsx` – Original dataset
- `cleaned_orders.xlsx` – Cleaned and enriched dataset
- `data_quality_report.xlsx` – Data quality assessment report
- `pivot_summary.xlsx` – Pivot-based analytical summaries
- `cleaning_log.md` – Documentation of cleaning activities

### Record Summary

| Metric | Count |
|----------|------:|
| Raw Records | 932 |
| Identical Duplicate Records Removed | 20 |
| Final Records | 912 |

### Key Data Fields

- order_id
- order_date
- ship_date
- customer_name
- segment
- region
- state
- city
- category
- sub_category
- quantity
- unit_price
- discount
- sales
- cost
- profit
- ship_mode
- payment_status
- order_status

### Additional Fields Created

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

## 3. Tools Used

### Microsoft Excel

Used for:
- Data cleaning
- Date standardization
- Duplicate analysis
- Pivot tables
- Data validation
- Reporting

### Excel Functions Used

- TRIM()
- PROPER()
- Flash Fill
- IF()
- YEAR()
- MONTH()
- Date functions
- Pivot Tables

---

## 4. Cleaning Steps Performed

### Text Cleaning

The following fields were standardized:

- customer_name
- segment
- region
- state
- city
- category
- sub_category
- ship_mode
- payment_status
- order_status

Cleaning actions:
- Removed leading spaces
- Removed trailing spaces
- Removed extra spaces
- Standardized capitalization
- Corrected inconsistent text formatting

### Date Cleaning

- Standardized order_date to YYYY/MM/DD format
- Standardized ship_date to YYYY/MM/DD format
- Verified date consistency
- No invalid calendar dates were found

### Duplicate Handling

- 20 identical duplicate records removed
- 12 conflicting duplicate pairs (24 records) retained and flagged for review

### Missing Value Handling

- Missing Region → Replaced with "Unknown"
- Missing Ship Mode → Replaced with "Unknown"
- Missing Discount → Reviewed according to business rules

### Validation Columns Added

- shipping_delay_days
- calculated_sales
- calculated_profit
- profit_margin
- sales_inclusion
- data_quality_flag

---

## 5. Business Rules Applied

| Rule Area | Action Taken |
|------------|-------------|
| Missing Region | Replaced with Unknown and flagged |
| Missing Ship Mode | Replaced with Unknown and flagged |
| Missing Discount | Treated according to business rule and reviewed |
| Negative Discount | Flagged as invalid |
| Cancelled Orders | Excluded from completed sales summaries |
| Failed Payments | Excluded from completed sales summaries |
| Refunded Orders | Summarized separately |
| Ship Date Before Order Date | Flagged as invalid shipping record |
| Sales Validation | Compared against Quantity × Unit Price × (1−Discount) |
| Invalid Status Combinations | Flagged for review |

### Sales Inclusion Logic

Orders were included in completed sales reporting only when:

- Order Status = Completed
- Payment Status = Paid

Cancelled orders and failed payments were excluded from completed sales reporting.

---

## 6. Summary of Data Quality Issues Found

| Issue | Count |
|---------|------:|
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
| Conflicting Duplicate Records | 24 |

### Duplicate Summary

- Identical duplicate records removed: 20
- Conflicting duplicate records retained and flagged: 24

---

## 7. Summary of Final Pivot Reports

### Sales and Profit by Region

Findings:
- South region generated the highest sales.
- West and East regions also contributed significantly.
- Unknown region records were retained for reporting transparency.

### Sales and Profit by Category and Sub-Category

Findings:
- Technology generated the highest sales and profit.
- Copiers produced the highest sales within Technology.
- Chairs and Furnishings were strong contributors within Furniture.

### Order Count by Ship Mode

Findings:
- Standard Class had the highest order count.
- Unknown ship modes were tracked separately.

### Profit Margin by Customer Segment

Average Profit Margin:

| Segment | Profit Margin (%) |
|----------|------:|
| Home Office | 28.99 |
| Small Business | 28.73 |
| Corporate | 28.03 |
| Consumer | 21.09 |

### Refunded / Cancelled / Failed Orders by Region

Separate pivot summaries were created to monitor operational issues by region.

### Monthly Sales Trend

Findings:
- February generated the highest sales.
- November and December recorded comparatively lower sales.
- Monthly trend analysis provides seasonality insights.

---

## 8. Key Business Insights

1. South region is the strongest sales contributor.
2. Technology is the highest-performing product category.
3. Copiers are the top-selling Technology sub-category.
4. Home Office customers generate the highest profit margins.
5. A significant number of cancelled and returned orders require operational review.
6. Invalid order and payment status combinations indicate process-quality issues.
7. Missing Region and Ship Mode values highlight data-entry weaknesses.
8. Sales validation identified records requiring financial review.

---

## 9. Assumptions and Limitations

### Assumptions

- Missing Region values were replaced with "Unknown".
- Missing Ship Mode values were replaced with "Unknown".
- Conflicting duplicate records were retained to preserve auditability.
- Original sales values were preserved.
- Business-rule violations were flagged instead of automatically corrected.

### Limitations

- Invalid status combinations were not corrected.
- Sales mismatches were flagged but retained.
- Conflicting duplicates require manual business review.
- Missing discounts could not be reliably inferred.
- Some flagged records may require domain-expert validation.

---

## 10. Screenshots Included

The submission includes screenshots demonstrating:

- Data cleaning process
- Business rule implementation
- Data quality report
- Pivot summaries
- Monthly sales trend analysis
- Sales and profit reporting
- Profit margin analysis
- Refunded, failed, and cancelled order summaries

---

## Deliverables

- cleaned_orders.xlsx
- data_quality_report.xlsx
- pivot_summary.xlsx
- cleaning_log.md
- README.md

