# Intro to Migrations

As you build your FastAPI application, your database structure will evolve. You might add new tables or columns, change existing ones, or remove those that are no longer needed. Simply creating tables manually or using `Base.metadata.create_all()` is fine for a quick start, but it doesn’t scale well once your app grows. Without a systematic approach, keeping the database schema in sync with your models becomes error-prone.

This is where **migrations** come in to save the day. Migrations provide a reliable, structured way to update your database schema over time, just as version control (like Git) manages changes to your codebase.

# What are Migrations?

**Database migrations** (specifically, schema migrations) are controlled sets of changes to your database schema, applied in sequence to transition the database from one state to another.

In other words, a migration is like a “recipe” for a database change – it could add a new table or column, modify an existing column’s type, rename something, or delete an unneeded table. Each migration is typically represented by a script that knows how to apply the change (and usually how to undo it).

Think of it as keeping a history of all the tweaks you’ve made to the database structure. If your database schema is the design of a building, a migration is a renovation plan: it describes what needs to be altered from the current design to reach the new design.

# Why are Migrations Important?

Migrations bring **order and safety** to database changes. Instead of executing ad-hoc SQL commands and hoping everyone on the team does the same, migrations act as version control for your database.

### Benefits

- **Consistency**: Ensures every developer or server applies the same schema changes in the same way.
- **History & Versioning**: Keeps a permanent record of all schema changes.
- **Safe Upgrades (and Downgrades)**: Each migration includes steps to apply and undo changes.
- **Team Collaboration**: Makes it easy for teams to stay in sync.
- **Zero Guesswork**: Automatically tracks schema versions so you know what’s applied.

You can think of Alembic migrations as **“Git for your database schema”**.
