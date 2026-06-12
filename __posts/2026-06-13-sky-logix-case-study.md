---
layout: post
title: 'Case Study: Building SkyLogix Weather Data Pipeline'
date: 2026-06-13
categories: data-engineering python
---

# Case Study: Building SkyLogix — An End-to-End Weather Data Pipeline

## Executive Summary
In modern data architecture, handling external API ingestions requires balancing volatile, unstructured payloads with the need for rigid, analytics-ready data structures. 

**SkyLogix** is a modular ETL (Extract, Transform, Load) data pipeline built to bridge this gap. The system automates the ingestion of global weather metrics from a live third-party API, secures the raw data in an unstructured landing zone, normalizes the nested payloads, and loads them into a structured relational warehouse optimized for downstream business intelligence.

---

## The Architecture & Design Strategy

When designing data infrastructure, a common pitfall is writing raw API data straight into a relational database. If the API schema changes unexpectedly, downstream tables break. 

To solve this, I implemented a **Dual-Database Architecture** using a specialized four-stage ETL workflow:

![SkyLogix Weather Data Pipeline Architecture](images/weather_skylogix_pipeline.png)

### 1. Extract (`weather_client.py`)
The pipeline triggers an authenticated request to the external weather API to capture real-time global metrics. To ensure production standards, this component isolates API credentials using secure environment variables.

### 2. Load - Raw Landing Zone (`ingest_weather.py` & `mongo_client.py`)
Instead of transforming data on the fly, the raw, deeply nested JSON response is immediately backed up into **MongoDB**. 
* **The "Why":** MongoDB acts as a durable landing zone (Data Lakehouse concept). If a downstream transformation fails, we never lose the historical raw data and can re-run pipelines without making repetitive, costly API calls.

### 3. Transform - Normalization Layer (`normalize.py`)
Once safely stored, the transformation script extracts the raw JSON documents from MongoDB. It flattens the nested structures, handles missing data points, enforces correct data types (such as timestamps and floats), and prepares clean, flat records.

### 4. Load - Analytical Warehouse (`ingest_pg.py`)
The clean, normalized metrics are written into a **PostgreSQL** relational database. 
* **The "Why":** PostgreSQL serves as the single source of truth for analytical queries, reporting, and BI tools, ensuring fast aggregations and strict schema enforcement.

---

## Project Structure & Component Breakdown

The codebase is engineered with strict modularity, separating operational orchestration from core infrastructure clients:

* **`main.py`**: The central execution brain that sequences the entire pipeline from end to end.
* **`src/`**: The core package housing individual ETL modules (`weather_client`, `mongo_client`, `normalize`, `ingest_pg`).
* **`.env.example`**: Ensures smooth onboarding for other engineers by detailing required infrastructure keys without exposing secrets.
* **`.exp.ipynb`**: Kept as a development scratchpad for prototyping API payloads and mapping database connections before promotion to production scripts.

---

## Key Technical Takeaways & Engineering Challenges

### Overcoming Data Volatility
API payloads are inherently unpredictable. By decoupling the extraction phase from the transformation phase via MongoDB, the pipeline achieves high fault tolerance. If the schema changes tomorrow, the data collection doesn't stop; we simply update `normalize.py` to handle the new fields.

### Production Environment Safety
Strict separation of environments was maintained. Utilizing a robust `.gitignore` strategy guarantees that active database strings, local paths, and API tokens are never leaked to public repositories, aligning with modern security compliance.

---

## How to Explore the Project

The complete code, schema definitions, and instructions on how to spin up this infrastructure locally are open-sourced on GitHub.

👉 [**View the Full Codebase on GitHub**](https://github.com/Oyetoluzeenat/weather_skylogix_zeenat)