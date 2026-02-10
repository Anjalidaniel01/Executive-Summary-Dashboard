# Executive-Summary-Dashboard
Executive sales summary built using MySQL stored procedures and ODBC connectivity for reusable, scalable reporting.
## 📌 Overview

This project demonstrates how to build an **executive-level sales summary** using a **MySQL stored procedure** and connect the database to external reporting tools using an **ODBC connector**.

The main objective is to centralize business logic inside the database and reuse it efficiently for reporting and analytics.

---

## 🛠️ Technologies Used

* **MySQL**
* **SQL**
* **Stored Procedures**
* **ODBC Connector**
* **Database Connectivity for BI Tools**

---

## Database & Table

**Database:** `practice`
**Table:** `salessummary`

### Table Columns

| Column Name   | Description                |
| ------------- | -------------------------- |
| Region        | Sales region               |
| TotalRevenue  | Actual revenue             |
| TargetRevenue | Planned/target revenue     |
| ProjectDelays | Number of delayed projects |
| ActiveDeals   | Active deals in pipeline   |

---

## 🔄 Project Flow

### 1️⃣ Data Insertion

Sales data was first inserted into the MySQL table:

```sql
SELECT * FROM practice.salessummary;
```

This step confirms that the data is successfully loaded.

---

### 2️⃣ Stored Procedure Creation

A stored procedure named **`usp_ExecutiveSummary`** was created to aggregate key metrics by region.

```sql
DELIMITER $$

CREATE PROCEDURE usp_ExecutiveSummary()
BEGIN
    SELECT 
        Region,
        SUM(TotalRevenue) AS Revenue,
        SUM(TargetRevenue) AS Target,
        SUM(ProjectDelays) AS DelayedProjects,
        SUM(ActiveDeals) AS ActivePipeline
    FROM SalesSummary
    GROUP BY Region;
END $$

DELIMITER ;
```

---

### 3️⃣ Execute Stored Procedure

The stored procedure is executed using:

```sql
CALL usp_ExecutiveSummary();
```

This returns a summarized regional sales view.

---

### 4️⃣ ODBC Connection

The MySQL database was connected to external tools using an **ODBC connector**, allowing:

* Direct access to stored procedure results
* Reusable SQL logic
* Seamless integration with BI tools like Power BI or Excel

---

## 📊 Output

The procedure generates an **executive summary** showing:

* Total Revenue by Region
* Target Revenue by Region
* Delayed Projects
* Active Sales Pipeline

