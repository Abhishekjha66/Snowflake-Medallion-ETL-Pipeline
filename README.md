# Snowflake Medallion ETL Pipeline

An end-to-end data transformation project built using **Snowflake SQL** and the **Medallion Architecture (Bronze, Silver, Gold)**.

This project demonstrates how raw sales data can be ingested, cleaned, transformed, aggregated, and monitored through scheduled Snowflake tasks.

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
- Filters null and invalid records.
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

Both tasks were verified through task execution history.

## SQL Scripts

| File | Description |
|---|---|
| `01_environment_setup.sql` | Database, schemas, and warehouse setup |
| `02_bronze_table_setup.sql` | Bronze schema context and table inspection |
| `03_transform_silver.sql` | Silver transformation logic |
| `04_transform_gold.sql` | Gold aggregation logic |
| `05_create_tasks.sql` | Scheduled task definitions |
| `06_monitoring.sql` | Task execution monitoring |

## Verified Pipeline Results

| Layer | Table | Verified records |
|---|---|---:|
| Bronze | `RAW_SALES` | 15 |
| Silver | `CLEAN_SALES` | 12 |
| Gold | `SALES_SUMMARY` | 5 product groups |

### Gold Output

| Product | Total Sales | Total Revenue |
|---|---:|---:|
| Keyboard | 1 | 3,000 |
| Laptop | 4 | 220,000 |
| Mouse | 1 | 1,200 |
| Phone | 4 | 100,000 |
| Tablet | 2 | 36,000 |

*Results from the verified project dataset.*

## Key Learning Outcomes

- Implementing the Medallion Architecture.
- Writing SQL transformations in Snowflake.
- Data cleaning and deduplication.
- Building aggregated reporting tables.
- Automating ETL workflows using Snowflake Tasks.
- Monitoring scheduled task execution.

## Project Status

The Bronze, Silver, and Gold tables were populated and verified. Scheduled task execution was also tested, with successful Silver and Gold task runs visible in execution history.

---

**Developed as a hands-on data engineering project using Snowflake.**
