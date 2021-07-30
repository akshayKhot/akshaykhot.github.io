---
layout: post
title: Associations in Rails
tags: rails
---

An association is a connection between two Active Record models. 

```ruby
class Author < ApplicationRecord
  has_many :books
end

class Book < ApplicationRecord
  belongs_to :author
end
```

Six types of associations in Rails

1. `belongs_to`
2. `has_one`
3. `has_many`
4. `has_many :through`
5. `has_one :through`
6. `has_and_belongs_to_many`

**Polymorphic Associations**

A model dcan belong to more than one other model, on a single association. For example, a picture model that belongs to both an employee and a product can be expressed as:

```ruby
class Picture < ApplicationRecord
  belongs_to :imageable, polymorphic: true
end

class Employee < ApplicationRecord
  has_many :pictures, as: :imageable
end

class Product < ApplicationRecord
  has_many :pictures, as: :imageable
end
```

