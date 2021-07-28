---
layout: post
title: Overriding Constructors in Ruby
tags: ruby
---

Everything in Ruby is an object, including the classes themselves. Classes are first-class objects. When you create a new class, you are basically creating an instance of class `Class`. Ruby even allows you to override the `new` method on a class, allowing you to customize the creation of all objects.

```ruby
class Person
  # person-specific code
end
```

When Ruby encounters the above code, it creates an instance of type `Class`. It then assigns this object to a global constant named `Person`. 

When you call `Person.new` to create a new person, the `#new` method on the `Class` is called, by default. However, like everything in Ruby, you can override it. 

```ruby
class Class
  alias create new

  def new(*args)
    puts "Creating a new #{self.name}"
    create(*args)
  end
end

class Person; end

ak = Person.new

# Creating a new Person
# #<Person:0x00007fde9e869280>
puts ak
```

Knowing that classes are instances of `Class` allows you to dynamically create classes on the fly.

```ruby
Person = Class.new do
  def greet
    "hello"
  end
end

ak = Person.new
puts ak.greet    # hello
```





















