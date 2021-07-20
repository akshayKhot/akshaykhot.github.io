---
layout: post
title: Active Record
tags: rails
img: rails/active_record.png
---

The active record pattern was introduced by [Martin Fowler](https://www.martinfowler.com/eaaCatalog/activeRecord.html) in his book [Patterns of Enterprise Application Architecture](https://www.martinfowler.com/eaaCatalog/index.html). Rails makes extensive use of it. This post tries to summarize my understanding of the pattern in the context of an Rails application. 

> An active record represents an object that wraps a row in a database table, encapsulates the database access, and adds domain logic on the data.

To create an active record, create a Ruby class that extends `ApplicationRecord`, which itself extends from `ActiveRecord::Base` class. 

```ruby
class Post < ApplicationRecord
end
```

Rails uses [convention over configuration](https://rubyonrails.org/doctrine/#convention-over-configuration), and a class named `Post` will automatically map to a database table named `posts`. Each instance of `Post` will represent a row in the `posts` table, and the attributes on the `Post` class will map to columns in the `posts` table. Rails assumes `id` as the primary key. 

<a target="_blank" href="{{ site.images }}/{{ page.img }}">
  <img src="{{ site.images }}/{{ page.img }}" alt="Class to Table Mapping">
</a>  

If you want to override the default Rails conventions to use different names, you can do so using the `table_name` and `primary_key` attributes. 

```ruby
class Post < ApplicationRecord
  self.table_name = "Article"
  self.primary_key = "p_id"
end
```

Query methods return  an `ActiveRecord::Relation`, which is a chainable object that is lazy evaluated against the database only when the actual records are needed. This is similar to Linq in C#. 	

**Macro Methods**

These are usually placed at the top of the class, adding run-time behavior to the class, in the form of instance variables and methods. These methods provide a readable DSL which make it easy to understand how the class is configured. 

The `has_many` method adds new associations on the `Post` class. 

```ruby
class Post < ApplicationRecord
  has_many :comments
end
```

The `attribute` method allows you to add a new attribute and specify its type and default value. 

```ruby
class Post < ApplicationRecord
	attribute :category, :string, default: 'note'
end
```

