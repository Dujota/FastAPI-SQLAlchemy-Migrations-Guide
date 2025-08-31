# Handling Future Model Changes

Example: adding a `birthdate` column to the `User` model.

### 1. Update the Model

```python
birthdate = Column(Date, nullable=True)
```

### 2. Generate Migration

```bash
pipenv run alembic revision --autogenerate -m "Add birthdate to User"
```

Alembic creates a script that includes:

```python
def upgrade():
    op.add_column('users', sa.Column('birthdate', sa.Date(), nullable=True))

def downgrade():
    op.drop_column('users', 'birthdate')
```

### 3. Apply Migration

```bash
pipenv run alembic upgrade head
```

Your `users` table now has a `birthdate` column.

# Managing Migrations

Once Alembic is set up, here are common commands:

- **Apply migrations**:

```bash
pipenv run alembic upgrade head
```

- **Check current version**:

```bash
pipenv run alembic current
```

- **List migration history**:

```bash
pipenv run alembic history
```

These commands ensure your database is always in sync with your models.

# Undoing a Migration

Sometimes you need to roll back a migration.

### Downgrade one step

```bash
pipenv run alembic downgrade -1
```

This runs the `downgrade()` function in the most recent migration.

### Downgrade all the way

```bash
pipenv run alembic downgrade base
```

⚠️ Warning: This removes all tables and data. Use with caution!
