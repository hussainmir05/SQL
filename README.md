# SQL Lab Work

SQL exercises from the database lab in my bachelor's degree. Each script creates its own tables, fills them with sample rows, then answers that lab's tasks, which are marked with comments such as `---Task 3`.

The scripts are written for **Microsoft SQL Server** (T-SQL). Some parts, such as `LEN()`, `LIKE '[123]'` patterns and `ALTER COLUMN`, won't run unchanged in MySQL or PostgreSQL.

## Labs

| Lab | File | Topics |
|---|---|---|
| 2 | [lab02_insert_update_delete.sql](lab02_insert_update_delete.sql) | `CREATE TABLE`; `INSERT` into all columns or only some; `UPDATE`; `DELETE`; `SELECT DISTINCT`; `ORDER BY` |
| 3 | [lab03_aggregate_and_string_functions.sql](lab03_aggregate_and_string_functions.sql) | `COUNT`, `MAX`, `MIN`, `AVG`, `SUM`; `UPPER`, `LOWER`, `LEN`; `GROUP BY` and `HAVING` |
| 4 | [lab04_q1_like_and_in.sql](lab04_q1_like_and_in.sql) | Pattern matching with `LIKE` and `NOT LIKE`; `IN`, and the same filter written with `OR` |
| 4 | [lab04_q2_between.sql](lab04_q2_between.sql) | `BETWEEN` and `NOT BETWEEN` on numbers and text; `LIKE` with a character set |
| 5 | [lab05_constraints.sql](lab05_constraints.sql) | Adding `NOT NULL`, `UNIQUE`, `PRIMARY KEY`, `FOREIGN KEY`, `CHECK` and `DEFAULT` constraints with `ALTER TABLE` |

Lab 1 isn't included.

### Lab 5's test queries are meant to fail

After adding each constraint, Lab 5 runs a query that tries to break it. An error means the constraint works.

| Constraint | Test query | Expected result |
|---|---|---|
| `NOT NULL` on `P_Id` | adds a person with no `P_Id` | error |
| `UNIQUE` on `P_Id` | adds a second person with `P_Id` 1 | error |
| `PRIMARY KEY` on `P_Id` | adds a person with no `P_Id` | error |
| `CHECK (P_Id > 0)` | adds a person with `P_Id` 0 | error |
| `DEFAULT 'RAWALPINDI'` for `City` | adds a person with no city | the row is added, with RAWALPINDI as the city |

## Running the scripts

1. Install [SQL Server](https://www.microsoft.com/en-us/sql-server/sql-server-downloads) (the free Express or Developer edition) and [SQL Server Management Studio](https://learn.microsoft.com/en-us/ssms/install/install) (SSMS).
2. In SSMS, create a database for the labs and switch to it:

   ```sql
   CREATE DATABASE SqlLabs;
   GO
   USE SqlLabs;
   ```

3. Open a lab file and click **Execute** (F5). To run a single task, select its lines first.

Running a file a second time fails at `CREATE TABLE`, because its tables already exist. Drop them first (for example `DROP TABLE List1;`) or use a new database. No two labs use the same table name, so all five can share one database.
