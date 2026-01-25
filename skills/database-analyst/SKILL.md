---
name: database-analyst
description: Analyzes database schemas, migrations, ORM entities, and repository pattern across Java, Kotlin, and Python codebases. Identifies performance issues, N+1 queries, locking risks, normalization violations, and generates ERD documentation
---

# Database Analyst

## Usage

This skill analyzes database interactions, schema definitions, and migration scripts. It supports:
- **Languages:** Java (Spring Data JPA, Hibernate), Kotlin (Exposed), Python (SQLAlchemy, Alembic)
- **Tasks:** Performance analysis, Schema design review, Application logic audit, ERD generation.

## Workflows

### 1. Identify Technology Stack

First, determine the database technology in use by checking configuration files:
- **Java/Spring:** Look for `pom.xml` (dependencies like `spring-boot-starter-data-jpa`, `flyway-core`), `application.properties`, and Entity classes (`@Entity`).
- **Python:** Look for `requirements.txt` (`sqlalchemy`, `alembic`), `alembic.ini`, and model definitions (`Base = declarative_base()`).

### 2. Select Analysis Mode

Based on the user's request, perform the following:

#### A. Performance & Migration Analysis
For requests about "slow queries", "locking", "migrations", or "tuning":
1.  Locate migration files (e.g., `src/main/resources/db/migration/*.sql` or `alembic/versions/*.py`).
2.  Review for locking risks and anti-patterns.
3.  **Read [references/performance.md](references/performance.md)** for specific checklists.

#### B. Schema Design & ERD
For requests about "normalization", "schema review", "database structure", or "diagrams":
1.  Locate Entity/Model classes.
2.  Analyze relationships, constraints, and keys.
3.  **Read [references/schema.md](references/schema.md)** for normalization rules and ERD formatting.

#### C. Application Logic & Query Analysis
For requests about "N+1 problems", "repository review", or "transaction issues":
1.  Locate Repository/DAO layers and Service layers.
2.  Trace method calls to identify implicit queries.
3.  **Read [references/java-jpa.md](references/java-jpa.md)** for Java/Spring specifics.
4.  **Read [references/python-sqlalchemy.md](references/python-sqlalchemy.md)** for Python specifics.

## Output Format

- **Analysis:** Group findings by "Critical", "Warning", and "Info".
- **ERD:** Use Mermaid diagram format unless requested otherwise.
- **Recommendations:** Provide concrete code snippets for fixes (e.g., adding an index, refactoring a query).