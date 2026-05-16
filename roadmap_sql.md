# 🗄️ SQL Learning Roadmap: Beginner to Advanced
### Industry-Focused · Practical · Implementable

> **How to use this roadmap:** Follow phases sequentially. Complete all exercises and projects before advancing. SQL is learned by *doing* — every concept should be practiced immediately against a real database. Estimated durations assume 1–2 hours of focused study per day.

---

## 📍 Phase 0 — Environment Setup & Orientation
**Goal:** Have a working SQL environment and understand the landscape

### Choose Your Learning Database
Install at least one. SQLite for zero-friction start; PostgreSQL for industry depth.

| Database | Best For | Install |
|----------|----------|---------|
| **SQLite** | Zero-config local learning | Built into Python; DB Browser for SQLite (GUI) |
| **PostgreSQL** | Industry standard (web, data, analytics) | postgresql.org or via Docker |
| **MySQL / MariaDB** | Web backends, legacy systems | mysql.com or via Docker |
| **SQL Server (Express)** | Enterprise / Microsoft environments | microsoft.com/sql-server |

### Tools to Install
- **DBeaver** (free, universal) or **TablePlus** — GUI database clients
- **pgAdmin** — PostgreSQL-specific GUI
- A terminal / command-line client (`psql`, `sqlite3`, `mysql`)
- VS Code with the **SQLTools** extension for in-editor querying

### Core Orientation Concepts
- What is a relational database? What problem does it solve?
- Tables, rows, and columns — the fundamental model
- SQL dialects: standard SQL vs PostgreSQL vs MySQL vs SQLite differences
- ACID properties (Atomicity, Consistency, Isolation, Durability) — why they matter
- The role of SQL in modern tech stacks (backend APIs, analytics, ML pipelines, reporting)

---

## 🟢 Phase 1 — SQL Foundations
**Goal:** Query and manipulate data confidently in any database

### 1.1 Database & Table Basics
- Creating a database and connecting to it
- `CREATE TABLE` — columns, data types, constraints
- Core data types:

| Category | Types |
|----------|-------|
| Numeric | `INTEGER`, `BIGINT`, `DECIMAL(p,s)`, `FLOAT` |
| Text | `VARCHAR(n)`, `TEXT`, `CHAR(n)` |
| Date/Time | `DATE`, `TIME`, `TIMESTAMP`, `INTERVAL` |
| Boolean | `BOOLEAN` |
| Other | `UUID`, `JSON`, `BYTEA` (PostgreSQL) |

- `ALTER TABLE` — adding, dropping, renaming columns
- `DROP TABLE` and `TRUNCATE` — differences and dangers
- `NULL` — what it means, why it's special, and pitfalls

### 1.2 Inserting & Modifying Data (DML)
- `INSERT INTO` — single and multi-row inserts
- `UPDATE` with `WHERE` clauses (always use `WHERE`!)
- `DELETE FROM` with `WHERE`
- `UPSERT` — `INSERT ... ON CONFLICT DO UPDATE` (PostgreSQL) / `REPLACE INTO` (MySQL)

### 1.3 Querying Data — SELECT
- `SELECT` basics: columns, aliases (`AS`), expressions
- `WHERE` clause and filter conditions
- Comparison operators: `=`, `!=`, `<`, `>`, `<=`, `>=`
- Logical operators: `AND`, `OR`, `NOT`
- `BETWEEN`, `IN`, `NOT IN`
- `LIKE` and `ILIKE` — pattern matching with `%` and `_`
- `IS NULL` / `IS NOT NULL`
- `DISTINCT` — removing duplicate rows
- `ORDER BY` — ascending and descending, multi-column sorting
- `LIMIT` and `OFFSET` — pagination

### 1.4 Aggregate Functions
- `COUNT()`, `SUM()`, `AVG()`, `MIN()`, `MAX()`
- `GROUP BY` — grouping rows for aggregation
- `HAVING` — filtering groups (vs `WHERE` filtering rows)
- Combining `WHERE`, `GROUP BY`, `HAVING`, `ORDER BY`, `LIMIT` — the logical execution order

