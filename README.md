# 🚀 FDE Lab 9 — Data Build Tool (dbt) Project

## 📘 Overview

This lab focuses on building a modular, maintainable, and scalable data transformation pipeline using **dbt (Data Build Tool)**.  
The goal is to transform raw staging data into analytics-ready models for business intelligence and reporting.

The project demonstrates a standard **data warehouse modeling workflow**, consisting of **staging models**, **dimension tables**, and **fact tables**.

---

---

## 🧠 Key Concepts

### 1. **dbt (Data Build Tool)**
dbt enables analysts and engineers to transform data in their warehouses more effectively.  
It handles:
- Modular SQL-based transformations
- Dependency management
- Version control
- Testing and documentation of data models

### 2. **Layers in the Project**
- **Staging Layer (`staging/`)**  
  Cleans, standardizes, and renames raw data from various source systems.
  
- **Mart Layer (`marts/`)**  
  Builds business-level entities and metrics such as dimensions and fact tables for analysis.

---

## 🧩 Model Details

### 🏗️ **Staging Models (`/staging`)**

| File | Description |
|------|--------------|
| `stg_customers.sql` | Prepares cleaned customer data with standardized column names. |
| `stg_employees.sql` | Standardizes employee details and removes duplicates. |
| `stg_offices.sql` | Cleans data related to company offices and locations. |
| `stg_orderdetails.sql` | Joins raw order details with necessary metadata. |
| `stg_orders.sql` | Standardizes order information such as status and dates. |
| `stg_productlines.sql` | Normalizes product line data. |
| `stg_products.sql` | Standardizes product-level data for further joins. |
| `_sources.yml` | Declares data sources, schema, and column-level metadata. |

---

### 📊 **Mart Models (`/marts`)**

| File | Description |
|------|--------------|
| `dim_customers.sql` | Customer dimension table combining customer and location details. |
| `dim_employees.sql` | Employee dimension model enriched with office location data. |
| `dim_offices.sql` | Provides office-level dimension attributes for geographical analysis. |
| `dim_products.sql` | Product dimension model integrating product lines and descriptions. |
| `fact_orders.sql` | Central fact table that joins order, customer, employee, and product data. |

---

## ⚙️ Configuration Files

### **`dbt_project.yml`**
Defines the project name, version, and configurations for model paths, materializations, and seeds.

### **`packages.yml`**
Lists any external dbt packages required by the project.  
Common packages include:
- `dbt_utils` – for macros and testing utilities.
- `dbt_expectations` – for data quality tests.

---

## 🧾 Workflow

### Step 1: Initialize dbt Environment
Make sure dbt is installed and configured:
```bash
pip install dbt-core dbt-postgres
# or for BigQuery / Snowflake users:
# pip install dbt-bigquery
# pip install dbt-snowflake

```
#### ============================================================
### Step 2: Connect to Your Data Warehouse
#### Set up your connection in the `profiles.yml` file 
#### (usually located in `~/.dbt/`)
#### ============================================================

name: 'fde_lab9'
version: '1.0.0'
config-version: 2

#### Define model paths
model-paths: ["staging", "marts"]

#### Define where compiled SQL and target data will be stored
target-path: "target"
clean-targets: ["target", "dbt_modules"]

#### Define models and their materialization
models:
  fde_lab9:
    staging:
      +materialized: view
    marts:
      +materialized: table
#### ============================================================
### Step 3: Run dbt Models
#### Execute the following dbt commands to build and test your data models:
#### ============================================================
```bash
# dbt run          # Runs all models
# dbt test         # Runs tests defined in YAML files
# dbt docs generate
# dbt docs serve   # Opens documentation site in your browser


