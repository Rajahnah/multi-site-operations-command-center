# Multi-Site Operations Command Center

### Business Intelligence | Financial Analysis | Operations Strategy

## 1. Project Overview

The Multi-Site Operations Command Center is an interactive Power BI business intelligence solution designed to support executive decision-making across a multi-location retail operation.

The project transforms transactional retail data into actionable financial and operational insights, enabling leadership to evaluate sales performance, profitability, discount utilization, product category performance, operational risk, and data quality.

The solution demonstrates an end-to-end analytics workflow, from raw data preparation and relational modeling to financial analysis, executive reporting, and strategic recommendations.

## 2. Executive Summary

The analysis evaluates 7,151 completed orders across 20 registered retail locations and eight product categories.

| Key Performance Indicator | Result |
|---|---:|
| Gross Sales | 479.47M |
| Net Sales | 436.88M |
| Cost of Goods Sold | 220.42M |
| Gross Profit | 216.46M |
| Gross Profit Margin | 49.55% |
| Discount Impact | 42.59M |
| Effective Discount Rate | 8.88% |
| Order Return Rate | 10.15% |

Key findings include:

- Kochi Market leads registered locations in net sales.
- Lucknow Central achieves the highest gross profit margin among registered locations.
- Bengaluru Central presents a targeted profitability improvement opportunity despite strong sales volume.
- Clothing leads product category sales but operates below the overall gross margin benchmark.
- Books exhibits both low relative sales volume and below-average profitability.
- Approximately 10.15% of completed orders have an associated return record.
- An unmatched StoreID was identified and remediated without removing associated financial activity.

All monetary figures are expressed in unspecified source currency and exclude financial return adjustments.

## 3. Business Objectives

The dashboard was developed to answer the following business questions:

- Which locations generate the highest sales and profitability?
- Which high-volume locations exhibit margin improvement opportunities?
- How do discounts affect realized sales?
- Which product categories contribute most to sales and gross profit?
- Where should leadership prioritize operational investigations?
- What data quality issues could compromise executive reporting?
- What potential financial improvements can be quantified through sensitivity analysis?

## 4. Dataset