### 1.5 String, Math & Date Functions
- String: `UPPER()`, `LOWER()`, `LENGTH()`, `TRIM()`, `SUBSTRING()`, `REPLACE()`, `CONCAT()`, `||`
- Math: `ROUND()`, `CEIL()`, `FLOOR()`, `ABS()`, `MOD()`
- Date: `NOW()`, `CURRENT_DATE`, `DATE_TRUNC()`, `DATE_PART()`, `EXTRACT()`, `AGE()`, `date + INTERVAL`
- Conditional: `CASE WHEN ... THEN ... ELSE ... END`
- `COALESCE()` and `NULLIF()` — handling NULLs gracefully

### 📝 Exercises (Phase 1)
Use a sample dataset (e.g., the classic Northwind database or a movies/employees dataset).

1. **The Basics** — retrieve all customers from a specific country, sorted by company name
2. **Filtered Aggregates** — find the total revenue per product category, only including categories with revenue > $10,000
3. **Date Arithmetic** — list all orders placed in the last 90 days with days-since-order calculated
4. **NULL Handling** — find all records where a phone number is missing; fill with `'N/A'` using `COALESCE`
5. **CASE Classifier** — classify orders as 'Small', 'Medium', or 'Large' based on total value
6. **String Operations** — extract the domain from a column of email addresses using string functions
7. **Top N per Group** — find the top 3 best-selling products in each category

### 🔨 Mini-Project 1: Sales Dashboard Queries
Design a small `sales` database from scratch (products, customers, orders, order_items). Then write a suite of business queries:
- Monthly revenue trend for the past 12 months
- Top 10 customers by lifetime value
- Products with declining sales month-over-month
- Average order value by customer region
- Inventory alert: products with fewer than 20 units in stock

---

## 🟡 Phase 2 — Joins, Relationships & Schema Design
**Goal:** Work with multi-table databases and design schemas professionally

### 2.1 Relational Thinking & Keys
- Primary keys (`PRIMARY KEY`) — uniquely identifying rows
- Foreign keys (`FOREIGN KEY`, `REFERENCES`) — enforcing relationships
- Surrogate keys (auto-increment `SERIAL`, `BIGSERIAL`, `UUID`) vs natural keys
- Composite keys — when and why
- Referential integrity and `ON DELETE CASCADE / SET NULL / RESTRICT`

### 2.2 The JOIN Family
- **INNER JOIN** — only matching rows from both tables
- **LEFT JOIN** — all rows from left, matched rows from right (NULLs for no match)
- **RIGHT JOIN** — all rows from right (prefer LEFT JOIN for consistency)
- **FULL OUTER JOIN** — all rows from both tables
- **CROSS JOIN** — Cartesian product (rare but useful)
- **SELF JOIN** — joining a table to itself (e.g., employee → manager)
- Multi-table joins — joining 3, 4, or more tables
- Join conditions beyond equality: range joins, non-equi joins

### 2.3 Subqueries
- Scalar subqueries — returning a single value
- Row subqueries — returning a single row
- Table subqueries — returning a result set
- Correlated subqueries — referencing the outer query
- `EXISTS` and `NOT EXISTS`
- Subqueries in `WHERE`, `FROM`, `SELECT`, and `HAVING`
- When to use subqueries vs JOINs (performance and readability tradeoffs)

### 2.4 Set Operations
- `UNION` and `UNION ALL` — combining result sets
- `INTERSECT` — rows in both queries
- `EXCEPT` / `MINUS` — rows in first query not in second
- Practical use cases: deduplication, gap analysis, change detection

### 2.5 Database Normalization
- **1NF** — atomic values, no repeating groups
- **2NF** — no partial dependencies (relevant for composite keys)
- **3NF** — no transitive dependencies
- **BCNF** — Boyce-Codd Normal Form
- **Denormalization** — when and why to intentionally break the rules (analytics, performance)
- Entity-Relationship (ER) diagrams — reading and drawing them
- Naming conventions for tables and columns (industry standards)

