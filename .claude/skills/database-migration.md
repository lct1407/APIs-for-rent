# Database Migration Skill

**Description**: Manage Alembic database migrations for PostgreSQL schema changes

**When to use**: When you need to create migrations, modify database schema, or manage database versions

## Instructions

When invoked, you should:

1. **Understand the change needed**:
   - Review the SQLAlchemy models in `backend/app/models/`
   - Identify what needs to change (new table, new column, index, constraint, etc.)
   - Check for data migration needs

2. **Create a new migration**:
   ```bash
   cd backend

   # Auto-generate migration from model changes
   alembic revision --autogenerate -m "descriptive_message"

   # Create empty migration for manual changes
   alembic revision -m "descriptive_message"
   ```

3. **Review the generated migration**:
   - Check `backend/migrations/versions/<timestamp>_<message>.py`
   - Verify `upgrade()` function has correct changes
   - Verify `downgrade()` function properly reverts changes
   - Add data migrations if needed

4. **Common migration patterns**:

```python
def upgrade() -> None:
    # Add a new column
    op.add_column('users', sa.Column('phone', sa.String(20), nullable=True))

    # Add an index
    op.create_index('idx_users_email', 'users', ['email'])

    # Add a foreign key
    op.create_foreign_key(
        'fk_orders_user_id',
        'orders', 'users',
        ['user_id'], ['id'],
        ondelete='CASCADE'
    )

    # Create a new table
    op.create_table(
        'new_table',
        sa.Column('id', sa.BigInteger(), nullable=False),
        sa.Column('name', sa.String(255), nullable=False),
        sa.Column('created_at', sa.DateTime(), server_default=sa.text('now()'), nullable=False),
        sa.PrimaryKeyConstraint('id')
    )

    # Data migration
    connection = op.get_bind()
    connection.execute(
        sa.text("UPDATE users SET status = 'active' WHERE status IS NULL")
    )

def downgrade() -> None:
    # Reverse all operations in reverse order
    op.drop_table('new_table')
    op.drop_constraint('fk_orders_user_id', 'orders', type_='foreignkey')
    op.drop_index('idx_users_email', 'users')
    op.drop_column('users', 'phone')
```

5. **Test the migration**:
   ```bash
   # Check current version
   alembic current

   # Run migration
   alembic upgrade head

   # Test rollback
   alembic downgrade -1

   # Re-apply
   alembic upgrade head

   # Show migration history
   alembic history --verbose
   ```

6. **Verify database changes**:
   ```bash
   # Connect to database and verify
   psql $DATABASE_URL -c "\d+ table_name"  # Describe table
   psql $DATABASE_URL -c "\di"  # List indexes
   ```

7. **Common migration tasks**:

   **Add a new model**:
   - Create model in `backend/app/models/`
   - Run `alembic revision --autogenerate -m "add <model_name> table"`
   - Review and apply migration

   **Add a column**:
   - Add column to model
   - Run `alembic revision --autogenerate -m "add <column_name> to <table>"`
   - If column is NOT NULL, handle existing data

   **Add an index**:
   - Add `__table_args__` to model or use `Index()`
   - Run autogenerate or create manual migration

   **Data migration**:
   - Create manual migration with `alembic revision`
   - Use `op.get_bind()` to get connection
   - Execute SQL or use ORM-style queries

8. **Safety checks**:
   - ⚠️ Never run migrations directly on production without testing
   - ⚠️ Always have database backups before migrations
   - ⚠️ Test both upgrade AND downgrade paths
   - ⚠️ Be careful with data migrations on large tables
   - ⚠️ Consider adding indexes concurrently for large tables

## Migration Best Practices

1. **Descriptive names**: Use clear, descriptive migration messages
2. **Atomic changes**: Keep migrations focused on one logical change
3. **Data preservation**: Never lose data in migrations
4. **Rollback support**: Always implement downgrade()
5. **Test on copy**: Test on a copy of production data
6. **Index strategy**: Add indexes CONCURRENTLY on production

## Database Schema Info

This project uses:
- **PostgreSQL 15+**
- **Incremental bigint IDs** (NOT UUID)
- **SQLAlchemy 2.0** async models
- **Alembic** for migrations
- Tables: users, organizations, api_keys, webhooks, subscriptions, payments, etc.

## Troubleshooting

**Issue**: Migration conflicts
```bash
# Merge multiple heads
alembic merge -m "merge migrations" <rev1> <rev2>

# Stamp specific version
alembic stamp <revision>
```

**Issue**: Need to modify old migration
- Don't modify old migrations that are in production
- Create a new migration to make changes

**Issue**: Failed migration
```bash
# Check current version
alembic current

# Manual rollback to specific version
alembic downgrade <revision>

# Fix the migration and try again
alembic upgrade head
```

## Output

Provide:
1. Migration file created/modified
2. SQL statements that will be executed
3. Verification of changes
4. Any warnings or considerations
5. Instructions for applying in production
