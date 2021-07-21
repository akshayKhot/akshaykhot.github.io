---
layout: post
title: "Active Record in Rails"
tags: rails
img: rails/active_record.png
---

Rails makes extensive use of the active record pattern, which was introduced by [Martin Fowler](https://www.martinfowler.com/eaaCatalog/activeRecord.html) in his book [Patterns of Enterprise Application Architecture](https://www.martinfowler.com/eaaCatalog/index.html). This post tries to summarize my understanding of the pattern in the context of a Rails application. 

> An active record represents an object that wraps a row in a database table, encapsulates the database access, and adds domain logic on the data.

Active Record is responsible for handling business-domain logic, validating the data, and managing persistent storage to a database. It allows you to easily create, read, update, and delete data from the database without writing SQL statements. 

To create an Active Record, create a Ruby class that extends `ApplicationRecord`, which itself extends from `ActiveRecord::Base` class. 

```ruby
class Post < ApplicationRecord
end
```

Rails uses [convention over configuration](https://rubyonrails.org/doctrine/#convention-over-configuration), and a class named `Post` will automatically map to a database table named `posts`. Each instance of `Post` will represent a row in the `posts` table, and the attributes on the `Post` class will map to columns in the `posts` table. By default, Active Record will use an integer column named `id` as the primary key for the table. 

<a target="_blank" href="{{ site.images }}/{{ page.img }}">
  <img src="{{ site.images }}/{{ page.img }}" alt="Class to Table Mapping">
</a>  

If you want to override the default Rails conventions to use different names, you can use the `table_name` and `primary_key` attributes. 

```ruby
class Post < ApplicationRecord
  self.table_name = "articles"
  self.primary_key = "p_id"
end
```

Query methods return  an `ActiveRecord::Relation`, a chainable object that is lazy evaluated against the database only when the actual records are needed. This is similar to Linq in C#. 	

Rails also inserts two columns named `created_at` and `updated_at` that automatically get set to the current date and time when the record is created and updated, respectively. 

Active Record automatically creates methods on your models, allowing you to read and manipulate the data stored in the database. 

**1. Create**

```ruby
post = Post.create(title: "first post", body: "hello world")
```

The `create` method creates and saves a new record in the database. You can also instantiate an object without saving it using the `new` method.

```ruby
post = Post.new
post.title = "second post"
post.body = "hello, again!"
```

 To save the record, call `post.save`.

Both `create` and `new` methods take a block that yields the newly created object. 

```ruby
post = Post.new do |p|
  p.name = "third post"
  p.body = "hello, hello!"
end
```

**2. Read**

You can access the data in the database using one of the many query methods provided by Active Record. 

```ruby
# Fetch all posts 
posts = Post.all

# Fetch the first post
post = Post.first

# Find the post with the given id
post = Post.find_by(id: 3)
```

**3. Update**

Once you fetch an Active Record object using a query, you can update it by modifying its attributes and calling `save` method to persist the changes in the database. 

```ruby
post = Post.first
post.title = "First Post"
post.save

# Shorthand using the update method
post.update(title: "First Post")
```

**4. Delete**

Similar to `update`, you can delete an Active Record instance from the database by calling the `destroy` method on it. It removes the record from the database.

```ruby
post = Post.first
post.destroy

# Delete all posts with the title "test"
Post.destroy_by(title: "test")

# Delete all posts
Post.destroy_all
```

**Macro Methods**

These are usually placed at the top of the class, adding run-time behavior to the class, in the form of instance variables and methods. These methods provide a readable DSL which makes it easy to understand how the class is configured. 

The `has_many` method adds new associations to the `Post` class. 

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

