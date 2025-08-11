# Microsoft Fabric — Transaction Data Normalization (End-to-End Project)

## 📈 Project Overview

This project demonstrates an **end-to-end data normalization and automation pipeline** in **Microsoft Fabric**, starting from raw transaction data and ending with a fully refreshed semantic model ready for **Power BI** reporting.
[![Watch the Demo Video](https://img.shields.io/badge/Watch%20Video-Click%20Here-red?style=for-the-badge&logo=google-drive)](https://drive.google.com/file/d/1yXWmCN9t5AJxaRMsVk7O3-GSJCL6x-Tm/view?usp=sharing)


The workflow covers:

1. Ingesting raw transaction data into a **Lakehouse**.
2. Normalizing the data into separate, clean dimension and fact tables.
3. Automating ETL processes using **Dataflow Gen2** and **Data Pipelines**.
4. Building and refreshing a semantic model for analytics.

---

## 📂 Dataset Description

The raw transaction dataset contains the following columns:

```
TransactionID | OrderNumber | LineItem | OrderDate | DeliveryDate | Quantity | CustomerID | CustomerGender | CustomerName | CustomerCity | CustomerStateCode | CustomerState | CustomerZip | CustomerCountry | CustomerContinent | CustomerDOB | StoreID | StoreCountry | StoreState | StoreSqMeters | StoreOpenDate | ProductID | ProductName | ProductBrand | ProductColor | ProductCost | ProductPrice | ProductSubcategoryID | ProductSubcategory | ProductCategoryID | ProductCategory
```

The table contains a mix of:

* **Transaction data** (orders, dates, quantities)
* **Customer attributes**
* **Store attributes**
* **Product attributes**

---

## 🛠️ Project Steps
<img width="1010" height="490" alt="image" src="https://github.com/user-attachments/assets/aa8261a3-82c6-4562-8a8d-dc3aa7323695" />

### 1. Lakehouse Creation

* Created a **Lakehouse** in Microsoft Fabric.
* Uploaded the raw transaction file to the **Files** section.

### 2. Dataflow Gen2 (Power Query) — Data Normalization
<img width="821" height="251" alt="query transformationtables" src="https://github.com/user-attachments/assets/86d9ce90-bae1-4c8b-a2f6-797ab8f03f6d" />

* Built a **Dataflow Gen2** using Power Query.
* Split the raw data into **four normalized tables**:

  1. **Transactions** — Fact table for order details.
  2. **Customers** — Dimension table for customer info.
  3. **Products** — Dimension table for product info.
  4. **Stores** — Dimension table for store info.
* Ensured each table contains **unique primary keys** and **no redundant data**.

### 3. Loading into Lakehouse
<img width="203" height="272" alt="tablesnm" src="https://github.com/user-attachments/assets/5c10f048-c976-48a4-995c-aaf51a86d5ee" />

* Each normalized table was loaded into the **Tables** section of the Lakehouse.
* Resulting in a clean **star schema** design.

### 4. Semantic Model Creation
<img width="689" height="394" alt="nmsemantic" src="https://github.com/user-attachments/assets/ca6595cf-ddcf-432f-b673-0d2fa4be33f8" />


* Built a **semantic model** from normalized tables.
* Created a sample measure:

  ```DAX
  Total Sales = SUM(Transactions[Quantity] * Products[ProductPrice])
  ```
* Model is ready to be connected to **Power BI**.

### 5. Automation with Data Pipeline
<img width="745" height="246" alt="nm1" src="https://github.com/user-attachments/assets/288108da-d2cf-477d-a489-43771039a8e7" />

* Created a **Data Pipeline** in Fabric.
* Pipeline triggers on **new file upload** to the Lakehouse.
* Executes:

  1. **Dataflow Gen2** to normalize new data.
  2. **Semantic model refresh** for Power BI.

---

## 📊 Normalization & Database Design

The dataset was normalized according to **1NF, 2NF, and 3NF** principles:

### **First Normal Form (1NF)**

* Removed repeating groups; each field holds atomic values.
* Example: Product attributes moved to a separate **Products** table.

### **Second Normal Form (2NF)**

* Removed partial dependencies from composite keys.
* Example: Customer details depend only on `CustomerID`, stored in **Customers** table.

### **Third Normal Form (3NF)**

* Removed transitive dependencies.
* Example: Store country/state data stored in **Stores** table, not in Transactions.

**Star Schema Structure:**

```
       Customers        Products         Stores
           |               |               |
           +---------------+---------------+
                           |
                     Transactions
```

---

## 🚀 Benefits

* **Eliminates redundancy** — data stored once in respective dimension tables.
* **Boosts performance** for analytics.
* **Simplifies updates** — changes to attributes require single updates.
* **Automated refresh** with no manual intervention.

---

## 📊 Usage Instructions

1. Upload a new transaction file to the Lakehouse.
2. Data Pipeline triggers automatically.
3. Dataflow Gen2 processes and updates normalized tables.
4. Semantic model refreshes and data is instantly available in Power BI.


---

## 🗂️ License

This project is for educational and demonstration purposes.
