# 🏬 RetailStore Analytics Pipeline

A scalable data engineering pipeline for retail analytics, built using **Databricks (PySpark)** for transformations, **Apache Airflow** for orchestration, **Azure Data Lake** for storage layers, and **Azure Synapse Analytics** for data warehousing with a star schema.  

---

## 🚀 Architecture Overview  

### 🔹 Data Flow
1. **Data Ingestion (Bronze Layer)**  
   - Extracted raw data from multiple sources (CSV, API, RDBMS).  
   - Landed into **Azure Data Lake Bronze Layer** as-is.  

2. **Data Transformation (Silver Layer)**  
   - Accessed Bronze data inside **Databricks**.  
   - Applied **cleaning, standardization, and enrichment** using **PySpark**.  
   - Stored curated data in **Azure Data Lake Silver Layer**.  

3. **Data Modeling (Gold Layer)**  
   - Further transformed Silver data into **fact and dimension tables** (star schema) within Databricks.  
   - Stored processed outputs in the **Azure Data Lake Gold Layer**.  

4. **Data Warehousing**  
   - Loaded **Gold Layer** data into **Azure Synapse Analytics** via **PolyBase**.  
   - Designed **Star Schema** for optimized BI queries.  

5. **BI & Reporting**  
   - Exposed data to **Power BI / reporting tools** for insights.  

---

## 🔄 Orchestration  
- **Apache Airflow** orchestrates Databricks notebooks in 3 stages:  
  1. **Extract** → Load raw data to Bronze.  
  2. **Transform** → Process Bronze → Silver.  
  3. **Load** → Silver → Gold → Synapse.  

---

## 📊 Pipeline Diagram  

The solution follows the **Medallion Architecture** (Bronze → Silver → Gold) with **Azure Synapse Analytics** as the serving layer.

```mermaid
flowchart TD
    A[Raw Retail Data] -->|Ingest| B[Azure Data Lake - Bronze]
    B -->|Clean + Standardize| C[Azure Data Lake - Silver]
    C -->|Aggregate + Enrich| D[Azure Data Lake - Gold]
    D -->|PolyBase Load| E[Azure Synapse Analytics - Star Schema]
    E -->|BI Queries| F[Power BI / Reports]

    subgraph Orchestration
        O[Apache Airflow]
    end
    
    subgraph Processing
        P[Databricks - PySpark]
    end

    O --> B
    O --> C
    O --> D
    P --> C
    P --> D
