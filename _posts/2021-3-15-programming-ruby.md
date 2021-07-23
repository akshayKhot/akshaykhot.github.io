---
layout: post
title: Programming Ruby
tags: ruby
---

I have started learning the Ruby programming language for one of my side-projects that uses Ruby on Rails. Now the project is simple enough so that I could get by without knowing Ruby. But I thought learning the language would be a worthwhile project in itself. 

So I started reading [Programming Ruby](https://pragprog.com/titles/ruby/programming-ruby-2nd-edition/) by Dave Thomas. The book is very readable and explains Ruby in conversational, simple language, which I always admire, especially in technical books. For example, here is a simple explanation of blocks, a pretty powerful concept in Ruby. 

**Blocks in Ruby**

You can use code blocks to implement callbacks, pass around chunks of code, and implement iterators. 

Code blocks are just chunks of code between braces. 

```ruby
{ puts "This is a block" }  # Use for single-line blocks
```

or between do...end

```ruby
# Use for multi-line blocks
do
  puts "This is also a block" 
end
```

You can pass a block to a method by providing it at the end.

```ruby
use_block { puts "Block is passed to the use_block method" }
```

If there are parameters, they appear before the block.

```ruby
with_params ("param1", "param2") { puts "With parameters" }
```

Once a method receives a block, it can invoke that block using Ruby's `yield` statement. Think of `yield` as a method call that calls out to the block. 

If the block has parameters, you can pass them to yield, which will forward them to the block. Within the block, you list the arguments between vertical bars  `|`.

```ruby
def demo_block
  yield "Akshay", 30
end

demo_block do |name, age| 
  puts "Hello, there."
  puts "Name: #{name}, Age: #{age}"
end

# Output:
# Hello, there.
# Name: Akshay, Age: 30
```

Here is a complete example that illustrates all the above concepts. 

```ruby
def demo_block
  puts "In the method call"
  yield
  puts "In the method call"
  yield
end

demo_block { puts "This is a block." }

# Output:
# In the method call
# This is a block.
# In the method call
# This is a block.
```

**Iterators**

Ruby uses blocks to implement iterators, methods operating on successive elements of a collection, such as an array.

```ruby
numbers = [1, 2, 3, 4]
numbers.each do |num|
  square = num * num
  puts "Square of #{num} is #{square}"
end
```

After learning about them, I definitely like the blocks in Ruby more than the callbacks in JavaScript, or the closures in C-Sharp. 
