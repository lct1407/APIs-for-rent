---
description: Run database migrations with Alembic
---

Manage database migrations using Alembic.

Check the current migration status and run pending migrations:

1. Show current database version: `cd backend && alembic current`
2. Show pending migrations: `alembic history`
3. Run migrations: `alembic upgrade head`
4. Verify success

If there are issues:
- Check database connection
- Review migration files for errors
- Suggest rollback if needed: `alembic downgrade -1`

Provide:
- Current database version
- Migrations applied
- Any errors encountered
- Next steps if issues arise
