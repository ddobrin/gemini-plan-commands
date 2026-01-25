# Performance Analysis Checklist

Use this guide when analyzing migration scripts and database configurations for performance risks.

## 1. Migration Safety (Flyway / Alembic)

Analyze SQL or Python migration files for operations that lock tables for extended periods.

### Critical Locking Operations
- **Adding a column with a default value** (in older Postgres versions < 11): Causes a table rewrite.
  - *Fix:* Add column nullable, backfill data in batches, then set NOT NULL.
- **Creating an Index concurrently:**
  - Standard `CREATE INDEX` locks writes.
  - *Recommendation:* Use `CREATE INDEX CONCURRENTLY` (Postgres) to avoid locking writes.
  - *Note:* In Flyway, concurrent index creation cannot run inside a transaction. Ensure the migration is configured with `non-transactional` execution if supported.
- **Changing Column Type:** Often causes a table rewrite.
- **Renaming Tables/Columns:** Fast, but requires an exclusive lock that might block other queries if long-running transactions are active.

## 2. Index Strategy

Review schema definitions and queries to ensure efficient access paths.

- **Foreign Keys:** Ensure all FK columns are indexed. Deletes on parent tables can cause full table scans on child tables if FKs are unindexed.
- **Low Cardinality Columns:** Avoid indexing columns with very few unique values (e.g., `boolean`, `status` with 2-3 states) unless used in composite indexes.
- **Composite Indexes:**
  - Order matters: `(a, b)` supports queries on `a` and `a AND b`, but NOT just `b`.
  - Place high-cardinality columns first.

## 3. Sequence & Identity Tuning

- **Allocation Size:** Check `@SequenceGenerator` (Java) or sequence definitions.
  - Default `allocationSize=1` (or `increment by 1`) causes a DB roundtrip for *every* insert.
  - *Recommendation:* Increase allocation size (e.g., 50 or 100) for bulk insert performance (Pooled-Lo optimizer).

## 4. Connection Pool Settings (HikariCP)

Check `application.properties` or `application.yaml`:
- `maximum-pool-size`: Analyze if set appropriate for the workload (CPU cores * 2 + disk_spindle_count).
- `connection-timeout`: Ensure it's not too long (default 30s is often fine, but check for timeouts during load).
