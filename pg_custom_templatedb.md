## Postgres productivity tip: template databases.

We’ve seen a lot of folks taking advantage of template databases for development environments. The basic idea here is that you have a single instance for development - and create and drop databases for dev as needed. The dev database has a template which is kept up to date with the production schema.

For remote teams using cloud hosted solutions, utilizing a template database can be a really cost effective and safe method. 

Using a template database for development can:

● streamline extension usage, Postgres configs, versioning, and other install issues that can take local development time
● ensure the schema is up to date with production, since templates can be easily created from a full copy of the database without data
● reduce time to provision and deprovision dev machines
● utilize anonymized seed data appropriate for development

More about template databases ⤵️ 

➡️ Create a template based on production, dump your production schema and extensions

```pg_dump -U my_user -h my_host -p 5432 -d my_database --exclude-table-data --no-owner --no-privileges > template.sql```

—exclude table data will remove the table data but include the full schema and all extensions. 

➡️ Create a restore database with your schema

```
-- create the database
CREATE DATABASE my_template_db OWNER postgres;

-- restore from the the dump file
psql -U my_user -h my_host -p 5432 -d my_template_db -f template.sql
```

Add seed data that you want to be used at this point. Adding seed data here makes things really fast when you do a template copy, as opposed to doing a restore function. 

➡️ To allow it to be used as a template, run:

ALTER DATABASE my_template_db is_template TRUE;

I should note here that this template database feature is only available from the Postgres superuser account. This is supported on Crunchy Bridge but not all managed Postgres services provide superuser. 

➡️ Now create a new database from the template

```CREATE DATABASE new_db WITH TEMPLATE my_template_db OWNER my_user;```

This will copy everything from my_template_db into new_db.

➡️ Update your connection string to connect to the new database for development and you’re off and ready to develop.
