
# Snowflake Medallion ETL Pipeline

An end-to-end data transformation project built using **Snowflake SQL** and the **Medallion Architecture (Bronze, Silver, Gold)**.

The project demonstrates how raw sales data can be organized, cleaned, transformed, aggregated, and monitored through scheduled Snowflake tasks.

## Architecture

```text
        Raw Sales Data
              |
              v
      +---------------+
      | Bronze Layer  |
      |   RAW_SALES   |
      +---------------+
              |
              v
      +---------------+
      | Silver Layer  |
      |  CLEAN_SALES  |
      +---------------+
              |
              v
      +---------------+
      |  Gold Layer   |
      | SALES_SUMMARY |
      +---------------+
              |
              v
       Business Insights
```

## Technology Stack

- Snowflake
- Snowflake SQL
- Medallion Architecture
- Snowflake Virtual Warehouse
- Snowflake Scheduled Tasks

## Data Pipeline

### 1. Bronze Layer
Stores raw sales data in the `RAW_SALES` table.

### 2. Silver Layer
Cleans and transforms raw data:
- Trims customer and product values.
- Filters invalid or null records.
- Removes duplicate sales records.
- Retains the latest record for each sale ID.

### 3. Gold Layer
Creates business-level sales summaries:
- Total sales by product.
- Total revenue.
- Average sale amount.

## Automation

The pipeline uses Snowflake Tasks:

- `SILVER_DAILY_TASK` runs daily at **8:00 AM IST**.
- `GOLD_DAILY_TASK` runs after the Silver task succeeds.

## SQL Scripts

| File | Description |
|---|---|
| `01_environment_setup.sql` | Database, schemas, and warehouse setup |
| `02_load_bronze.sql` | Bronze schema context and table inspection |
| `03_transform_silver.sql` | Silver transformation logic |
| `04_transform_gold.sql` | Gold aggregation logic |
| `05_create_tasks.sql` | Scheduled task definitions |
| `06_monitoring.sql` | Task execution monitoring |

## Sample Gold Output

| Product | Total Sales | Total Revenue |
|---|---:|---:|
| Laptop | 2 | 110000 |
| Phone | 2 | 50000 |
| Tablet | 1 | 18000 |

*Sample results from the project dataset.*

## Key Learning Outcomes

- Implementing the Medallion Architecture.
- Writing SQL transformations in Snowflake.
- Data cleaning and deduplication.
- Building aggregated reporting tables.
- Automating ETL workflows using Snowflake Tasks.
- Monitoring scheduled task execution.

## Project Status

The Bronze, Silver, and Gold tables were populated and verified. Scheduled task execution was also tested.

---

**Developed as a hands-on data engineering project using Snowflake.**
