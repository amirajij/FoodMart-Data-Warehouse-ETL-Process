# FoodMart Data Warehouse - ETL Process

This project implements the **Extract, Transform, and Load (ETL)** process for the FoodMart Data Warehouse. Using **Pentaho Data Integration (PDI)**, data was integrated from the "Pegasus" operational system and external files to populate a dimensional model (Star Schema) for business analysis.

---

## Project Goals
* Extract raw data from a legacy operational system (Pegasus).
* Cleanse and transform data to ensure consistency.
* Implement **Slowly Changing Dimensions (SCD)** to manage historical data.
* Load optimized tables into the **FoodMartDW** for analytical reporting.

---

## Technology Stack
* **Pentaho Data Integration (Spoon):** Core ETL tool.
* **MySQL / Oracle (SQL):** Database management.
* **SCD Techniques:** Types 1 and 2 implemented.

---

## ETL Pipeline Overview

### 1. Customer Dimension (`D_Customer`)
* **Technique:** **SCD Type 1** (Overwrite).
* **Logic:** Since history is not required for customers, the flow uses the `Dimension Lookup/Update` step to compare the `ChangeDateTime` field and update records directly.

### 2. Product Dimension (`D_Product`)
* **Technique:** **SCD Type 2** (Version History).
* **Logic:** Designed to preserve historical changes in price and categories. New versions of products are created whenever critical attributes change.

### 3. Time Dimension (`D_Time`)
* Automated generation of time hierarchies (Year, Quarter, Month, Day) to allow granular temporal analysis in the Data Warehouse.

### 4. Sales Fact Table (`F_Sales_Month`)
* **Logic:** Aggregates sales data on a monthly basis.
* Uses **Database Lookups** to map natural keys from source systems to surrogate keys in the dimensions.

---

## 📂 Repository Structure
* `ktr`: Pentaho transformation files (`.ktr`).
* `docs`: Project documentation and requirements (PDF/Docx).

---

## How to Run
1.  Install **Pentaho Data Integration (Spoon)**.
2.  Set up the source database (Pegasus) and the target database (FoodMartDW).
3.  Configure the database connections in Spoon.
4.  Run the transformations in order: Dimensions first, then Fact tables.
