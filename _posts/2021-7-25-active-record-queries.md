---
layout: post
title: Active Record Queries
tags: rails
---

There are two types of finder methods in Active Record; those that return a single instance of the model, e.g. `find` and  `first`, and those that return return an instance of `ActiveRecord::Relation` representing a collection of instances, e.g. `where` and `group`.  This post summarizes the query methods that return a single instance. 

- `find`

Retrieve the object with the given primary key. Raises `ActiveRecord::RecordNotFound` if no matching record is found. 

```ruby
irb(main):001:0> TimeReport.find(23)
   (1.5ms)  SELECT sqlite_version(*)
  TimeReport Load (0.3ms)  SELECT "time_reports".* FROM "time_reports" WHERE "time_reports"."id" = ? LIMIT ?  [["id", 23], ["LIMIT", 1]]
=> #<TimeReport id: 23, ...>

irb(main):002:0> TimeReport.find(230)
  TimeReport Load (0.3ms)  SELECT "time_reports".* FROM "time_reports" WHERE "time_reports"."id" = ? LIMIT ?  [["id", 230], ["LIMIT", 1]]
Traceback (most recent call last):
        1: from (irb):2:in `<main>'
ActiveRecord::RecordNotFound (Couldn't find TimeReport with 'id'=230)
```

You can also provide multiple primary keys (in an optional array) to fetch an array of results. 

```ruby
# SELECT * FROM customers WHERE (customers.id IN (1,10))
irb> customers = Customer.find([1, 10]) # OR Customer.find(1, 10)
```

- `take`

Retrieve a single record without any specific order. You can also pass the number of records you want. 

```ruby
irb(main):012:0> TimeReport.take
  TimeReport Load (0.3ms)  SELECT "time_reports".* FROM "time_reports" LIMIT ?  [["LIMIT", 1]]
=> #<TimeReport id: 1, date: "2023-11-14 00:00:00.000000000 +0000", hours_worked: 0.75e1, employee_id: 1, job_group: "A", report_id: 43>
```

- `first`

Fetch the first row, ordered by the primary key, by default. If you pass a number, Active Record will fetch that many number of rows. 

```ruby
irb(main):013:0> TimeReport.first
  TimeReport Load (0.4ms)  SELECT "time_reports".* FROM "time_reports" ORDER BY "time_reports"."id" ASC LIMIT ?  [["LIMIT", 1]]
=> #<TimeReport id: 1,...
```

If you don't want to order the results by primary key, first order them using the `order` method and then call `first(n)` to fetch the first `n` records. 

```ruby
# SELECT * FROM customers ORDER BY customers.first_name ASC LIMIT 1
Customer.order(:first_name).first
```

`last` acts in a similar way, except that it will fetch the last row in the result set. 

- `find_by`

Use this query method to find the first record that matches a condition. For example, to find the first customer with the name John, 

```ruby
# SELECT * FROM customers WHERE (customers.first_name = 'Lifo') LIMIT 1
Customer.find_by first_name: "John"
```

Alternatively, you can also write, 

```ruby
Customer.where(first_name: "John").take
```

