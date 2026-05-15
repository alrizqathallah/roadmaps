# 🗄️ SQL & Databases Learning Roadmap
### From Beginner to Advanced — Practical, Structured & Project-Driven

---

## 📌 How to Use This Roadmap

- Follow stages **in order** — concepts are deliberately cumulative
- **Type every query by hand** — never copy-paste; muscle memory matters
- Complete **every exercise and project** before advancing
- Use real datasets (links provided) — fake data teaches fake instincts
- Keep a **query journal**: a `.sql` file per topic where you save your work
- Revisit earlier stages when stuck — that's normal and productive

---

## 🛠️ Initial Setup (Before Stage 1)

### Choose Your Database System
> Start with **PostgreSQL** — it's the industry standard, open-source, and powers the concepts that transfer to all other systems.

| System | Best For | Install |
|---|---|---|
| **PostgreSQL** ✅ (recommended) | General purpose, industry standard | postgresql.org |
| **SQLite** | Lightweight, embedded, no server needed | Built into Python |
| **MySQL / MariaDB** | Web apps, legacy systems | mysql.com |
| **SQL Server (Express)** | Microsoft / enterprise environments | microsoft.com |

### Tools to Install
- [ ] **PostgreSQL** + **pgAdmin 4** (GUI client)
- [ ] **DBeaver** (universal DB GUI — works with all systems)
- [ ] **VS Code** with SQL extensions (SQLTools + driver)
- [ ] **DB Fiddle** or **SQLFiddle** (browser-based practice, no install needed)

### Practice Databases to Download
- **Northwind** — classic orders/products dataset (beginner–intermediate)
- **AdventureWorks** — Microsoft's rich sample DB (intermediate–advanced)
- **DVD Rental** — PostgreSQL official sample database
- **Chinook** — digital music store dataset (multi-table, cross-platform)
- **Stack Overflow Data Dump** — massive real-world dataset (advanced)

---

## 🟢 Stage 1 — SQL Foundations (Beginner)
**Estimated Time:** 3–4 weeks

---

### 1.1 What Is a Database?
- [ ] Difference between a database and a spreadsheet
- [ ] Relational vs. non-relational databases — when to use each
- [ ] What is a DBMS (Database Management System)?
- [ ] Tables, rows (records), and columns (fields)
- [ ] What is a schema?
- [ ] Introduction to data types: `INTEGER`, `VARCHAR`, `TEXT`, `BOOLEAN`, `DATE`, `NUMERIC`

### 1.2 Your First Queries — SELECT
- [ ] Basic `SELECT` statement
- [ ] Selecting specific columns vs. `SELECT *`
- [ ] `DISTINCT` — removing duplicates
- [ ] `WHERE` — filtering rows
- [ ] Comparison operators: `=`, `!=`, `<`, `>`, `<=`, `>=`
- [ ] Logical operators: `AND`, `OR`, `NOT`
- [ ] `BETWEEN`, `IN`, `LIKE`, `IS NULL`, `IS NOT NULL`
- [ ] `ORDER BY` — ascending and descending sorting
- [ ] `LIMIT` / `FETCH FIRST` — restricting result size

### 1.3 Working with Data — Basic Functions
- [ ] String functions: `UPPER()`, `LOWER()`, `LENGTH()`, `TRIM()`, `CONCAT()`, `SUBSTRING()`
- [ ] Numeric functions: `ROUND()`, `ABS()`, `CEIL()`, `FLOOR()`
- [ ] Date functions: `NOW()`, `CURRENT_DATE`, `EXTRACT()`, `DATE_PART()`, `AGE()`
- [ ] `COALESCE()` — handling NULLs gracefully
- [ ] `CAST()` and `::` type conversion

### 1.4 Aggregate Functions & Grouping
- [ ] `COUNT()`, `SUM()`, `AVG()`, `MIN()`, `MAX()`
- [ ] `GROUP BY` — grouping results
- [ ] `HAVING` — filtering groups (vs. `WHERE`)
- [ ] Combining aggregates with `GROUP BY`
- [ ] Counting NULLs vs. non-NULLs

