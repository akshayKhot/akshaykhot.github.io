---
layout: post
title: "Generating Rails Migrations"
tags: rails
img: rails/migrations.jpeg
---

Like source code, database schema changes and evolves over time. Migrations are a feature of Active Record that allows you to manage the database schema changes gracefully, without writing any SQL. This post contains my notes on generating Active Record migrations from the official [Rails guides](https://guides.rubyonrails.org/active_record_migrations.html). 

**Key Points**

- Consider what Rails generates for you as a starting point. Update it as per your requirements. 
- Think of each migration as a new version of the database.
- Migrations allow you to modify schema in a database-independent way.
- `db/schema.rb` file contains the current structure of your database. 

Here's an example of a migration that adds a `time_logs` table with four explicit columns named `project`, `task`, `start_time`, and `end_time`. As you can see, it's a Ruby class with a `change` method. Along with the four columns, the migration will also add an `id` column as a primary key. The `timestamps` macro adds two columns `created_at` and `updated_at`. 

```ruby
class CreateTimeLogs < ActiveRecord::Migration[6.1]
  def change
    create_table :time_logs do |t|
      t.string :project
      t.string :task
      t.datetime :start_time
      t.datetime :end_time

      t.timestamps
    end
  end
end

```

To generate a migration, run the following command, which generates an empty migration. 

```shell
bin/rails generate migration AddPartNumberToProducts
```

It generates the following code:

```ruby
class AddPartNumberToProducts < ActiveRecord::Migration[6.0]
  def change
  end
end
```

If you want to add/remove columns or index to a table, use the `add_column`, `remove_column`, and `add_index` methods.

```ruby
class AddPartNumberToProducts < ActiveRecord::Migration[6.0]
  def change
    add_column :products, :part_number, :string
    add_index :products, :part_number
  end
end
```

Rails even allows you to mention the changes in the command. For example, 

```bash
bin/rails generate migration CreateProducts name:string part_number: string
# or
bin/rails generate migration AddDetailsToProducts part_number:string price:decimal
```

**Naming Conventions**

If the name of the migration starts with `Create__` followed by column names along with the types, then the resulting migration will create a table. 

```ruby
# bin/rails generate migration CreateProducts name:string part_number:string

class CreateProducts < ActiveRecord::Migration[6.0]
  def change
    create_table :products do |t|
      t.string :name
      t.string :part_number

      t.timestamps
    end
  end
end
```

If the name starts with `Add`, it will add columns to an existing table. 

```ruby
# bin/rails generate migration AddDetailsToProducts part_number:string price:decimal

class AddDetailsToProducts < ActiveRecord::Migration[6.0]
  def change
    add_column :products, :part_number, :string
    add_column :products, :price, :decimal
  end
end
```

If the name contains `JoinTable`, the generator will produce a join table. 

```ruby
# bin/rails generate migration CreateJoinTableCustomerProduct customer product

class CreateJoinTableCustomerProduct < ActiveRecord::Migration[6.0]
  def change
    create_join_table :customers, :products do |t|
      # t.index [:customer_id, :product_id]
      # t.index [:product_id, :customer_id]
    end
  end
end
```

