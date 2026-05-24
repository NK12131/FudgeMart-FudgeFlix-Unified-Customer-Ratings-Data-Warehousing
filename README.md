# FudgeMart & FudgeFlix — Unified Customer Ratings Data Warehouse

> Star schema data warehouse integrating 3,407 customer ratings across retail (FudgeMart) and streaming (FudgeFlix) platforms. Built with Snowflake, dbt, and Power BI. Achieved 99% data integrity across merged dimensions and facts.

![Snowflake](https://img.shields.io/badge/Snowflake-29B5E8?style=flat&logo=snowflake&logoColor=white)
![dbt](https://img.shields.io/badge/dbt-FF694B?style=flat&logo=dbt&logoColor=white)
![Power BI](https://img.shields.io/badge/Power_BI-F2C811?style=flat&logo=powerbi&logoColor=black)
![MSSQL](https://img.shields.io/badge/MSSQL-CC2927?style=flat&logo=microsoftsqlserver&logoColor=white)

---

## Overview

This project integrates customer feedback data from two distinct business domains **FudgeMart** (retail e-commerce) and **FudgeFlix** (streaming service) into a unified data warehouse for comprehensive customer analytics. The integration enables cross-platform insights into customer behavior, preferences, and ratings.

**Author:** Nithin Kumar Hadhge Girish Kumar  
---

## Key Metrics

| Metric | Value |
|--------|-------|
| Total Ratings Integrated | 3,407 |
| Total Items Unified | 7,238 |
| Customers Merged | 60 |
| Data Integrity | 99% |
| Date Range | 1970–2019 |

---

## 01 — Star Schema Design

### Dimensions

**DIM_CUSTOMER** — 60 customers merged
- FudgeMart: 25 customers
- FudgeFlix: 35 customers
- Common attributes: customer_id, name, location

**DIM_ITEM** — 7,238 items unified
- FudgeMart products: 53
- FudgeFlix titles: 7,185

**DIM_DATE**
- Date range: 1970–2019
- Standard date dimension attributes

### Facts

**FACT_CUSTOMER_RATINGS** - 3,407 rows
- FudgeMart: 1,039 ratings
- FudgeFlix: 2,368 ratings

**OBT_FACT_CUSTOMER_RATINGS** — 3,407 rows
- One Big Table implementation for simplified querying

> **Key Assumption:** Queue Date in FudgeFlix was mapped to Review Date to align with FudgeMart's rating timestamp.

---

## 02 — ETL Pipeline

```
MSSQL Source → Extract → dbt Transform → Snowflake DWH → Power BI
(FudgeMart · FudgeFlix)   (Raw pull)    (Modeling + QA)  (Star schema)   (Dashboards)
```

---

## 03 — Tech Stack

| Tool | Role |
|------|------|
| **Snowflake** | Target data warehouse cloud-native analytics |
| **dbt** | ETL transformations, data quality checks, Git-versioned |
| **Power BI** | Interactive dashboards with drill-down analysis |
| **MSSQL** | Source databases for both platforms |
| **Git** | Version control for all transformations |

---

## 04 — Analytics & Insights

### Analyses Performed

- **Average Rating by Year**: Temporal trend analysis of customer satisfaction
- **Average Rating by Category**: Product/content category performance comparison
- **Total Ratings by Customer**: Customer engagement and power user identification
- **Total Ratings by Item Type**: Distribution across products vs. streaming content

### Power BI Dashboards

- **FudgeFlix Customer Feedback Analysis**: Streaming content insights
- **FudgeMart Customer Feedback Analysis**: Product rating insights
- **Unified Cross-Platform View**: Customer engagement metrics across both platforms

---

## 05 — Data Quality Recommendations

**R1 — Add Source Identifier**  
Include a platform origin flag (FudgeMart / FudgeFlix) in every table to enable clean source-system tracking.

**R2 — Enhanced Item Classification**  
Add a `type_genre` attribute to the Item dimension for richer content and product categorization.

**R3 — Rating Constraints**  
Enforce a minimum rating value of 1 in FudgeFlix to prevent null or zero-value entries from skewing analysis.

**R4 — Location Enhancement**  
Expand FudgeFlix customer location fields to include city, country, and region reducing sole reliance on postal code.

---

## 06 — Project Outcomes

- Successfully merged two disparate data sources
- Created unified customer feedback analytics platform
- Delivered actionable insights for business stakeholders
- Established scalable ETL pipeline for ongoing integration
- Achieved 99% data integrity across migration

---