### 2.6 Constraints & Data Integrity
- `NOT NULL` — prevent missing required values
- `UNIQUE` — enforce uniqueness outside of primary key
- `CHECK` — enforce business rules at the database level
- `DEFAULT` — automatic values on insert
- Deferrable constraints (PostgreSQL) — useful in transactions

### 📝 Exercises (Phase 2)
1. **JOIN Ladder** — write the same query using INNER JOIN, LEFT JOIN, and a subquery; compare results and explain the differences
2. **Org Chart Query** — using a self-join on an `employees` table, display each employee alongside their manager's name
3. **Missing Records** — find all products that have never been ordered using a LEFT JOIN and `IS NULL`
4. **Multi-table Report** — join 4+ tables to produce a formatted invoice-style output
5. **Schema Design** — design an ER diagram and `CREATE TABLE` statements for a library management system (books, authors, members, loans)
6. **Normalization Exercise** — take a given denormalized spreadsheet and normalize it to 3NF, writing all table definitions

### 🔨 Mini-Project 2: E-Commerce Schema & Query Suite
Design a complete e-commerce database (users, addresses, products, categories, orders, order_items, reviews, inventory). Then:
- Write all `CREATE TABLE` statements with proper constraints and foreign keys
- Populate with realistic sample data (50+ products, 200+ orders)
- Build a set of 10 analytical queries covering joins, aggregates, and subqueries
- Document the ER diagram in a schema diagram tool (dbdiagram.io or draw.io)

---

## 🟠 Phase 3 — Advanced Querying
**Goal:** Write expert-level queries using modern SQL features

### 3.1 Window Functions
Window functions are the single most impactful advanced SQL skill for analytics and reporting.

- `OVER()` clause — the foundation of window functions
- `PARTITION BY` — dividing results into groups
- `ORDER BY` within `OVER()` — ordering within partitions
- Frame specifications: `ROWS BETWEEN`, `RANGE BETWEEN`

**Ranking Functions:**
- `ROW_NUMBER()` — unique sequential number
- `RANK()` — rank with gaps on ties
- `DENSE_RANK()` — rank without gaps
- `NTILE(n)` — divide into n equal buckets (percentiles)

**Offset Functions:**
- `LAG(col, n)` — access previous row's value
- `LEAD(col, n)` — access next row's value
- `FIRST_VALUE()`, `LAST_VALUE()`, `NTH_VALUE()`

**Aggregate as Windows:**
- Running totals: `SUM() OVER (ORDER BY date)`
- Running averages, cumulative counts
- Moving averages: `AVG() OVER (ROWS BETWEEN 6 PRECEDING AND CURRENT ROW)`

### 3.2 Common Table Expressions (CTEs)
- Basic CTEs with `WITH`
- Multiple CTEs in one query — chaining and reuse
- **Recursive CTEs** — tree structures, hierarchies, sequences
  - Organizational charts
  - Category hierarchies
  - Generating date/number series
- CTEs vs subqueries: readability, performance, and when each wins
- Materialized CTEs (PostgreSQL `WITH ... AS MATERIALIZED`)

### 3.3 Advanced Aggregation
- `GROUPING SETS` — multiple GROUP BY combinations in one query
- `ROLLUP` — hierarchical subtotals
- `CUBE` — all possible grouping combinations
- `FILTER` clause on aggregates: `COUNT(*) FILTER (WHERE status = 'active')`
- Conditional aggregation with `CASE WHEN` inside aggregates
- `STRING_AGG()` / `GROUP_CONCAT()` — aggregating text

### 3.4 JSON & Semi-Structured Data
- `JSON` vs `JSONB` in PostgreSQL (and equivalents in other DBs)
- Querying JSON: `->`, `->>`, `#>` operators (PostgreSQL)
- `JSON_VALUE()`, `JSON_QUERY()` (standard SQL / SQL Server / MySQL 8)
- Indexing JSON fields
- When to store JSON in SQL vs normalize into relational tables
- Aggregating rows into JSON with `JSON_AGG()`, `JSON_BUILD_OBJECT()`

