---
layout: post
title: Running Rails Migrations
tags: rails
---

In one of my [previous](/active-record-migrations) posts, we saw how to create migrations in Rails to update the database schema. However, creating a migration on its own doesn't update the database. You have to run the migration to make the changes. This post summarizes all the commands that modify the database.

`rails db:migrate`

This command runs the `change` method for all the migrations that have not run yet, in the order based on migration's date. It also updates the `db/schema.rb` file to match the database structure. 

`rails db:rollback`

Reverts the last migration. If you made a mistake and want to go back to the state before running the migration, use this command. Provide the `STEP=n` option if you want to revert last `n` migrations. You can run `db:migrate` after making corrections to the migration. 

However, the Rails guides recommend that it's not a good idea to edit an existing migration, especially if it has already been run on a production database. What you should do is create a new migration that performs the changes you need. 

`rails db:setup`

This command creates the database, loads the schema, and initializes it with the seed data. 

`rails db:reset`

Drop the database and set it up again. Equivalent to running `db:drop` and `db:setup` in sequence. 

`rails db:seed`

Migrations can also add, modify, or delete data in the database. However, to add seed data after a database is created, you can use the 'seeds' feature in the database. Simply add some sample data in `db/seeds.rb`, and run the `db:seed` command. 

**Schema Files**

Rails stores the current structure of the database schema in the `db/schema.rb` file. Schema files are also handy to check the attributes of a model. This information is not in the model's code and is frequently spread across several migrations, but it's outlined in the schema file.

Schema files are commonly used to create new databases, and it's recommended to check them into source control. 

By default, the schema file uses the `:ruby` format, but you can set it to `:sql`. This will save the schema in `db/structure.sql` file, using a database-specific tool, e.g. `pg_dump` for PostgreSQL and `SHOW CREATE TABLE` for MySQL.  

`rails db:schema:load`

To create a new instance of your database, you can simply run the `rails db:schema:load` command. It's better than running the entire migration history, as it may fail to apply correctly. 

The `:ruby` format cannot express everything in the database schema, such as triggers, stored procedures, etc. Setting the format to `:sql` will ensure that an accurate schema is generated and a perfect copy of the database schema is created upon running `db:schema:load`. 

The `db/schema.rb` or `db/structure.sql` is a snapshot of the current state of your database and is the authoritative source for rebuilding that database. This allows you to delete old migration files.