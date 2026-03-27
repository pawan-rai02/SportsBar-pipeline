# Quick Reference Guide

## SportsBar Data Pipeline - Quick Start

### 📁 Project Structure

```
SportsBar-pipeline/
├── code/           # Python scripts for ETL
├── data/           # Source data files
├── docs/           # Documentation & reports
├── images/         # Diagrams & visuals
├── README.md       # Full documentation
└── QUICKSTART.md   # This guide
```

---

## 🚀 Quick Start

### 1. Upload Notebooks to Databricks

**Option A: Using Databricks UI**
- Go to **Workspace** → **Create** → **Folder** → `SportsBar`
- Upload all `.py` files from `code/` folder

**Option B: Using Databricks CLI**
```bash
databricks workspace import_dir ./code /Workspace/SportsBar/code
```

### 2. Run Setup Scripts (in order)

1. `code/setup/setup_catalog.py` - Create Unity Catalog structure
2. `code/setup/dim_date_table_creation.py` - Create date dimension

### 3. Run Data Pipeline

**Dimension Processing:**
1. `code/dimension_data_processing/1_customer_data_processing.py`
2. `code/dimension_data_processing/2_products_data_processing.py`
3. `code/dimension_data_processing/3_pricing_data_processing.py`

**Fact Processing:**
1. `code/fact_data_processing/1_full_load_fact.py`
2. `code/fact_data_processing/2_incremental_load.py`

---

## 📊 Pipeline Overview

```
Bronze (Raw) → Silver (Cleansed) → Gold (Analytics) → Dashboard
```

---

## 🔧 Common Commands

### Run Full Pipeline
```python
# In Databricks notebook
%run /Workspace/SportsBar/code/setup/setup_catalog
%run /Workspace/SportsBar/code/dimension_data_processing/1_customer_data_processing
%run /Workspace/SportsBar/code/dimension_data_processing/2_products_data_processing
%run /Workspace/SportsBar/code/dimension_data_processing/3_pricing_data_processing
%run /Workspace/SportsBar/code/fact_data_processing/1_full_load_fact
%run /Workspace/SportsBar/code/fact_data_processing/2_incremental_load
```

### Check Data Quality
```sql
-- Row counts
SELECT COUNT(*) FROM bronze.parent_company_orders;
SELECT COUNT(*) FROM silver.dim_customer;
SELECT COUNT(*) FROM gold.fact_orders;

-- Data freshness
SELECT MAX(load_date) FROM gold.fact_orders;
```

---

## 📧 Contact & Support

- **Documentation:** See `README.md` for full details
- **Report Author:** Pawan Kumar Rai

---

## 🔗 Quick Links

- [Databricks Docs](https://docs.databricks.com/)
- [Delta Lake Docs](https://docs.delta.io/)
- [Unity Catalog Guide](https://docs.databricks.com/data-governance/unity-catalog/)

---

*For detailed information, see the full README.md*
