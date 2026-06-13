---
layout: post
title: 'Case Study: Optimizing an Enterprise Medallion Data Warehouse for Telecom Analytics'
date: 2026-06-13
categories: data-engineering bigquery python
permalink: /portfolio/datatel-communication-pipeline/
---

# Case Study: Building DataTel — An End-to-End Enterprise Medallion Data Warehouse

## Executive Summary
In high-volume telecommunications architectures, data engineering pipelines must reconcile a critical friction point: capturing massive streams of volatile, unstructured transactional records (customer profiles, high-frequency network usage sessions, and dynamic billing logs) and converting them into high-performance, strictly governed business intelligence assets. 

**DataTel Communication Analytics Pipeline** is an enterprise-grade ETL data infrastructure built to solve this problem. The system isolates raw, unstructured operational ingestion data, normalizes it using a structured four-stage **Medallion Architecture** inside **Google BigQuery**, enforces complete type-safety through **Python validation layers**, and materializes optimized analytics matrices that empower downstream corporate leadership to track financial metrics and churn indicators with zero compute overhead.

---

## System Architecture & Data Flow

A common anti-pattern in cloud analytics is querying raw landing zones directly or running heavy joins across unstructured fields inside production tables. This introduces significant computing costs and query latency. 

To bypass this bottleneck, DataTel decouples operational capture from business logic using a specialized, multi-stage ingestion and transformation architecture:

![DataTel Communication Analytics Pipeline Architecture](/images/datatel_comm_pipeline.png)

### 1. Ingestion & Operational Data Capture
The operational environment simulates real-world transaction layers. Raw subscriber data, mobile/data network sessions, and transaction events are generated and processed through `ingestion/ingest_pg.py` into a transactional relational layer (PostgreSQL). This preserves the integrity of the transactional systems while preparing raw assets for cloud staging.

### 2. Bronze Layer: Immutable Land Zone (`data_tel_bronze`)
The master orchestration controller triggers extraction loops that stream flat files out of the operational layer and load them as raw logs into Google BigQuery. 
* **Design Strategy:** The tables `src_customers`, `src_billing_transactions`, and `src_network_sessions` serve as a durable, historical log. No schema changes or transformation rules are applied at this stage; if an upstream pipeline breaks, the raw historical backup remains safely intact.

### 3. Silver Layer: Processing & Cleansing (`data_tel_silver`)
Managed by `scripts/pipeline.py`, the transformation engine reads from the Bronze tables to apply strict type casting, structural string trimming, timestamp standardization, and de-duplication rules.
* **SQL Realization:** Staging views (`stg_customers.sql`, `stg_sessions.sql`) strip null fields, convert network bytes into usable megabytes, and append high-water mark logs incrementally using `stg_billing_inc.sql` to avoid reprocessing duplicate historical billing statements.

### 4. Gold Warehouse Layer: Structured Enterprise Modeling (`data_tel_gold`)
The polished staging records are joined and structured into an analytical core. The system materializes performant, pre-aggregated tables (`sql/gold_metrics/`) tracking key corporate indices:
* **`dw_user_analytics.sql`**: A unified, comprehensive analytics matrix that merges customer dimensions, aggregate byte consumption, and billing histories into a singular, wide-reporting table optimized for hyper-fast querying.
* **Aggregated KPIs**: Scripts like `agg_arpu.sql` and `agg_monthly_revenue.sql` continuously compute performance layers, preparing the data for instant reporting pipelines.

---

## Repository Workspace Structure

The project code maintains a strict separation of concerns, ensuring python script handlers dictate orchestration, while Google Cloud compute resources process the core transformation data using highly optimized BigQuery Standard SQL:

![DataTel Project Repository Structure Map](/images/repository_structure.png)

* **`main.py`**: The central workflow brain that sequentially boots up the pipeline, monitors status, and verifies end-to-end execution.
* **`validate.py`**: A specialized data-quality assurance script that tests data freshness, schema alignments, and active database connection handshakes before allowing code execution.
* **`scripts/bigquery_orchestrator.py`**: An automated engine that programmatically parses the logical lineage order of the SQL scripts and executes them across the BigQuery console.

---

## Business Intelligence & Execuitve Insights

The final design choice of this infrastructure is routing the polished Gold layer metrics straight into an executive visual command center, bridging the gap between low-level data engineering and top-tier business decisions.

![Looker Studio Business Intelligence Dashboard](/images/looker_studio_dashboard.png)

By surfacing the materialization tables in **Google Looker Studio**, non-technical stakeholders can interact with live system insights on-demand:
1. **Financial Health Tiles:** Displays live global performance indicators like *Total Lifetime Revenue (LTV)* and *Active User Base Growth* metrics.
2. **Customer Segmentation Grid:** Automatically splits subscribers into high-value, mid-tier, and entry-level cohorts using custom SQL quantiles, allowing product managers to protect high-revenue contracts.
3. **Maturity-Guarded Churn Tracker:** A defensive alert monitor that maps active network session drops over time, isolating accounts showing high decay patterns while filtering out fresh, un-matured user profiles.

---

## Key Technical Takeaways

* **Compute Offloading:** By shifting all cleansing, tracking, and transformation sequences into BigQuery Standard SQL, the infrastructure harnesses the massive scaling power of Google’s serverless compute engine.
* **Production Security Alignment:** Operational credentials, GCP service account paths, and production connection strings are fully isolated into environment-specific variable systems (`tel.env`). The `.gitignore` config completely shields underlying authorization tokens from ever hitting public codebases.

## How to Explore the Project

The complete code, schema definitions, and instructions on how to spin up this infrastructure locally are open-sourced on GitHub.

👉 [**View the Full Codebase on GitHub**](https://github.com/Oyetoluzeenat/datatel_comm_analytics_pipeline)