### 1.5 Creating and Modifying Data (DML)
- [ ] `INSERT INTO` — adding rows (single and bulk)
- [ ] `UPDATE` — modifying existing rows
- [ ] `DELETE` — removing rows
- [ ] `TRUNCATE` — clearing a table
- [ ] The importance of `WHERE` with `UPDATE` and `DELETE`

### 1.6 Creating Tables (DDL)
- [ ] `CREATE TABLE` with appropriate data types
- [ ] `PRIMARY KEY` constraint
- [ ] `NOT NULL` constraint
- [ ] `DEFAULT` values
- [ ] `DROP TABLE`, `ALTER TABLE`
- [ ] `ADD COLUMN`, `DROP COLUMN`, `RENAME COLUMN`

---

### 🏋️ Stage 1 Exercises

**Exercise Set A — SELECT & Filtering**
```
Using the DVD Rental or Northwind database:
1. List all customers from Germany, sorted alphabetically by last name.
2. Find all products with a unit price between $10 and $50.
3. Show all orders placed in the year 1997.
4. Find all employees whose last name starts with 'S'.
5. List products where the quantity in stock is NULL or zero.
```

**Exercise Set B — Aggregates**
```
1. How many customers does each country have? Show top 10.
2. What is the average order value per customer?
3. Which product category has the highest total revenue?
4. Find the most recent and oldest order dates in the database.
5. How many orders were placed each month of 1997?
```

**Exercise Set C — DML & DDL**
```
1. Create a 'students' table with: id, name, email, enrollment_date, gpa.
2. Insert 5 rows of student data.
3. Update the GPA of one student.
4. Delete students with a GPA below 1.0.
5. Add a 'major' column to the students table.
```

### 🔨 Stage 1 Mini-Project: Personal Library Tracker
**Goal:** Design and build a database for tracking a personal book collection.

```
Requirements:
- Table: books (id, title, author, genre, pages, rating, date_read, status)
- Insert at least 15 books
- Queries to answer:
  · What genres have you read most?
  · What is your average rating per genre?
  · List all unread books sorted by page count
  · Which author do you have the most books by?
  · Books read per year
```

