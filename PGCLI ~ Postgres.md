---
Title: PGCLI Postgres
Date: 12.02.2024
Time: 18:50
tags:
  - cheatsheet
  - dev
  - pgcli
  - postgres
---

## Manage DB

#### DB size

> [!example]- retrieve db size
> ```sql
> SELECT pg_size_pretty(pg_database_size('db')) AS database_size;
>```

> [!example]- retrieve tables sizes in db
> ```sql
> SELECT
>    table_name,
>    pg_size_pretty(pg_total_relation_size('"' || table_name || '"')) AS total_size
> FROM
>    information_schema.tables
> WHERE
>    table_schema = 'public'
> ORDER BY
>    pg_total_relation_size('"' || table_name || '"') DESC;
> ```

#### Close idle connections

> [!example]- Show `PID` and all IDLE connections
> ```sql
> SELECT * FROM pg_stat_activity WHERE datname = 'project_db';
> ```

> [!example]- Close IDLE connections to DB
> ```sql
> SELECT pg_terminate_backend(pid) FROM pg_stat_activity WHERE datname = 'project_db';
> ```

#### Roles & Users

> [!example]- Create `ROLE` & Set privileges
> ### Create Role
> ```sql
> CREATE ROLE analytics WITH LOGIN PASSWORD 'your_password' NOINHERIT;
> ```
> ### grant only `SELECT` privileges
> ```sql
> GRANT SELECT ON ALL TABLES IN SCHEMA public TO analytics;
> ```
> ### check privileges for analytics role
> ```sql
> select relname as table_name, CASE WHEN has_table_privilege('analytics', relname, 'SELECT') THEN 'SELECT' ELSE '-' END as select_privilege FROM pg_class WHERE relkind = 'r' AND relnamespace = 'public'::regnamespace;
> ```

> [!example]- Create `User`
> ```sql
> create USER some_user WITH PASSWORD 'somepassword'
> ```
> ### Make member of role analytics
> ```sql
> GRANT analytics TO some_user
> ```

> [!example]- list users
> ```bash
> pgcli list users: \du
> ```

----------------------

