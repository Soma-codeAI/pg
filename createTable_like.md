Postgres tip for copying schema: CREATE TABLE LIKE.

Postgres has a really handy tool that lets you create a table with the same schema of an existing table: CREATE TABLE new_table (LIKE existing_table INCLUDING ALL);

The `INCLUDING ALL` clause ensures that all attributes of the schema are copied:

- Column definitions
- Data types
- Constraints (including primary keys, unique keys, check constraints)
- Indexes
- Storage parameters

This basically copies everything EXCEPT the actual data. 

There’s lots of reasons you might want to create a new table just like an existing table:

- Creating a backup schema for testing changes on your production table
- To create a temporary table with the same schema as an existing one for staging or data transformation
- When archiving data, you may want the archive table to have the same schema as the original table to ensure consistency.
- Ensuring that tables with related data have consistent schemas.