Source: [Retail Sales Analysis Dataset](https://github.com/kirthana739/retail-sales-analysis)

The project uses publicly accessible retail transaction data for an independent portfolio case study.

### Data Scope

- 10,000 source orders
- 7,151 completed orders analyzed
- 20 registered retail locations
- 8 product categories
- 5 integrated data tables
- 1,000 source return records
- 10 DAX measures
- 7 executive KPI cards
- 3 interactive analytical charts

### Data Tables

| Table | Purpose |
|---|---|
| stores | Store identification and location attributes |
| orders | Order-level transactions and operational attributes |
| order_items | Product-level quantities and discounts |
| products | Product pricing, costs, and categories |
| returns | Order-level return records and reasons |

## 5. Tools and Technologies

| Technology | Application |
|---|---|
| Power BI Desktop | Interactive dashboard development |
| Power Query | Data extraction, cleaning, and transformation |
| Power Query M | Programmatic data remediation |
| DAX | Financial calculations and analytical measures |
| CSV | Source data ingestion |
| GitHub | Project documentation and version management |
| Financial Modeling | Margin and operational sensitivity analysis |

## 6. Data Preparation and Transformation

The data preparation process included:

1. Importing five relevant CSV datasets into Power BI.
2. Promoting source headers and assigning appropriate data types.
3. Reviewing identifiers and transaction attributes.
4. Investigating date conversion errors.
5. Preserving return records containing invalid dates.
6. Establishing relationships between transaction and reference tables.
7. Applying a completed-order reporting filter.
8. Identifying and resolving an unmatched store identifier.
9. Validating financial KPIs before and after remediation.

The original source files were preserved.

## 7. Relational Data Model

The solution uses a relational model connecting order transactions, order items, products, stores, and returns.

### Model Relationships

| Primary Table | Related Table | Relationship Key |
|---|---|---|
| stores | orders | StoreID |
| orders | order_items | OrderID |
| products | order_items | ProductID |
| orders | returns | OrderID |

The model supports store-level and product-category financial analysis while preserving order-level return attribution.

## 8. DAX Measures and KPI Definitions

### Gross Sales

Gross sales before promotional discounts.

```dax
Gross Sales =
SUMX(
    order_items,
    order_items[Quantity] * RELATED(products[Price])
)
```

### Net Sales

Sales after applying transaction-level discounts.

```dax
Net Sales =
SUMX(
    order_items,
    order_items[Quantity] *
    RELATED(products[Price]) *
    (1 - order_items[Discount])
)
```

### Discount Impact

```dax
Discount Impact =
[Gross Sales] - [Net Sales]
```

### Effective Discount Rate

```dax
Effective Discount Rate =
DIVIDE([Discount Impact], [Gross Sales], 0)
```

### Cost of Goods Sold

```dax
Cost of Goods Sold =
SUMX(
    order_items,
    order_items[Quantity] * RELATED(products[Cost])
)
```

### Gross Profit

```dax
Gross Profit =
[Net Sales] - [Cost of Goods Sold]
```

### Gross Profit Margin

```dax
Gross Profit Margin =
DIVIDE([Gross Profit], [Net Sales], 0)
```

### Total Orders

```dax
Total Orders =
DISTINCTCOUNT(orders[OrderID])
```

### Orders with Returns

```dax
Orders with Returns =
DISTINCTCOUNT(returns[OrderID])
```

### Order Return Rate

```dax
Order Return Rate =
DIVIDE([Orders with Returns], [Total Orders], 0)
```

## 9. Executive Dashboard

The dashboard consolidates financial and operational performance into a centralized executive reporting interface.

### Executive KPIs

- Gross Sales
- Net Sales
- Gross Profit
- Gross Profit Margin
- Discount Impact
- Effective Discount Rate
- Order Return Rate

### Analytical Visualizations

- Gross and Net Sales by Store
- Gross Profit Margin by Store
- Net Sales by Product Category

Interactive visual selections enable location-specific performance analysis and cross-filtering across financial KPIs.

*Final dashboard screenshot will be added following presentation refinements.*

## 10. Business Findings and Strategic Analysis

### Finding 1: Sales Performance Benchmark — Kochi Market

Kochi Market generated the highest net sales among registered locations.

| Metric | Result |
|---|---:|
| Net Sales | 27.10M |
| Gross Profit | 13.86M |
| Gross Profit Margin | 51.17% |
| Effective Discount Rate | 9.07% |
| Order Return Rate | 9.48% |

Its gross profit margin exceeded the overall benchmark by 1.62 percentage points, while its return rate remained 0.67 percentage points below the overall rate.

**Recommendation:** Evaluate Kochi Market as an internal sales performance benchmark and investigate its product mix, pricing, and operational practices.

### Finding 2: Profitability Benchmark — Lucknow Central

Lucknow Central achieved the highest gross profit margin among registered locations.

| Metric | Result |
|---|---:|
| Net Sales | 22.40M |
| Gross Profit | 11.65M |
| Gross Profit Margin | 52.02% |
| Effective Discount Rate | 9.22% |
| Order Return Rate | 9.14% |

Its gross profit margin exceeded the overall benchmark by 2.47 percentage points.

An illustrative sensitivity analysis indicates approximately 10.81M in incremental gross profit if the overall operation achieved a comparable margin at unchanged net sales.

**Recommendation:** Investigate product mix, merchandise costs, and pricing practices to identify potentially scalable profitability improvements.

### Finding 3: High-Volume, Low-Margin Opportunity — Bengaluru Central

Bengaluru Central ranked second in net sales but recorded the lowest gross profit margin among registered locations.

| Metric | Result |
|---|---:|
| Net Sales | 26.20M |
| Gross Profit | 12.29M |
| Gross Profit Margin | 46.92% |
| Effective Discount Rate | 9.01% |
| Order Return Rate | 10.55% |

Its gross profit margin fell 2.63 percentage points below the overall benchmark.

#### Margin Sensitivity Analysis

| Target Gross Margin | Potential Incremental Gross Profit |
|---|---:|
| 49.55% — Overall benchmark | 689K |
| 51.17% — Kochi benchmark | 1.11M |
| 52.02% — Lucknow benchmark | 1.34M |

**Recommendation:** Prioritize a targeted profitability review covering product mix, merchandise costs, pricing, discount utilization, and return patterns.

### Finding 4: Product Category Revenue Driver — Clothing

Clothing emerged as the highest-selling product category.

| Metric | Result |
|---|---:|
| Net Sales | 65.42M |
| Gross Profit | 31.46M |
| Gross Profit Margin | 48.08% |
| Share of Total Net Sales | 14.97% |

Despite its strong sales contribution, Clothing's gross profit margin fell 1.47 percentage points below the overall benchmark.

Achieving the overall gross margin at unchanged net sales represents approximately 962K in potential incremental gross profit.

**Recommendation:** Review merchandise costs, pricing, promotions, and product assortment to identify margin improvement opportunities.

### Finding 5: Product Category Underperformance — Books

Books recorded the lowest net sales among the eight product categories and a substantially below-average gross profit margin.

| Metric | Result |
|---|---:|
| Net Sales | 40.42M |
| Gross Profit | 16.66M |
| Gross Profit Margin | 41.22% |
| Share of Total Net Sales | 9.25% |

Its gross profit margin fell 8.33 percentage points below the overall benchmark.

#### Margin Sensitivity Analysis

| Target Gross Margin | Potential Incremental Gross Profit |
|---|---:|
| 45.00% | 1.53M |
| 48.08% — Clothing benchmark | 2.77M |
| 49.55% — Overall benchmark | 3.37M |

**Recommendation:** Conduct a category profitability review focused on supplier costs, pricing, promotional effectiveness, and assortment before making resource allocation decisions.

### Finding 6: Operational Risk and Returns

| Metric | Result |
|---|---:|
| Completed Orders | 7,151 |
| Orders with Recorded Returns | 726 |
| Orders without Recorded Returns | 6,425 |
| Order Return Rate | 10.15% |

Reducing the return rate to a hypothetical target of 9% at unchanged order volume could result in approximately 82 fewer orders with recorded returns.

**Recommendation:** Investigate return reasons and location-level patterns while improving return-data collection to support financial impact analysis.

## 11. Financial Opportunity Assessment

| Improvement Area | Illustrative Incremental Gross Profit |
|---|---:|
| Overall margin improvement to 52.02% | 10.81M |
| Books category margin improvement | 3.37M |
| Clothing category margin improvement | 962K |
| Bengaluru Central margin improvement | 689K |

### Sensitivity Analysis Methodology

Incremental gross profit is estimated by applying a hypothetical target margin to existing net sales and comparing the result with current gross profit.

These scenarios:

- Assume unchanged net sales.
- Are illustrative rather than predictive.
- Do not establish that target margins are achievable.
- Exclude financial return adjustments.
- May overlap across store and category dimensions.

The opportunities must not be aggregated without further transaction-level analysis.

## 12. Data Quality, Validation and Remediation

### Issue 1: Invalid Return Dates

Five return records contained date conversion errors, representing 0.5% of the 1,000 source return records.

**Resolution:** Replaced invalid dates with null values while retaining the associated return records.

**Business rationale:** Removing these records could understate return activity and distort operational performance reporting.

### Issue 2: Unmatched Store Identifier

Dashboard analysis identified an unexpected blank store category with a gross profit margin of 52.80%.

Investigation revealed:

- The stores table contained 20 registered StoreIDs.
- The orders table contained 21 distinct StoreIDs.
- StoreID S999 had no corresponding store dimension record.

### Financial Activity Associated with S999

| Metric | Result |
|---|---:|
| Gross Sales | 279.43K |
| Net Sales | 226.65K |
| Gross Profit | 119.66K |
| Gross Profit Margin | 52.80% |
| Effective Discount Rate | 18.89% |
| Share of Total Net Sales | Approximately 0.052% |

### Remediation

An explicit Unknown Store dimension record was created using Power Query M.

```powerquery
Table.InsertRows(
    #"Promoted headers",
    20,
    {
        [
            StoreID = "S999",
            StoreName = "Unknown Store",
            City = "Unknown",
            Region = "Unknown",
            StoreType = "Unknown"
        ]
    }
)
```

### Validation Results

- Resolved the blank store classification.
- Preserved the associated transactions.
- Preserved the original source CSV.
- Confirmed that all seven displayed executive KPIs remained unchanged.
- Distinguished unattributed activity from registered operating locations.

Unknown Store represents a data quality classification, not a verified physical location.

## 13. Strategic Recommendations

| Priority | Recommended Action |
|---|---|
| Profitability | Investigate margin drivers within Bengaluru Central |
| Category Performance | Conduct a targeted Books profitability review |
| Revenue Optimization | Evaluate Clothing pricing and merchandise costs |
| Benchmarking | Compare Kochi and Lucknow performance drivers |
| Operational Risk | Investigate return reasons and recurring patterns |
| Data Governance | Implement StoreID validation and exception monitoring |
| Financial Reporting | Improve refund and returned-product data collection |

## 14. Assumptions and Limitations

- Financial reporting is restricted to completed orders.
- Source currency is unspecified.
- Net sales reflect promotional discounts but exclude refund adjustments.
- Gross profit is not equivalent to operating profit or net income.
- Operating expenses are not included.
- Return records do not contain refund amounts, returned quantities, or product-level return attribution.
- Order return rate measures orders with recorded returns rather than units returned.
- Invalid return dates were retained as null values.
- S999 is an unknown dimension member rather than a verified location.
- Performance comparisons are descriptive and do not establish causation.
- Sensitivity analyses are hypothetical and should not be interpreted as forecasts.
- Displayed financial values and derived estimates may reflect rounding.

## 15. Planned Repository Structure

```text
multi-site-operations-command-center/
│
├── README.md
├── dashboard/
│   └── Multi_Site_Operations_Command_Center.pbix
├── screenshots/
│   └── Multi_Site_Operations_Dashboard.png
└── documentation/
    ├── data-model.md
    └── kpi-definitions.md
```

## 16. Future Enhancements

Potential future iterations may include:

- Time-series performance analysis.
- Regional and sales-channel comparisons.
- Product-level profitability analysis.
- Return-reason analysis.
- Automated data quality exception reporting.
- Financial scenario modeling.
- Budget-versus-actual performance tracking.
- Automated data refresh and reporting workflows.

## 17. Professional Competencies Demonstrated

- Business Intelligence and Executive Reporting
- Financial Performance Analysis
- Multi-Site Operations Analytics
- Profitability Optimization
- Financial Sensitivity Analysis
- Relational Data Modeling
- Power Query and DAX
- Data Quality Investigation
- Referential Integrity Remediation
- Operational Risk Assessment
- Strategic Business Recommendations
- Technical Documentation

---

Developed by Rajahnah Matra

Independent Business Intelligence and Operations Analytics Portfolio Project
