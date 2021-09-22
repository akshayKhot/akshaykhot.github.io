---
layout: post
title: Class Metaprogramming in Ruby
tags: ruby
---

A Ruby class definition is just regular code that runs. When you use the `class` keyword to create a class, you aren't just dictating how objects will behave in the future. You are actually running code. 

You can put any code in a class definition, and it returns the value of the last statement, just like methods and blocks do. 

```ruby
name = class Ruby
  puts "Hello world"
  creator = "Matz"
end

puts name

# Output
Hello world
Matz
```

Inside the class definition, the class itself takes the role of the `self`. 

```ruby
klass = class Ruby
  self
end

puts klass		# Ruby
puts klass.new		# <Ruby:0x00007fbd25854af0>
```

To access variables defined outside the class definition (i.e., flattening the scope), use `class_eval`. Inside, you can also define new methods dynamically on the class, using `define_method`.

```ruby
ror = "Ruby on Rails"

class Ruby; end

Ruby.class_eval do
  puts ror

  define_method(:run) do
    puts "Hello, from the new method"
  end
end

Ruby.new.run

# Output
# Ruby on Rails
# Hello, from the new method
```

Instance variables of a class (class instance variables) are different from the instance variables of that class's objects. If you come from Java or C#, it's tempting to think that the class instance variables are just the static fields of the class. Instead, they're just regular instance variables of an object of class `Class`. 

The following example illustrates this. The class `Ruby` is an object of the class `Class`, whereas `rb` is an object of the class `Ruby`. 

```ruby
class Ruby
  # ror is a instance variable of class 'Ruby'
  @ror = "Ruby on Rails" 

  def self.rails
    puts @ror
  end

  def initialize
    # language is an instance variable of 'a Ruby object'
    @language = "Ruby" 
  end

  def execute
    puts @language
  end
end

rb = Ruby.new

# valid code
Ruby.rails
rb.execute

# invalid code
Ruby.execute
rb.rails

# Output
#
# Ruby on Rails
# Ruby
# undefined method `execute' for Ruby:Class
# undefined method `rails' for #<Ruby:0x00007ff1...
```

**Singleton Methods**

When you define a method on a class, e.g. `Ruby.rails`, it's also known as a **singleton method of a class**. 

Here's the syntax to define singleton method on an object. Here, *object* can be an object reference, a class name, or self. 

```ruby
def object.method_name
  # method body
end
```

**Singleton Classes**

A singleton class is where an object's singleton methods live, whether that object is a class name or an object reference. You can access the singleton class by calling `singleton_class` method on the object. 

The superclass of the singleton class of an object is the object’s class.

The superclass of the singleton class of a class is the singleton class of the class’s superclass.

*from: [Metaprogramming Ruby 2](https://learning.oreilly.com/library/view/metaprogramming-ruby-2/9781941222751/)*