### 3.5 Full-Text Search
- `LIKE` vs full-text search — when each applies
- PostgreSQL: `tsvector`, `tsquery`, `@@` operator, `to_tsvector()`, `to_tsquery()`
- `GIN` indexes for full-text search
- Ranking results by relevance: `ts_rank()`
- MySQL `FULLTEXT` index and `MATCH ... AGAINST`
- Practical alternatives: Elasticsearch for heavy search workloads

### 3.6 Transactions & Concurrency
- `BEGIN`, `COMMIT`, `ROLLBACK`
- Savepoints: `SAVEPOINT`, `ROLLBACK TO SAVEPOINT`
- Isolation levels: Read Uncommitted, Read Committed, Repeatable Read, Serializable
- Concurrency problems: dirty reads, non-repeatable reads, phantom reads
- Locking: `SELECT FOR UPDATE`, `SELECT FOR SHARE`, advisory locks
- Deadlocks — what causes them and how to avoid them

### 📝 Exercises (Phase 3)
1. **Window Function Suite** — on an orders table, compute: running total revenue, rank of each customer by spend, month-over-month growth percentage using `LAG`
2. **Recursive Hierarchy** — write a recursive CTE that traverses an employee org chart from CEO down to all leaf nodes, showing depth level
3. **Top-N per Group** — using `ROW_NUMBER()` in a CTE, find the top 3 orders per customer without using `LIMIT`
4. **JSON Query** — given a `products` table with a JSONB `attributes` column, find all products where `attributes->>'color' = 'red'` and aggregate unique colors
5. **Rolling Average** — compute a 7-day rolling average of daily signups using a window function with a frame clause
6. **Pivot Table** — use conditional aggregation to pivot monthly sales data from rows into columns (Jan, Feb, Mar...)

### 🔨 Mini-Project 3: Business Intelligence Query Library
Using a real public dataset (e.g., NYC Taxi data, Stack Overflow data dump, or AdventureWorks), build a library of 15 analytical queries:
- Customer segmentation using `NTILE()` (RFM analysis: Recency, Frequency, Monetary)
- Cohort retention analysis using `DATE_TRUNC` and window functions
- Period-over-period comparisons (WoW, MoM, YoY) using `LAG`
- Running totals and cumulative percentage of total
- Hierarchical category rollup using `ROLLUP`
- Funnel analysis: conversion rates between steps
- Full-text search query with relevance ranking

---

## 🔴 Phase 4 — Performance, Indexing & Query Optimization
**Goal:** Write queries that perform at scale; understand and fix slow queries

### 4.1 How Databases Execute Queries
- The query planner / optimizer — what it does
- `EXPLAIN` — reading query execution plans
- `EXPLAIN ANALYZE` — actual vs estimated rows, real timing
- Key plan nodes: `Seq Scan`, `Index Scan`, `Index Only Scan`, `Bitmap Heap Scan`, `Hash Join`, `Nested Loop`, `Merge Join`
- Statistics: `pg_stats`, `ANALYZE`, `VACUUM ANALYZE`
- Why the optimizer sometimes makes wrong choices — and how to guide it

### 4.2 Indexes — The Core Tool
- How B-tree indexes work (the most common type)
- When indexes help and when they don't (low cardinality, small tables)
- **Index types:**
  - `B-tree` — default, equality and range queries
  - `Hash` — equality-only (rarely preferred)
  - `GIN` — arrays, JSONB, full-text search
  - `GiST` — geometric data, fuzzy search
  - `BRIN` — very large, naturally ordered tables (e.g., time-series)
  - Partial indexes — `CREATE INDEX ... WHERE condition`
  - Expression indexes — `CREATE INDEX ON t (LOWER(email))`
  - Composite indexes — column order matters
- Index bloat and `REINDEX`
- Covering indexes and index-only scans
- The cost of indexes on writes — not free!

