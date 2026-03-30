# TelcoX SQL Database: Telecom Analytics

Full SQL project for a fictional telecom company (TelcoX), covering database design, schema creation, data population, and 11 analytical queries. Developed as part of the Data Management course at Athens University of Economics and Business (AUEB).

## Project Overview

Built a relational database from scratch to analyze telecom customer behavior: call patterns, plan usage, city demographics, and year-over-year trends. The project demonstrates end-to-end database work — from ERD design to complex analytical SQL queries, plus a final Python integration using `pyodbc` and `pandas`.

## Database Schema

```
City (city_id PK, name, population, mean_income)
  └── Customer (customer_id PK, first_name, last_name, date_of_birth, gender, city_id FK)
        └── Contract (contract_id PK, phone_number, start_date, end_date, customer_id FK, plan_id FK)
              └── Calls (call_id PK, contract_id FK, call_datetime, called_number, duration_seconds)

Plan (plan_id PK, name, free_minutes, free_sms, free_mb)
  └── Contract (via plan_id FK)
```

**Sample data:** 20 cities, 20 customers, 10 plans, 20 contracts, 40 call records.

## Queries Implemented

| # | Query | Techniques |
|---|-------|-----------|
| a | Calls between 08:00–09:59 in June 2022 with duration < 30s | `DATEPART`, `WHERE` filtering |
| b | Customer names in cities with population > 200,000 | `JOIN`, subquery |
| c | Customers with contracts in "Freedom" plans | `LIKE`, `IN` subquery |
| d | Contracts ending within next 60 days | `GETDATE()`, `DATEADD`, multi-table `JOIN` |
| e | Average call duration per contract per month (2022) | `GROUP BY`, `DATEPART`, aggregate |
| f | Total call duration in 2022 by plan | `JOIN` chain, `SUM`, `GROUP BY` |
| g | Most frequently called number in 2022 | `COUNT`, `ORDER BY`, `TOP 1` |
| h | Months where usage exceeds plan's free minutes | `HAVING`, `SUM`, plan comparison |
| i | % change monthly duration: 2022 vs 2021 | `WITH` (CTEs), `FULL JOIN`, `CASE` |
| j | Avg call duration by city and gender (2022) | Conditional aggregation, `CASE WHEN` |
| k | City call ratio vs population ratio (2022) | Window functions (`SUM OVER`), `LEFT JOIN` chain |

## Final Section: Python Integration

The last query (k) is replicated in Python using `pyodbc` and `pandas`, demonstrating SQL-to-Python pipeline skills: connect to SQL Server, extract data via `pd.read_sql_query()`, and compute ratios using `groupby` and vectorized operations.

## File Structure

```
├── README.md
├── schema_and_data.sql          # CREATE TABLE + INSERT statements
├── queries.sql                  # All 11 analytical queries (a–k)
├── python_integration.py        # Python version of query (k)
└── report/
    └── SQL_Assignment.docx      # Full report with ERD diagram
```

## How to Run

```sql
-- 1. Open SQL Server Management Studio (or Azure Data Studio)
-- 2. Run schema_and_data.sql to create tables and insert data
-- 3. Run queries.sql to execute all analytical queries
```

```bash
# For the Python integration:
pip install pyodbc pandas
python python_integration.py
```

## Tools

SQL Server (T-SQL) · Python · pyodbc · pandas · ERD design

## Context

Developed for the Data Management course, MSc in Business Analytics, Athens University of Economics and Business (AUEB), November 2025.
