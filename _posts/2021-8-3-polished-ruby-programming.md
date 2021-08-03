---
layout: post
title: Polished Ruby Programming
tags: ruby
---

I started reading [Polished Ruby Programming](https://learning.oreilly.com/library/view/polished-ruby-programming/9781801072724/) by Jeremy Evans, author of the popular [sequel](https://github.com/jeremyevans/sequel) and [roda](https://github.com/jeremyevans/roda) libraries. This is an advanced Ruby book, diving into the design principles, best practices, and trade-offs while programming Ruby. So far, it hasn't disappointed. Here are my notes from the first chapter. 

**When to use core classes?**

Only create custom classes when the benefits outweigh the costs. 

With core classes, your code is more intuitive and in general, will perform better as it results in less indirection. 

Use custom classes when you have to encapsulate the logic to write maintainable code. However, the benefits of encapsulation are not greater than the loss of intuition and performance. 

> Start with the core classes, and only add a custom class when you see a clear advantage. 

**Strings or Symbols?**

Ruby is focused on programmer happiness and productivity, so it will often automatically convert a string to a symbol if it needs a symbol, or a symbol to a string if it needs a string.

A string in Ruby is a series of characters or bytes, useful for storing text or binary data. Unless the string is frozen, you can append to it, modify existing characters in it, or replace it with a different string.

A symbol in Ruby is a number with an attached identifier that is a series of characters or bytes.

> The general principle is to use symbols when you need an identifier in your code, and strings when you need text or data. 

**Arrays, Hashes, or Sets?**

Use an array if you need a simple list of values that you are iterating over or using the collection as a queue or a stack. 

If you need a mapping of one or more objects to one or more objects, use a hash. 

If you want a large list of unique objects and want to see whether a given object is contained in it, use a set.

**Use Structs**

It's one of the underappreciated core class in Ruby. `Struct` allows you to create classes with one or more fields and automatically creates accessors for each field. 

Using `Struct`, you can replace the following code:

```ruby
class Artist
  attr_accessor :name, :albums

  def initialize(name, albums)
    @name = name
    @albums = albums
  end
end
```

with 

```ruby
Artist = Struct.new(:name, :albums)
```

Though `Struct` is lighter on memory than a regular class, it has slower accessor methods. It used to be faster than accessor methods in older versions of Ruby, but regular classes and `attr_accessor` methods have gotten significantly faster. 

> For maximum performance, stick to regular classes. 