### 4.3 Query Optimization Techniques
- Avoiding `SELECT *` — only fetch what you need
- Filter pushdown — applying `WHERE` conditions early
- Avoiding functions on indexed columns in `WHERE` clauses
- Rewriting correlated subqueries as JOINs
- Using `EXISTS` instead of `COUNT(*)` for existence checks
- `LIMIT` early — filter before joining where possible
- Pagination anti-patterns: deep `OFFSET` and keyset pagination
- N+1 query problem — recognizing and eliminating it
- `MATERIALIZED VIEW` — precomputing expensive queries

### 4.4 Table Design for Performance
- Choosing the right data types (smaller = faster)
- `SERIAL` vs `BIGSERIAL` vs `UUID` as primary keys — tradeoffs
- Table partitioning:
  - Range partitioning (e.g., by date)
  - List partitioning (e.g., by region)
  - Hash partitioning (e.g., for even distribution)
- `VACUUM` and `AUTOVACUUM` — preventing table bloat
- `TOAST` — how PostgreSQL handles large values
- Write-heavy vs read-heavy design tradeoffs

### 4.5 Monitoring & Diagnostics
- `pg_stat_statements` — finding your slowest queries
- `pg_stat_user_tables` — detecting sequential scans
- `pg_stat_user_indexes` — finding unused indexes
- Lock monitoring: `pg_locks`, `pg_stat_activity`
- Connection pooling with **PgBouncer** — why it matters at scale
- Query timeout settings and circuit breakers

### 📝 Exercises (Phase 4)
1. **EXPLAIN Workout** — take 5 slow queries, run `EXPLAIN ANALYZE`, identify the bottleneck, fix it, and document before/after performance
2. **Index Design Challenge** — given a table with 1M rows and a set of common query patterns, design the optimal index strategy and justify each index
3. **Rewrite the Subquery** — rewrite 5 correlated subqueries as JOINs or CTEs and compare execution plans
4. **Pagination Fix** — replace an `OFFSET`-based paginator with keyset pagination and benchmark both
5. **Partition a Table** — take a large `events` table, partition it by month using range partitioning, and verify query pruning with `EXPLAIN`

### 🔨 Mini-Project 4: Query Performance Audit
Take the e-commerce database from Phase 2 and scale it to 5M+ rows using a data generator script. Then:
- Identify the top 5 slowest queries using `pg_stat_statements`
- Run `EXPLAIN ANALYZE` on each and document findings
- Apply fixes: indexes, rewrites, materialized views
- Produce a before/after performance report with execution times
- Add a scheduled `REFRESH MATERIALIZED VIEW` for the most expensive dashboard query

---

## 🔵 Phase 5 — Database Administration Essentials for Developers
**Goal:** Operate, secure, and maintain a production database

### 5.1 Users, Roles & Security
- Creating users and roles: `CREATE USER`, `CREATE ROLE`
- `GRANT` and `REVOKE` — principle of least privilege
- Row-level security (RLS) — restrict data access at the row level
- Schema-level permissions — separating read/write access
- Auditing: who changed what and when
- Never store plaintext passwords — `pgcrypto` and application-level hashing
- SQL injection — how it works, how to prevent it (parameterized queries, always)

### 5.2 Migrations & Schema Changes
- What database migrations are and why they matter
- Migration tools: **Flyway**, **Liquibase**, **Alembic** (Python), **golang-migrate**
- Writing safe migrations for production:
  - Adding a column with a default (safe vs unsafe)
  - Renaming a column without downtime (expand/contract pattern)
  - Adding indexes `CONCURRENTLY` — non-blocking index builds
  - Dropping columns safely
- Rolling back migrations — when it's possible and when it isn't
- Zero-downtime migration strategies

### 5.3 Backup & Recovery
- Logical backups: `pg_dump`, `pg_dumpall`, `mysqldump`
- Physical backups: base backups and WAL archiving
- Point-in-time recovery (PITR)
- Backup testing — restoring and verifying regularly
- Recovery time objective (RTO) and recovery point objective (RPO) — business concepts
- Automated backup scheduling and retention policies

