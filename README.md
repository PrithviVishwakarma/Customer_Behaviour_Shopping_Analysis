# Customer Shopping Behavior: End-to-End Analytics Pipeline

An end-to-end data engineering and analytics project that processes retail consumer behavior data to uncover actionable business insights. This repository demonstrates a complete data lifecycle workflow: moving from raw unstructured text files, cleaning and programmatically engineered data via Python, loading schemas into a local relational MySQL instance, and running optimized SQL analytics to isolate high-value revenue drivers.

## 🛠️ Tech Stack & Prerequisites
* **Programming Languages:** Python, SQL
* **Core Libraries:** Pandas, SQLAlchemy, PyMySQL, MySQL-Connector
* **Database Engine:** MySQL Server
* **IDE/Environment:** VS Code / Jupyter Notebook

---

## 📂 Repository Components

* **`customer_shopping_behavior.csv`**: The primary retail dataset containing 3,900 rows tracking consumer demographic information (age, gender, location), transaction granularities (category, item, prices), and purchase behaviors (frequencies, ratings).
* **`customer_shopping_behavior.ipynb`**: A robust Jupyter notebook housing the programmatic ETL pipeline used to clean and structure raw data before database migration.
* **`customer_shopping_behavior.sql`**: A production-ready script containing optimized analytical queries targeting 10 critical retail business objectives.

---

## ⚙️ Data Engineering & Pipeline Breakdown (`customer_shopping_behavior.ipynb`)

The data pipeline standardizes and expands the raw data structure through the following programmatic operations:

1. **Handling Missing Values:** Identifies missing categorical attributes in product reviews and dynamically imputes `review_rating` elements based on the median rating within that item's specific retail category.
2. **Schema Normalization:** Sanitizes structural syntax across all elements by mapping column headers to a clean `snake_case` lowercase naming convention.
3. **Feature Engineering:**
   * **`age_group`**: Converts raw continuous numerical ages into structured demographic cohorts (`Young Adult`, `Adult`, `Middle-aged`, `Senior`) using quartile categorization.
   * **`purchase_frequency_days`**: Maps custom text strings (e.g., *Fortnightly*, *Weekly*, *Quarterly*) into definitive numeric values representing standardized intervals of days to enable mathematical timeline analysis.
4. **Relational Database Migration:** Establishes connection endpoints locally utilizing an active `SQLAlchemy` database engine combined with a `PyMySQL` driver dialect to format and push clean datasets directly into a relational table.

---

## 📊 Analytics Deep Dive (`customer_shopping_behavior.sql`)

The repository includes strategic SQL queries addressing critical business questions to provide actionable insights for retail managers:

| Query Focus | Objective | SQL Techniques Applied |
| :--- | :--- | :--- |
| **Q1. Revenue Breakdown** | Calculate total sales performance across individual gender categories. | `SUM()`, `GROUP BY` |
| **Q2. Premium Discounter Filter** | Isolate customers utilizing active discounts whose purchase values still exceed average storefront prices. | Subqueries, Conditional `WHERE` |
| **Q3. Top-Tier Items** | Identify the top 5 individual products maintaining the highest average consumer review scores. | `AVG()`, `ROUND()`, `ORDER BY DESC` |
| **Q4. Shipping Logistics** | Compare transaction sizes relative to standard vs. express delivery formats. | Aggregations with explicit string filters |
| **Q5. Subscription ROI** | Evaluate whether subscribed rewards programs increase customer spending and overall revenue streams. | Multi-column groupings, `COUNT()` calculations |
| **Q6. Discount Susceptibility** | Track products with the highest percentage of discount usage to pinpoint promo-driven sales. | `SUM(CASE WHEN...)` flag mapping |
| **Q7. Cohort Separation** | Classify accounts into distinct tiers (`New`, `Returning`, `Loyal`) based on lifetime order volumes. | Common Table Expressions (CTEs), `CASE WHEN` |
| **Q8. Category Top Sellers** | Dynamically locate the top 3 best-selling product items restricted inside each unique market domain. | Window Functions (`ROW_NUMBER() OVER(PARTITION BY...)`) |
| **Q9. Loyalty Convergence** | Cross-reference repeat buyers to check if frequent shopping correlates with formal premium subscription adoption. | Multi-factor filtering criteria |
| **Q10. Age Contribution** | Analyze total generated revenue across specific engineered target age groups. | Aggregate cross-sections with engineered groups |

---

## 🚀 Step-by-Step Execution Guide

### 1. Database Initialization
Open your local MySQL instance (via command-line or MySQL Workbench) and initialize your database environment:
```sql
CREATE DATABASE customer_behavior;
