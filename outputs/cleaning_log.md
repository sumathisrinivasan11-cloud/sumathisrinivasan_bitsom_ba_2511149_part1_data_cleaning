# Cleaning Log

## Issues Found
- Inconsistent text formatting
- Mixed date formats
- Invalid discounts
- Sales mismatches
- Duplicate rows and duplicate order IDs
- Missing region/ship_mode

## Cleaning Actions Performed
- Standardized text fields
- Parsed and validated dates using universal parser
- Cleaned discount values
- Recomputed sales and profit
- Removed exact duplicates
- Flagged conflicting duplicates

## Business Rules Applied
- Missing region/ship_mode → Unknown
- Missing discount → 0 when valid
- Negative/too-high discounts flagged
- Cancelled/failed excluded from completed sales
- Refunded orders tracked separately
- Ship date before order date flagged

## Records Removed
- Exact duplicates removed: 20

## Records Flagged
- Duplicate order IDs flagged: 31

## Limitations
- Some ambiguous records flagged but not corrected
