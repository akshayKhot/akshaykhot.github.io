---
layout: post
title: Running Rails Migrations
tags: rails
---

In one of my [previous](/active-record-migrations) posts, we saw how to create migrations in Rails to update the database schema. However, creating a migration on its own doesn't update the database. You have to run the migration to make the changes. This post summarizes all the commands that modify the database.

`db:migrate`

This command runs the `change` method for all the migrations that have not run yet, in the order based on migration's date. It also updates the `db/schema.rb` file to match the structure of the database. 

`db:rollback`

Reverts the last migration. If you made a mistake and want to go back to the state before running the migration, use this command. Provide the `STEP=n` option if you want to revert last `n` migrations. 

`db:setup`

This command creates the database, loads the schema, and initializes it with the seed data. 

`db:reset`

Drop the database and set it up again. Equivalent to running `db:drop` and `db:setup` in sequence. 

