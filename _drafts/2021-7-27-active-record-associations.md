---
layout: post
title: Associations in Active Record
tags: rails
---

After taking a brief hiatus, I resumed reading Obie Fernandez's excellent book The Rails 5 Way. I am still trying to wrap my head around associations and how they work, but here are my notes. 

Active Record associations let you declaratively express relationships between model classes. They are an important part of Rails and when people talk about 'Rails magic', they are usually talking about associations. 

**One-to-Many**

A typical example of the one-to-many mapping is that a blog post has many comments. On the other hand, a comment always belongs to one post. Rails provides `has_many` and `belongs_to` methods that let you specify these relationships in code and manages the foreign keys for you. 

```ruby
class Post < ActiveRecord::Base
  has_many :comments
end

class Comment < ActiveRecord::Base
  belongs_to :post
end
```

