---
layout: post
title: "Ruby Standard Library: CSV"
tags: ruby
---

Here are my notes from the standard library [documentation](https://ruby-doc.org/stdlib-3.0.1/libdoc/csv/rdoc/CSV.html) for the CSV module. I took the notes as I was reading the docs and programming at the same time, so they aren't formatted very well, but they do capture the essence of working with CSV data in Ruby. 

CSV stands for comma-separated values.

A CSV file represents a table that contains text values separated by commas. In simple words, CSV data is a text representation of a table.

A row separator, typically a newline character `\n` separates the rows. A column separator, typically a comma `,`, separates the columns.

If a value needs a comma, enclose the comma in quotes.

**Examples**

CSV data with 4 rows and 3 columns (includes the header rows)

```
Company, Founder, CEO
Microsoft,Bill Gates,Satya Nadella
Google,"Larry Page, Sergey Brin",Sunder Pichai
Amazon,Jeff Bezos,Andy Jassy
```

CSV data with 3 rows and 2 columns.

 `foo,0\nbar,1\nbaz,2\n` 

**CSV in Ruby**

The `CSV` class in the Ruby standard library helps us parse:

1. a string representing CSV data
2. a file containing CSV data
3. an IO object providing CSV data

It can also generate CSV data as a String.

For most of the basic purposes the singleton (static) methods on the CSV class will do.

**Parsing CSV String**

1. `CSV.parse(csv_string)`

Returns an Array of Array of Strings. The first array represents the table and the inner arrays
represent the rows. Each String inside the Array represent a field value.

2. `CSV.parse_line(csv_string)`

Returns the first row, which is typically the header columns.

3. `String.parse_csv`

Ruby's monkey-patching also allows it to extend a String, to add the `parse_csv` method. This
method also returns the first row.

The following example illustrates the above methods.

```ruby
require "csv"

data = %(Company,Founder,CEO
Microsoft,Bill Gates,Satya Nadella
Google,"Larry Page and Sergey Brin",Sunder Pichai
Amazon,Jeff Bezos,Andy Jassy)

# [["Company", "Founder", "CEO"], ["Microsoft", "Bill Gates", "Satya Nadella"], ["Google", "Larry Page and Sergey Brin", "Sunder Pichai"], ["Amazon", "Jeff Bezos", "Andy Jassy"]]
p CSV.parse(data)

# ["Company", "Founder", "CEO"]
p CSV.parse_line(data)

# ["Company", "Founder", "CEO"]
p data.parse_csv
```

**Parsing CSV file**

The `read` method on the CSV class takes the file path and returns the CSV data.

```ruby
require "csv"

CSV.read("Data/companies.csv")
```

If you want to iterate over each row in a CSV file, use the `foreach` method.

```ruby
path = "Data/companies.csv"

CSV.foreach(path) do |row|
  p row
end
```

If you want a data structure instead of arrays, the `table` method returns the entire CSV data
as a `CSV::Table` object.

```ruby
path = "Data/companies.csv"

table = CSV.table(path)   # #<CSV::Table mode:col_or_row row_count:4>
p table.headers   # [:company, :founder, :ceo]
```

**Generate CSV Data**

The `generate` method on the CSV class generates the CSV data. You can use it as follows:

```ruby
output = CSV.generate do |csv|
  csv << %w{ Company Founder }
  csv << ["37Signals", "Jason Fried"]
  csv << ["Fog Creek Software", "Joel Spolsky"]
end

# Company,Founder
# 37Signals,Jason Fried
# Fog Creek Software,Joel Spolsky
puts output
```

You can also generate a single line from an array, using the `generate_line` method.

```ruby
values = %w{ hello world }
output = CSV.generate_line(values)

# hello,world
puts output
```

Finally, the CSV class also extends Array, so you can simply call `to_csv` to build a CSV string from an Array.

```ruby
values = %w{ hello world }
output = values.to_csv

# hello,world
puts output
```
