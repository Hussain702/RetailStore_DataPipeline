# 🛍️ RetailStore Analytics Pipeline

An **end-to-end cloud data engineering project** for retail sales analytics.  
This pipeline transforms raw retail data into **analytics-ready insights** using modern data engineering tools and **Azure cloud services** following the **Medallion Architecture** (Bronze → Silver → Gold).

---

## 📌 Architecture Overview

```mermaid
flowchart TD
    A[📂 Raw Retail Data] -->|Ingest| B[🌊 Azure Data Lake - Bronze]
    B -->|Clean + Standardize| C[🌊 Azure Data Lake - Silver]
    C -->|Aggregate + Enrich| D[🌊 Azure Data Lake - Gold]
    D -->|Load| E[🗄️ Azure Synapse Analytics]
    E -->|BI Queries| F[📊 Power BI / Reports]

    subgraph Orchestration
        O[⏱️ Apache Airflow]
    end
    
    subgraph Processing
        P[⚡ Apache Spark / PySpark]
    end
    
    O --> B
    O --> C
    O --> D
    P --> C
    P --> D
