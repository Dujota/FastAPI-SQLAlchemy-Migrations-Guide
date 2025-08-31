# Migrations in FastAPI

FastAPI itself doesn’t have a built-in migration system. Instead, developers typically use **SQLAlchemy** for database models and **Alembic** for migrations.

Alembic is a database migration tool built specifically for SQLAlchemy. It can:

- Autogenerate migration scripts based on changes to your models.
- Apply those changes to the database safely.
- Roll back changes if needed.

In our project, we already have a `User` model defined with SQLAlchemy. Our goal is to use Alembic to track schema changes for this model (and any others we create later).

# Implementing Migrations in FastAPI

Here’s how to set up Alembic for your FastAPI project:

### 1. Install Alembic

```bash
pipenv install alembic
```

### 2. Initialize Alembic

```bash
pipenv run alembic init migrations
```

This creates a `migrations/` folder and `alembic.ini` config file.

### 3. Configure Alembic

#### Step 1: Set Database URL

- In `migrations/env.py`, set your database URL after the `config = context.config` line

```python
import os

database_url = os.environ.get("DB_URI")

if database_url:
        config.set_main_option("sqlalchemy.url", database_url)
else:
    # Fallback to a default or raise an error if the variable is not set
    # For example, you can get it from alembic.ini if not found in env
    raise ValueError("DB_URI environment variable is required")
```

#### Step 2: Link Models

- In `migrations/env.py`, import your models and set:

```python
from database import Base
from models import user

target_metadata = Base.metadata
```

### 4. Create First Migration

```bash
pipenv run alembic revision --autogenerate -m "Create users table"
```

Alembic generates a migration file under `migrations/versions/`.

### 5. Apply Migration

```bash
pipenv run alembic upgrade head
```

This applies the migration and creates the `users` table in your database.
