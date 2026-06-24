# 📘 **Retail Orders Data Cleaning Project**

## **1. Problem Summary**
The raw retail orders dataset contained inconsistent text fields, mixed date formats, invalid discounts, missing values, duplicate records, and business‑rule violations.  
The goal of this project was to clean, validate, and standardize the dataset to produce an analysis‑ready version, generate data‑quality reports, create pivot summaries, and document the entire cleaning process.

---

## **2. Dataset Description**
The dataset includes order‑level retail transactions with the following key fields:

- **Order details:** order_id, order_date, ship_date, ship_mode, order_status  
- **Customer details:** customer_id, customer_name, segment, region, state, city  
- **Product details:** product_id, product_name, category, sub_category  
- **Financials:** quantity, unit_price, discount, sales, cost, profit  
- **Payment details:** payment_status  
- **Additional fields:** shipping_delay_days, calculated_sales, calculated_profit, profit_margin, order_month, order_year, data_quality_flag  

The raw dataset was stored in:

```
data/raw_orders.xlsx
```

The cleaned dataset is generated as:

```
outputs/cleaned_orders.xlsx
```

---

## **3. Tools Used**
- **Python 3.12**
- **Pandas** for data cleaning and transformation  
- **NumPy** for numerical operations  
- **dateutil** for universal date parsing  
- **OpenPyXL** for Excel export  
- **Excel** for pivot tables and screenshots  

---

## **4. Cleaning Steps Performed**
### ✔ Text Cleaning
- Trimmed leading/trailing spaces  
- Removed extra internal spaces  
- Standardized case (Title Case / Proper Case)  
- Normalized inconsistent category, region, and ship mode names  
- Removed unwanted characters  

### ✔ Date Cleaning
- Used a universal date parser to handle mixed formats:
  - DD/MM/YYYY  
  - MM/DD/YYYY  
  - YYYY-MM-DD  
  - DD-MMM-YYYY  
- Created standardized fields:
  - `order_date_clean`
  - `ship_date_clean`
- Calculated `shipping_delay_days`
- Flagged:
  - Missing dates  
  - Invalid dates  
  - Ship dates earlier than order dates  

### ✔ Discount Cleaning
- Converted discount to numeric  
- Missing discount → treated as **0** only when sales fields were valid  
- Flagged:
  - Negative discounts  
  - Discounts above allowed range (> 0.8)  

### ✔ Duplicate Handling
- Identified exact duplicate rows  
- Removed exact duplicates (keeping first occurrence)  
- Identified duplicate order IDs  
- Flagged conflicting duplicates for review  
- Summarized:
  - Number removed  
  - Number flagged  

### ✔ Business Rules Applied
- Missing region → filled as **Unknown**  
- Missing ship_mode → filled as **Unknown**  
- Cancelled and failed orders excluded from completed sales  
- Refunded orders tracked separately  
- Invalid shipping records flagged  
- Sales mismatches flagged  

### ✔ Calculated Columns Created
- `cleaned_discount`  
- `calculated_sales`  
- `calculated_profit`  
- `profit_margin`  
- `shipping_delay_days`  
- `order_month`  
- `order_year`  
- `data_quality_flag` (Clean / Warning / Invalid)  

---

## **5. Business Rules Applied**
| Rule Area | Action Taken |
|----------|--------------|
| Missing region | Filled as **Unknown**, flagged |
| Missing ship_mode | Filled as **Unknown**, flagged |
| Missing discount | Treated as 0 only when sales fields valid |
| Negative discount | Flagged as invalid |
| Discount > allowed range | Flagged as invalid |
| Cancelled orders | Excluded from completed sales |
| Failed payments | Excluded from completed sales |
| Refunded orders | Separately summarized |
| Ship date < order date | Flagged as invalid shipping record |

---

## **6. Summary of Data Quality Issues Found**
Based on `outputs/data_quality_report.xlsx`:

- **Missing values:** Found in date fields, region, ship_mode  
- **Invalid discounts:** Negative or > 0.5  
- **Date issues:** Missing dates, invalid formats, ship-before-order  
- **Duplicate issues:**  
  - Exact duplicates removed  
  - Duplicate order IDs flagged  
- **Sales mismatches:** Sales not matching quantity × price × (1 – discount)  
- **Unknown region/ship_mode:** Filled and flagged  
- **Overall data quality:**  
  - Clean records  
  - Warning records  
  - Invalid records  

---

## **7. Summary of Final Pivot Reports**
Generated in `outputs/pivot_summary.xlsx`:

### **Sales & Profit by Region**
- Identifies top‑performing regions  
- Highlights low‑performing or problematic regions  

### **Sales & Profit by Category & Sub‑Category**
- Shows which product lines drive revenue and profit  
- Useful for inventory and marketing decisions  

### **Order Count by Ship Mode**
- Reveals customer shipping preferences  
- Helps evaluate logistics performance  

### **Profit Margin by Customer Segment**
- Shows which segments are most profitable  
- Useful for targeted marketing  

### **Refunded / Cancelled / Failed Orders by Region**
- Highlights operational issues  
- Helps identify regions with high failure/refund rates  

### **Monthly Sales Trend**
- Shows seasonality  
- Helps forecast demand  

---

## **8. Key Business Insights**
- Certain regions consistently outperform others in both sales and profit.  
- Some product sub‑categories contribute disproportionately to total profit.  
- A few regions show high refund/cancellation rates, indicating operational inefficiencies.  
- Customer segments differ significantly in profit margin, suggesting targeted campaigns could improve revenue.  
- Monthly sales trends show seasonality, useful for inventory planning.  

---

## **9. Assumptions and Limitations**
- Discount validity assumed to be between **0 and 0.5**.  
- Sales mismatch threshold set to **0.01** due to rounding.  
- Some ambiguous records were flagged but not corrected.  
- Pivot tables are based on cleaned data; Excel screenshots required for final submission.  
- Universal date parser may interpret ambiguous dates (e.g., 03/04/2024) based on best guess.  

---

## **10. Screenshots Included**
The following screenshots must be included in the `screenshots/` folder:

| Screenshot File | Must Show |
|-----------------|-----------|
| `raw_data_preview.png` | Raw dataset before cleaning |
| `cleaned_data_preview.png` | Cleaned dataset with calculated columns |
| `pivot_summary_1.png` | Sales and profit by region |
| `pivot_summary_2.png` | Sales and profit by category and sub-category |

---