### 5.4 Replication & High Availability
- Replication concepts: primary / replica architecture
- Streaming replication in PostgreSQL
- Read replicas for scaling read-heavy workloads
- Connection routing: writes to primary, reads to replicas
- Failover and promoted replicas
- Managed databases (AWS RDS, Google Cloud SQL, Supabase, Neon) — tradeoffs vs self-hosting

### 5.5 Cloud & Managed Databases
- AWS RDS / Aurora — setup, parameter groups, multi-AZ
- Google Cloud SQL / AlloyDB
- Supabase / Neon — developer-focused PostgreSQL platforms
- PlanetScale — MySQL-compatible with branching
- Connection string management and secrets in production
- Cost management: right-sizing instances, reserved capacity

---

## 🟣 Phase 6 — Specialized Tracks
**Choose based on your target role**

---

### 📊 Track A: Analytics & Data Engineering

#### Topics
- **Data Warehousing** concepts: OLTP vs OLAP, star schema, snowflake schema, fact tables, dimension tables
- **dbt (data build tool)** — the industry standard for transforming data in the warehouse
  - Models, sources, seeds, snapshots
  - Testing with `dbt test`
  - Documentation with `dbt docs`
  - Incremental models for large tables
- **Analytical databases:** BigQuery, Snowflake, Redshift, DuckDB
  - Columnar storage — why it's faster for analytics
  - Clustering and partitioning in BigQuery/Snowflake
  - Cost optimization strategies
- **Window functions at scale** — advanced analytical patterns
- **SCD (Slowly Changing Dimensions)** — Types 1, 2, 3
- **ELT vs ETL** — modern data stack patterns
- **Data quality** — `dbt test`, Great Expectations, schema contracts

#### 🔨 Capstone A: dbt Analytics Project — "RetailMetrics"
Build an end-to-end analytics project on a retail dataset:
- Raw data → staging models → mart models using dbt
- Star schema with `dim_customer`, `dim_product`, `dim_date`, `fact_orders`
- Implement SCD Type 2 for customer records using dbt snapshots
- Write dbt tests for every model (not null, unique, referential integrity)
- Build dashboard-ready mart models: revenue by channel, customer cohort retention, product affinity
- Generate full dbt documentation site
- Schedule with Airflow or dbt Cloud

---

### 🌐 Track B: Backend & Application Development

#### Topics
- **ORM integration:** SQLAlchemy (Python), Prisma (Node.js), ActiveRecord (Rails), GORM (Go)
  - Model definitions and migrations from ORM
  - Eager vs lazy loading — avoiding the N+1 problem
  - Raw SQL when ORM falls short
- **Connection pooling** in applications: PgBouncer, pgpool, built-in pool settings
- **Database transactions in application code** — managing commit/rollback in your ORM
- **Optimistic vs pessimistic locking** at the application level
- **Read replica routing** in application code
- **Soft deletes** — `deleted_at` pattern vs hard deletes
- **Audit logging** — tracking changes in application tables
- **Multi-tenancy patterns:** row-level (tenant_id column), schema-level, database-level
- **Database-driven features:** queues with `SKIP LOCKED`, caching with `MATERIALIZED VIEW`, scheduled jobs

#### 🔨 Capstone B: Production-Ready Application Database — "SaaSBase"
Design and implement the complete database layer for a multi-tenant SaaS application:
- Multi-tenancy via `tenant_id` with row-level security
- Users, teams, subscriptions, billing events, audit log, feature flags
- Full migration history (10+ migrations using Alembic or Flyway)
- Soft delete pattern on all user-facing entities
- Read replica routing for reporting queries
- `SKIP LOCKED` job queue table for background tasks
- Comprehensive indexes with justification for each
- Load test with 100K tenants and verify query performance

---

## 📚 Curated Resources

