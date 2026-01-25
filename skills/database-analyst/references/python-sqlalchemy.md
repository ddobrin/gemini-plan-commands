# Python / SQLAlchemy Analysis

## 1. N+1 Query Detection

### Detection
- Look for access to relationships (e.g., `user.addresses`) inside a loop over results.
- Default loading in SQLAlchemy is usually lazy.

### Solutions
- **Eager Loading:** Use `joinedload` or `subqueryload` options in the query.
  ```python
  stmt = select(User).options(joinedload(User.addresses))
  ```
- **AsyncIO:** For `asyncpg`, ensure relationships are loaded via options or explicit `await` calls to avoid "Greenlet error" or implicit I/O blocking.

## 2. Session Management

- **Scope:** Ensure `Session` is scoped to the request (e.g., using `dependency_injector` or FastAPI dependency).
- **Commit/Rollback:** Verify explicit commit or context manager usage.
  ```python
  with Session(engine) as session:
      # ... operations
      session.commit()
  ```

## 3. Alembic Migrations

- **Autogenerate Review:** Always inspect `alembic revision --autogenerate` output. It may miss:
  - Sequence creation/renaming.
  - Triggers.
  - Complex constraint changes.
