# SQL

> The language for querying, manipulating, and defining data in relational databases.

> **Related:** [Python](python.md) | [Choosing a Language](choosing-a-language.md)

---

## What Is It?

SQL (Structured Query Language) is the standard language for working with relational databases. It's declarative — you describe *what* data you want, not *how* to retrieve it. Every major database (PostgreSQL, SQLite, MySQL, SQL Server) uses SQL with minor dialect differences.

## Core Operations

### Querying Data

```sql
SELECT name, email
FROM users
WHERE active = 1
ORDER BY created_at DESC
LIMIT 10;
```

### Inserting Data

```sql
INSERT INTO users (name, email, active)
VALUES ('Alice', 'alice@example.com', 1);
```

### Updating Data

```sql
UPDATE users
SET email = 'newemail@example.com'
WHERE id = 42;
```

### Deleting Data

```sql
DELETE FROM users
WHERE active = 0;
```

## Filtering & Conditions

| Clause | What It Does |
|--------|-------------|
| `WHERE` | Filter rows before grouping |
| `AND`/`OR` | Combine conditions |
| `IN` | Match any value in a list |
| `BETWEEN` | Range check (inclusive) |
| `LIKE` | Pattern matching (`%` wildcard, `_` single char) |
| `IS NULL` / `IS NOT NULL` | Null checks |
| `HAVING` | Filter groups after `GROUP BY` |

## Joins

Joins combine data from multiple tables:

```sql
SELECT orders.id, users.name, orders.total
FROM orders
JOIN users ON orders.user_id = users.id;
```

| Join Type | What It Returns |
|-----------|----------------|
| `INNER JOIN` | Only rows with matches in both tables |
| `LEFT JOIN` | All rows from left table, matched rows from right (nulls for no match) |
| `RIGHT JOIN` | All rows from right table, matched rows from left |
| `FULL OUTER JOIN` | All rows from both tables |
| `CROSS JOIN` | Cartesian product (every row × every row) |

## Aggregation

```sql
SELECT status, COUNT(*) as count, AVG(total) as avg_total
FROM orders
GROUP BY status
HAVING count > 10;
```

| Function | What It Returns |
|----------|----------------|
| `COUNT(*)` | Number of rows |
| `SUM(col)` | Sum of values |
| `AVG(col)` | Average of values |
| `MIN(col)` | Minimum value |
| `MAX(col)` | Maximum value |
| `DISTINCT col` | Unique values only |

## Indexes

Indexes speed up lookups at the cost of slower writes:

```sql
CREATE INDEX idx_users_email ON users (email);
CREATE INDEX idx_orders_user_id ON orders (user_id);
```

| Index Type | Use Case |
|-----------|----------|
| B-tree (default) | General purpose, equality + range queries |
| Hash | Equality lookups only |
| Partial | Index only a subset of rows |
| Composite | Multi-column queries |
| Full-text | Text search |

## Table Design

```sql
CREATE TABLE users (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    name TEXT NOT NULL,
    email TEXT UNIQUE NOT NULL,
    active INTEGER DEFAULT 1,
    created_at TEXT DEFAULT (datetime('now'))
);
```

### Constraints

| Constraint | What It Does |
|-----------|-------------|
| `PRIMARY KEY` | Unique identifier for each row |
| `FOREIGN KEY` | References a column in another table |
| `UNIQUE` | No duplicate values in this column |
| `NOT NULL` | Column must have a value |
| `CHECK` | Enforce a condition on values |
| `DEFAULT` | Default value if not provided |

## Normalization

Normalization reduces data redundancy:

| Normal Form | Rule |
|-------------|------|
| 1NF | Each column contains atomic values (one value per cell) |
| 2NF | 1NF + every non-key column depends on the whole primary key |
| 3NF | 2NF + every non-key column depends only on the primary key |

In practice, 3NF is usually sufficient. Denormalize (intentionally break normal forms) only for performance-critical reads.

## Common Pitfalls

| Pitfall | Why | Fix |
|---------|-----|-----|
| `SELECT *` in production | Returns unnecessary columns, breaks if schema changes | Name columns explicitly |
| Missing indexes | Full table scans on large tables | Add indexes on columns used in `WHERE`, `JOIN`, and `ORDER BY` |
| N+1 queries | Query inside a loop instead of a JOIN | Use `JOIN` or batched queries |
| No transactions | Partial updates leave data inconsistent | Wrap related operations in `BEGIN TRANSACTION` / `COMMIT` |
| SQL injection | User input concatenated into queries | Use parameterized queries (`?` placeholders) |

## Best Practices

- **Use parameterized queries** — never concatenate user input into SQL
- **Name columns explicitly** — `SELECT id, name` not `SELECT *`
- **Add indexes on foreign keys** — JOIN columns need indexes
- **Use transactions for related operations** — all-or-nothing consistency
- **Test queries with EXPLAIN** — `EXPLAIN QUERY PLAN SELECT ...` shows how the database executes the query
- **Back up before destructive operations** — `DELETE` and `UPDATE` without `WHERE` are irreversible
- **Use migrations** — version-controlled schema changes (Alembic for Python, EF Core for C#)