### Reference Datasets (use throughout the roadmap)
| Dataset | Source | Best For |
|---------|--------|----------|
| Northwind | GitHub (many ports) | Classic OLTP practice |
| AdventureWorks | Microsoft | Enterprise schema complexity |
| NYC Taxi Trips | NYC Open Data | Large-scale analytics |
| Stack Overflow Data Dump | archive.org | Real-world complex data |
| Pagila (DVD Rental) | PostgreSQL wiki | PostgreSQL-specific features |
| DuckDB Sample Data | duckdb.org | Analytical SQL practice |

### Books
| Title | Level | Focus |
|-------|-------|-------|
| *Learning SQL* — Alan Beaulieu | Beginner | Comprehensive foundations |
| *SQL Antipatterns* — Bill Karwin | Intermediate | Avoiding common mistakes |
| *The Art of PostgreSQL* — Dimitri Fontaine | Intermediate–Advanced | Deep PostgreSQL mastery |
| *Designing Data-Intensive Applications* — Kleppmann | Advanced | Distributed systems & databases |
| *High Performance MySQL* — Schwartz et al. | Advanced | MySQL optimization |
| *The Data Warehouse Toolkit* — Kimball & Ross | Advanced | Dimensional modeling |

### Online Platforms
- **SQLZoo** — interactive browser-based exercises
- **Mode SQL Tutorial** — analytics-focused SQL learning
- **pgexercises.com** — PostgreSQL-specific practice problems
- **use-the-index-luke.com** — the definitive guide to SQL indexing
- **explain.dalibo.com** — visualize PostgreSQL `EXPLAIN` plans
- **dbfiddle.uk** — test SQL across multiple database engines

---

## 🗓️ Recommended Study Schedule

| Phase | Commitment | Timeline |
|-------|-----------|----------|
| Phase 0: Setup | 1–2 hrs/day | Week 1 |
| Phase 1: Foundations | 1–2 hrs/day | Weeks 2–5 |
| Phase 2: Joins & Schema Design | 1.5 hrs/day | Weeks 6–10 |
| Phase 3: Advanced Querying | 1.5–2 hrs/day | Weeks 11–16 |
| Phase 4: Performance & Indexing | 1.5–2 hrs/day | Weeks 17–21 |
| Phase 5: Administration Essentials | 1.5 hrs/day | Weeks 22–25 |
| Phase 6: Specialization Track | 2 hrs/day | Weeks 26–32 |

> 💡 **Tip:** Always practice on real data. Import a public dataset instead of hand-crafting toy data — it forces you to deal with messiness, scale, and unexpected edge cases that teach the most.

---

## ✅ Progress Tracker

- [ ] Phase 0 complete — database running, first `SELECT` executed
- [ ] Phase 1 complete — Sales Dashboard Queries project done
- [ ] Phase 2 complete — E-Commerce Schema & Query Suite done
- [ ] Phase 3 complete — BI Query Library done
- [ ] Phase 4 complete — Query Performance Audit done
- [ ] Phase 5 complete — administration essentials understood
- [ ] Phase 6 Track chosen: ___________
- [ ] Phase 6 Capstone complete — production-grade project shipped

---

## 🧠 SQL Golden Rules (Internalize These)

1. **Always use `WHERE` with `UPDATE` and `DELETE`** — test in a transaction first
2. **`NULL` is not a value** — use `IS NULL`, never `= NULL`
3. **`EXPLAIN ANALYZE` before assuming** — measure, don't guess performance
4. **Indexes are not free** — they slow writes; add them deliberately
5. **Normalize first, denormalize with reason** — understand the rules before breaking them
6. **Use parameterized queries, always** — SQL injection is never acceptable
7. **Transactions wrap related changes** — partial updates are worse than no updates
8. **`SELECT *` is a code smell in production** — always specify columns
9. **Read the execution plan** — the optimizer tells you exactly what it's doing
10. **Test migrations on a copy of production** — never run untested schema changes live

---

*Roadmap version 1.0 · PostgreSQL-primary · Updated May 2026*