### 📚 Stage 1 Resources
- **Tutorial:** SQLZoo (sqlzoo.net) — interactive, free
- **Tutorial:** Mode SQL Tutorial (mode.com/sql-tutorial)
- **Book:** *Learning SQL* — Alan Beaulieu (O'Reilly)
- **Practice:** HackerRank SQL — Easy track

---

## 🔵 Stage 2 — Intermediate SQL
**Estimated Time:** 4–6 weeks

---

### 2.1 JOINs — Combining Tables
- [ ] Understanding relational data and foreign keys
- [ ] `INNER JOIN` — matching rows in both tables
- [ ] `LEFT JOIN` / `LEFT OUTER JOIN` — all rows from left, matching from right
- [ ] `RIGHT JOIN` — all rows from right
- [ ] `FULL OUTER JOIN` — all rows from both
- [ ] `CROSS JOIN` — cartesian product
- [ ] `SELF JOIN` — joining a table to itself
- [ ] Joining more than two tables
- [ ] Using table aliases to keep queries clean
- [ ] Understanding and avoiding duplicate rows from JOINs

### 2.2 Subqueries
- [ ] Scalar subqueries (return a single value)
- [ ] Row subqueries
- [ ] Table subqueries (in FROM clause — derived tables)
- [ ] Correlated subqueries
- [ ] `EXISTS` and `NOT EXISTS`
- [ ] `ANY`, `ALL` operators
- [ ] When to use a subquery vs. a JOIN

### 2.3 Common Table Expressions (CTEs)
- [ ] `WITH` clause — defining CTEs
- [ ] Benefits of CTEs over subqueries (readability, reusability)
- [ ] Multiple CTEs in one query
- [ ] Recursive CTEs — traversing hierarchical data
- [ ] CTE vs. temporary table vs. subquery — choosing the right tool

### 2.4 Window Functions
- [ ] What are window functions and why they matter
- [ ] `OVER()` clause — defining the window
- [ ] `PARTITION BY` — segmenting the window
- [ ] `ORDER BY` inside `OVER()`
- [ ] Ranking functions: `ROW_NUMBER()`, `RANK()`, `DENSE_RANK()`, `NTILE()`
- [ ] Offset functions: `LAG()`, `LEAD()`, `FIRST_VALUE()`, `LAST_VALUE()`
- [ ] Aggregate window functions: `SUM() OVER`, `AVG() OVER`, `COUNT() OVER`
- [ ] Running totals and moving averages
- [ ] Frame clauses: `ROWS BETWEEN`, `RANGE BETWEEN`

### 2.5 Advanced Filtering & Set Operations
- [ ] `UNION` and `UNION ALL`
- [ ] `INTERSECT`
- [ ] `EXCEPT` / `MINUS`
- [ ] `CASE WHEN` — conditional logic in queries
- [ ] `CASE WHEN` in aggregates (conditional counts/sums)
- [ ] `FILTER (WHERE ...)` aggregate modifier (PostgreSQL)
- [ ] `NULLIF()` — turning values into NULL
- [ ] `IIF()` / `IF()` — inline conditionals

### 2.6 String & Pattern Matching
- [ ] `LIKE` and `ILIKE` with wildcards (`%`, `_`)
- [ ] Regular expressions: `~`, `~*`, `REGEXP_MATCHES()` (PostgreSQL)
- [ ] `POSITION()`, `REPLACE()`, `SPLIT_PART()`
- [ ] `STRING_AGG()` — concatenating grouped strings
- [ ] `ARRAY_AGG()` — grouping into arrays

---

### 🏋️ Stage 2 Exercises

**Exercise Set D — JOINs**
```
Using Chinook or Northwind database:
1. List all orders with the customer name, not just customer_id.
2. Find all employees and their manager's name (self join).
3. List all products that have NEVER been ordered (hint: LEFT JOIN + NULL).
4. Show each order with product names, quantities, and line totals.
5. Find customers who have placed orders AND have a support rep assigned.
```

**Exercise Set E — Window Functions**
```
1. Rank customers by total spending within each country.
2. Calculate a running total of monthly sales for the year 1997.
3. For each product, show its price and the average price in its category side-by-side.
4. Find the month-over-month revenue change using LAG().
5. Identify the top 3 best-selling products per category using DENSE_RANK().
```

**Exercise Set F — CTEs & Subqueries**
```
1. Using a CTE, find customers whose total orders exceed the overall average.
2. Write a recursive CTE that generates numbers from 1 to 100.
3. Find the second highest salary in an employees table (no LIMIT).
4. Using EXISTS, find all categories that have at least one discontinued product.
5. Rewrite a complex subquery as a CTE and compare readability.
```

### 🔨 Stage 2 Mini-Project: Sales Analysis Dashboard Queries
**Goal:** Answer 10 business questions for a fictional e-commerce company using the Northwind database.

```
Business Questions to Answer:
1. Who are the top 5 customers by revenue in each country?
2. What is the month-over-month sales trend for the past 2 years?
3. Which products are frequently bought together?
4. Which employees have the highest order values on average?
5. What percentage of total revenue does each category contribute?
6. Find customers who haven't ordered in the last 6 months (churned).
7. What is the average time between a customer's first and second order?
8. Which shipping company has the most delayed orders?
9. Rank products by revenue within each category.
10. Build a customer segmentation (High/Mid/Low) based on spend using NTILE().

Deliverable: A well-commented .sql file with all queries + a short written
explanation of each finding.
```

### 📚 Stage 2 Resources
- **Book:** *SQL Cookbook* — Anthony Molinaro (O'Reilly)
- **Course:** Advanced SQL for Data Scientists — Mode Analytics
- **Practice:** LeetCode SQL — Medium problems
- **Practice:** DataLemur (datalemur.com) — real interview questions

---

## 🟡 Stage 3 — Database Design & Architecture
**Estimated Time:** 4–5 weeks

---

### 3.1 Relational Database Design
- [ ] Entity-Relationship (ER) diagrams — reading and drawing them
- [ ] Entities, attributes, and relationships
- [ ] Cardinality: one-to-one, one-to-many, many-to-many
- [ ] Identifying primary keys and surrogate keys
- [ ] Foreign keys and referential integrity
- [ ] Junction / bridge tables for many-to-many relationships
- [ ] Tools: dbdiagram.io, Lucidchart, draw.io

### 3.2 Normalization
- [ ] Why normalization matters (avoiding anomalies)
- [ ] **1NF** — First Normal Form: atomic values, no repeating groups
- [ ] **2NF** — Second Normal Form: no partial dependencies
- [ ] **3NF** — Third Normal Form: no transitive dependencies
- [ ] **BCNF** — Boyce-Codd Normal Form
- [ ] **4NF & 5NF** — conceptual understanding
- [ ] **Denormalization** — when and why to break the rules for performance

### 3.3 Constraints & Data Integrity
- [ ] `PRIMARY KEY` — uniqueness and non-null guarantee
- [ ] `FOREIGN KEY` — referential integrity, `ON DELETE CASCADE / SET NULL`
- [ ] `UNIQUE` constraint
- [ ] `CHECK` constraint — custom validation rules
- [ ] `NOT NULL` — mandatory fields
- [ ] Deferrable constraints (PostgreSQL)
- [ ] Triggers for enforcing complex business rules

### 3.4 Indexes
- [ ] What is an index and how does it work (B-tree structure)
- [ ] When to use an index and when NOT to
- [ ] `CREATE INDEX`, `DROP INDEX`
- [ ] Composite indexes — column order matters
- [ ] Partial indexes (PostgreSQL)
- [ ] Unique indexes
- [ ] Index types: B-tree, Hash, GIN, GiST, BRIN (PostgreSQL)
- [ ] Covering indexes
- [ ] Monitoring index usage

### 3.5 Transactions & ACID
- [ ] What is a transaction?
- [ ] **ACID** properties: Atomicity, Consistency, Isolation, Durability
- [ ] `BEGIN`, `COMMIT`, `ROLLBACK`
- [ ] `SAVEPOINT` — partial rollbacks
- [ ] Isolation levels: Read Uncommitted, Read Committed, Repeatable Read, Serializable
- [ ] Concurrency problems: dirty reads, phantom reads, non-repeatable reads
- [ ] Deadlocks — what they are and how to prevent them
- [ ] Optimistic vs. pessimistic locking

### 3.6 Views & Materialized Views
- [ ] Creating and using views (`CREATE VIEW`)
- [ ] Updatable views
- [ ] Using views for security (hiding sensitive columns)
- [ ] `MATERIALIZED VIEW` — cached query results
- [ ] `REFRESH MATERIALIZED VIEW`
- [ ] When to use views vs. CTEs vs. temp tables

### 3.7 Stored Procedures & Functions
- [ ] Creating functions with `CREATE FUNCTION`
- [ ] PL/pgSQL basics (PostgreSQL procedural language)
- [ ] Input/output parameters
- [ ] `CREATE PROCEDURE` vs. `CREATE FUNCTION`
- [ ] Using functions in queries
- [ ] Triggers: `BEFORE`, `AFTER`, `INSTEAD OF`
- [ ] When to use stored procedures (pros and cons)

---

### 🏋️ Stage 3 Exercises

**Exercise Set G — Database Design**
```
Design the ER diagram and SQL schema (CREATE TABLE statements) for:
1. A university system: students, courses, professors, enrollments, grades
2. A social media app: users, posts, comments, likes, follows
3. A hospital: patients, doctors, appointments, diagnoses, medications
4. An e-commerce site: users, products, orders, order_items, reviews, addresses

For each:
- Identify all entities and their attributes
- Define all relationships and cardinality
- Write complete CREATE TABLE statements with all constraints
- Draw the ER diagram using dbdiagram.io
```

**Exercise Set H — Normalization**
```
Given this denormalized table:
OrderID | CustomerName | CustomerCity | ProductName | Category | UnitPrice | Qty | Total

1. Identify all normalization violations
2. Normalize to 3NF step by step
3. Write all resulting CREATE TABLE statements
4. Write the original query to reconstruct the denormalized view
```

**Exercise Set I — Indexes & Performance**
```
1. On a 100k+ row table, run a query WITHOUT an index and record execution time.
2. Add the appropriate index, re-run, compare times.
3. Use EXPLAIN ANALYZE to read the query plan before and after.
4. Create a composite index and demonstrate when column order matters.
5. Create a partial index for an 'active = true' filter.
```

### 🔨 Stage 3 Mini-Project: Hospital Management Database
**Goal:** Design, build, and populate a complete relational database from scratch.

```
Entities to model:
- patients (demographics, contact info, insurance)
- doctors (specialization, department, contact)
- departments
- appointments (patient, doctor, date, status, notes)
- diagnoses (linked to appointments, ICD codes)
- medications (prescribed per diagnosis)
- billing (per appointment, line items, payment status)

Requirements:
- Full ER diagram using dbdiagram.io
- All tables in 3NF with proper constraints
- Populate with at least 50 patients, 20 doctors, 200 appointments
- Create views for: active appointments, unpaid bills, doctor schedules
- Write 10 analytical queries: busiest doctors, avg billing per department, etc.
- Add indexes on high-traffic columns and document your reasoning
```

### 📚 Stage 3 Resources
- **Book:** *Database Design for Mere Mortals* — Michael Hernandez
- **Book:** *SQL and Relational Theory* — C.J. Date
- **Tool:** dbdiagram.io — free ER diagram tool
- **Practice:** Design challenges on Reddit r/SQL

---

## 🟠 Stage 4 — Performance & Query Optimization
**Estimated Time:** 3–5 weeks

---

### 4.1 Understanding Query Execution
- [ ] How a SQL query is processed (parse → plan → execute)
- [ ] The Query Optimizer — what it does and its limitations
- [ ] `EXPLAIN` — reading a basic query plan
- [ ] `EXPLAIN ANALYZE` — actual vs. estimated rows
- [ ] Understanding nodes: Seq Scan, Index Scan, Hash Join, Nested Loop, Merge Join
- [ ] Reading costs: startup cost vs. total cost
- [ ] `EXPLAIN (ANALYZE, BUFFERS, FORMAT JSON)` — deep analysis

### 4.2 Writing Efficient Queries
- [ ] Avoid `SELECT *` in production queries
- [ ] Use `EXISTS` instead of `COUNT()` for existence checks
- [ ] Avoid functions on indexed columns in `WHERE` clause
- [ ] Use `LIMIT` early when possible
- [ ] Prefer JOINs over correlated subqueries for large datasets
- [ ] Use `UNION ALL` instead of `UNION` when duplicates are acceptable
- [ ] Avoid implicit type conversions
- [ ] Batch large `INSERT` / `UPDATE` / `DELETE` operations

### 4.3 Advanced Indexing Strategy
- [ ] Index selectivity — high vs. low cardinality columns
- [ ] When a query ignores your index (and how to fix it)
- [ ] Index-only scans and covering indexes
- [ ] Expression indexes: `CREATE INDEX ON orders (LOWER(email))`
- [ ] Full-text search indexes: `GIN` with `tsvector`
- [ ] Index bloat and `REINDEX`
- [ ] `pg_stat_user_indexes` — finding unused indexes

### 4.4 Table Partitioning
- [ ] Why partition large tables?
- [ ] Range partitioning (e.g., by date)
- [ ] List partitioning (e.g., by region)
- [ ] Hash partitioning
- [ ] Partition pruning — automatic query optimization
- [ ] Partition management: adding and dropping partitions

### 4.5 Statistics & the Planner
- [ ] `pg_stats` — how the planner sees your data
- [ ] `ANALYZE` — updating table statistics
- [ ] `VACUUM` and `AUTOVACUUM` — table bloat and dead tuples
- [ ] `VACUUM FULL` — reclaiming disk space
- [ ] Planner configuration: `work_mem`, `effective_cache_size`, `random_page_cost`

### 4.6 Identifying & Fixing Slow Queries
- [ ] `pg_stat_statements` — finding the slowest queries
- [ ] `auto_explain` — logging slow queries with their plans
- [ ] `pg_activity` — real-time query monitoring
- [ ] Identifying table bloat and lock contention
- [ ] Query rewriting strategies
- [ ] Caching hot queries with materialized views

---

### 🏋️ Stage 4 Exercises

**Exercise Set J — EXPLAIN Analysis**
```
For each query:
1. Run EXPLAIN ANALYZE
2. Identify the most expensive node
3. Propose and implement an optimization
4. Re-run and compare execution plans

Queries to analyze:
a) A multi-table JOIN with no indexes on join columns
b) A WHERE clause using a function on a column: WHERE LOWER(email) = 'x'
c) A correlated subquery that runs once per row
d) A large GROUP BY on a non-indexed column
e) A query returning 100k rows with ORDER BY on a non-indexed column
```

**Exercise Set K — Optimization Rewrites**
```
Rewrite each slow query into a faster equivalent:
1. Correlated subquery → JOIN
2. Multiple UNIONs → single query with CASE WHEN
3. Repeated CTE → materialized CTE or temp table
4. Row-by-row cursor logic → set-based operation
5. Expensive view → denormalized summary table with triggers
```

### 🔨 Stage 4 Mini-Project: Slow Query Audit
**Goal:** Take a poorly designed schema and optimize it systematically.

```
You are given:
- A 1 million row orders table with no indexes
- 5 slow queries (provided) that take 10+ seconds each
- A set of business requirements

Deliverables:
1. EXPLAIN ANALYZE output for all 5 queries (before)
2. Root cause analysis for each slow query (written)
3. Optimizations applied: indexes, query rewrites, partitioning
4. EXPLAIN ANALYZE output for all 5 queries (after)
5. Performance comparison table: before vs. after (time, rows, cost)
6. Written report: what you changed and why
```

### 📚 Stage 4 Resources
- **Book:** *PostgreSQL: Up and Running* — Regina O. Obe & Leo S. Hsu
- **Tool:** pgBadger — PostgreSQL log analyzer
- **Tool:** explain.depesz.com — visual query plan reader
- **Reading:** Use the Index, Luke (use-the-index-luke.com) — free, excellent

---

## 🔴 Stage 5 — Advanced Topics & Specialization
**Estimated Time:** 6–10 weeks (choose your path)

---

### 5.1 Advanced PostgreSQL Features
- [ ] **JSONB** — storing and querying JSON documents
- [ ] `jsonb_set()`, `->`, `->>`, `@>`, `?` operators
- [ ] **Arrays** — PostgreSQL array type and functions
- [ ] **Full-Text Search** — `tsvector`, `tsquery`, `to_tsvector()`, `GIN` index
- [ ] **Lateral Joins** — correlated subqueries in FROM
- [ ] **Row-Level Security (RLS)** — user-scoped data access
- [ ] **Table Inheritance** — parent-child table relationships
- [ ] **Foreign Data Wrappers (FDW)** — querying external data sources
- [ ] **Logical Replication** — streaming changes between databases

### 5.2 Data Warehousing & Analytics
- [ ] OLTP vs. OLAP — transactional vs. analytical systems
- [ ] Star schema design — fact tables and dimension tables
- [ ] Snowflake schema
- [ ] Slowly Changing Dimensions (SCD Types 1, 2, 3)
- [ ] ETL vs. ELT pipelines
- [ ] Introduction to **dbt** (data build tool)
- [ ] Columnar storage concepts (Parquet, Redshift, BigQuery)
- [ ] Introduction to **Apache Spark SQL**
- [ ] Window functions in analytics: percentiles, cohort analysis

### 5.3 NoSQL Databases — Conceptual Mastery
- [ ] When NOT to use a relational database
- [ ] **Document stores**: MongoDB — flexible schemas, embedded documents
- [ ] **Key-Value stores**: Redis — caching, sessions, leaderboards
- [ ] **Wide-column stores**: Cassandra — high-write, time-series
- [ ] **Graph databases**: Neo4j — relationships as first-class citizens
- [ ] **Time-series databases**: InfluxDB, TimescaleDB
- [ ] CAP theorem — Consistency, Availability, Partition Tolerance
- [ ] BASE vs. ACID — eventual consistency
- [ ] Polyglot persistence — using multiple DB types together

### 5.4 Database Administration Essentials
- [ ] User management: `CREATE ROLE`, `GRANT`, `REVOKE`
- [ ] Row-Level Security policies
- [ ] Backup strategies: `pg_dump`, `pg_basebackup`, WAL archiving
- [ ] Point-in-time recovery (PITR)
- [ ] Replication: streaming replication, logical replication
- [ ] Connection pooling: PgBouncer
- [ ] High availability: Patroni, read replicas
- [ ] Monitoring: `pg_stat_activity`, Prometheus + Grafana

### 5.5 SQL in Applications (Developer Track)
- [ ] ORM vs. raw SQL — tradeoffs
- [ ] Using **SQLAlchemy** (Python) — Core and ORM
- [ ] N+1 query problem — identifying and fixing
- [ ] Database migrations: **Alembic**, Flyway, Liquibase
- [ ] Connection pooling in application code
- [ ] SQL injection — what it is and how parameterized queries prevent it
- [ ] Optimistic locking in application code
- [ ] Database testing: seeding, fixtures, rollback per test

---

### 🏋️ Stage 5 Exercises

**Exercise Set L — JSONB & Advanced Types**
```
Using a 'products' table with a JSONB 'attributes' column:
1. Insert products with varying JSON structures (electronics, clothing, food)
2. Query all products where attributes->>'color' = 'red'
3. Find products where price in JSON exceeds a threshold
4. Add a GIN index and verify it speeds up containment queries (@>)
5. Use jsonb_set() to update a nested attribute value
```

**Exercise Set M — Data Warehouse Design**
```
Design a star schema for an e-commerce analytics system:
1. Identify the central fact table (orders_facts)
2. Design dimension tables: dim_customer, dim_product, dim_date, dim_location
3. Write SQL to populate dim_date for years 2020–2030
4. Write 5 analytics queries:
   · Revenue by quarter and region
   · Year-over-year product category growth
   · Customer cohort retention (30/60/90 day)
   · Average order value trend by customer segment
   · Product affinity matrix (what's bought together)
```

### 🔨 Stage 5 Capstone Project: End-to-End Database System

**Option A — Analytics Platform**
```
Build a complete analytics data warehouse:

1. Source Data: Use the Stack Overflow data dump (or Kaggle equivalent)
2. Staging Layer: Raw tables that mirror source data
3. Transformation Layer: Cleaned, normalized tables
4. Analytics Layer: Star schema with fact + dimension tables
5. Reports (SQL only):
   · User growth over time (monthly cohorts)
   · Question-to-answer conversion rate by tag
   · Top contributors per quarter
   · Tag popularity trends
6. Materialized views for each report with refresh strategy
7. Full documentation: ER diagram, data dictionary, query guide
```

**Option B — Multi-Tenant SaaS Database**
```
Design and implement the database backend for a project management SaaS:

Entities: organizations, users, projects, tasks, comments,
          attachments, labels, time_logs, notifications

Requirements:
- Multi-tenancy via organization_id on every table
- Row-Level Security policies per organization
- Full audit trail: created_at, updated_at, deleted_at, modified_by
- Soft deletes on all core entities
- Full-text search on tasks and comments
- Event log table for activity feeds
- Stored procedures for: assign task, close project, invite user
- Performance: all common queries under 50ms (EXPLAIN verified)
- Seed script: 10 orgs, 100 users, 1000 tasks, 5000 comments
- Complete API query library: 25 parameterized queries
- Written runbook: setup, migration, backup, monitoring
```

### 📚 Stage 5 Resources
- **Book:** *Designing Data-Intensive Applications* — Martin Kleppmann *(essential reading)*
- **Book:** *The Data Warehouse Toolkit* — Ralph Kimball
- **Course:** CMU Database Systems (15-445) — free on YouTube, world-class
- **Course:** Stanford DB Course — db.cs.stanford.edu
- **Practice:** LeetCode SQL — Hard problems

---

## 🏆 Summary: Skills Matrix

| Skill | Stage | Depth |
|---|---|---|
| SELECT, WHERE, ORDER BY | 1 | ████████░░ Foundation |
| Aggregates & GROUP BY | 1 | ████████░░ Foundation |
| JOINs (all types) | 2 | ██████████ Core |
| Window Functions | 2 | ██████████ Core |
| CTEs & Subqueries | 2 | ██████████ Core |
| ER Diagram & Normalization | 3 | ██████████ Core |
| Indexes & Constraints | 3 | ██████████ Core |
| Transactions & ACID | 3 | ████████░░ Core |
| Query Optimization | 4 | ██████████ Advanced |
| EXPLAIN ANALYZE | 4 | ██████████ Advanced |
| JSONB / Advanced Types | 5 | ████████░░ Specialist |
| Data Warehousing | 5 | ████████░░ Specialist |
| NoSQL Concepts | 5 | ██████░░░░ Awareness |
| DBA Essentials | 5 | ██████░░░░ Awareness |

---

## 📊 Summary Timeline

| Stage | Focus | Duration |
|---|---|---|
| ⚙️ Setup | Environment & tools | 1–2 days |
| 🟢 Stage 1 | SQL Foundations | 3–4 weeks |
| 🔵 Stage 2 | JOINs, CTEs, Window Functions | 4–6 weeks |
| 🟡 Stage 3 | Database Design & Architecture | 4–5 weeks |
| 🟠 Stage 4 | Performance & Optimization | 3–5 weeks |
| 🔴 Stage 5 | Advanced Specialization | 6–10 weeks |
| ♾️ Ongoing | Real projects, interviews, DBA topics | Continuous |

> **Total estimated time to job-ready proficiency:** ~6–8 months with consistent daily practice (1–2 hours/day).

---

## 💡 Real Datasets to Practice With

| Dataset | Rows | Topics Covered | Source |
|---|---|---|---|
| DVD Rental | ~16K | JOINs, aggregates | PostgreSQL Tutorial |
| Northwind | ~100K | Business analytics | GitHub |
| Chinook | ~400K | Music store analytics | GitHub |
| NYC Taxi Trips | 1B+ | Performance, partitioning | NYC OpenData |
| Stack Overflow Dump | Massive | Full-text, complex JOINs | archive.org |
| IMDb Datasets | ~10M | Complex queries, analytics | imdb.com/interfaces |
| Kaggle Datasets | Varies | Domain-specific practice | kaggle.com |

---

## 💡 Golden Rules for Learning SQL & Databases

1. **Every query has a cost** — always ask "could this be faster?"
2. **NULLs are not zero** — treat them deliberately, always
3. **Indexes are a trade-off** — they speed reads but slow writes; choose wisely
4. **Design first, code second** — a bad schema creates suffering forever
5. **Test with real data volumes** — a query fast on 100 rows may die on 10M
6. **Read query plans** — `EXPLAIN ANALYZE` is your most powerful diagnostic tool
7. **Transactions are not optional** — wrap multi-step operations, always
8. **Know your constraints** — the database enforcing rules beats application code
9. **Understand the data** — the best SQL comes from deeply knowing the domain
10. **Write readable queries** — format consistently; your future self will thank you

---

*Roadmap version: 2025 | PostgreSQL 16.x | ANSI SQL compatible*