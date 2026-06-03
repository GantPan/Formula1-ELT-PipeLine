# Formula 1 End-to-End Data Engineering Pipeline

## Project Overview
This project is an End-to-End ELT (Extract, Load, Transform) data pipeline built in **Databricks**
It automatically ingests Formula 1 race data, processes telemetry and weather information,
and feeds a dynamic AI/BI Dashboard for race strategy analysis.

## Teck Stack
- Environment: Databricks, Apache Spark
- Languages: Python, SQL
- Libraries: FastF1, Pandas, PySpark
- Data Storage: Delta Lake (Bronze & Silver Architecture)
- Visualization: Databricks AI/BI Dashboards

## Pipeline Architecture
1. Data Ingestion (Extract): Utilizes the `fastf1` API to extract live session data, lap times, and weather conditions.
2. Raw Layer (Bronze): Implements a time-series merge (`merge_asof`) to synchronize lap times with weather data and stores it in a Delta table.
3. Cleaning & Transformation (Silver): Uses SQL to handle data anomalies (e.g. converting DNF '0' positions to `NULL` for accurate visualization) and creates the final optimized dataset.
4. Visualization: A Databricks Dashboard with Global Filters allowing dynamic driver comparison.

## Dashboard Preview
`[F1 Dashboard](F1 DASHBOARDS ALL.png)`

## Key Challenges Solved
- API Latency & Timeout: Implemented a local caching strategy (`/tmp/`) and disabled redundant telemetry data, reducing API load time from several minutes to under 5 seconds.
- Data Integrity: Used SQL `CASE WHEN` statements to clean `NaN` anomalies from driver retirements, ensuring charting accuracy.
