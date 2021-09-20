---
layout: post
title: Callable Objects
tags: ruby
---

There are at least three places in Ruby where you can package code to be executed later. In a **block**, a **proc/lambda**, and a **method**. 

**Block**

A block is a chunk of code you can associate with method invocations, almost as if they were parameters. You can use code blocks to implement callbacks, pass around chunks of code, and implement iterators. 

Here are two different ways to define blocks. We use the first version with braces for single-line blocks and `do/end` for multi-line blocks. 

```ruby
# this is a code block
{ puts "hello" } 

# this is also a code block
do
  puts "hello"
  puts "hello world"
end
```

A block is typically associated with a call to a method, by putting the block at the end of the source line containing the method call. The method can then invoke the block using the `yield` keyword in Ruby. 

```ruby
def greet(name)
  puts "hey, #{name}"
  yield
end

greet("Matz") { puts "Thanks for creating Ruby" }

greet("David") do 
  puts "Thanks for creating Rails"
end
```

You can also pass arguments to the call to `yield`, and Ruby will pass them to the block. 

```ruby
def add(a, b)
  sum = a + b
  yield sum
end

add(3, 4) { |sum| puts "result: #{sum}" }

add(3, 4) do |sum|
  puts "result: #{sum}"
end
```

**Proc**

A Proc object encapsulates a block, allowing us to store the block in a local variable, pass it around, and execute it later. 

There are four ways to convert a block into a Proc object. 

- Pass a block to a method whose last parameter starts with `&`. 

```ruby
def foo(p1, p2, &block)
  puts block.inspect
end

# #<Proc:0x00007fd9ff119848 main.rb:5>
foo(1, 3) { "a block" }

# nil
foo(3, 4)
```

- Call `Proc.new` or `Kernel#proc`,  associating it with a block.

```ruby
block = Proc.new { |arg| puts "a block with argument: #{arg}" }
block_new = proc { |arg| puts "shorthand block with argument: #{arg}" }

#<Proc:0x00007fa532035ac8 main.rb:1>
puts block.inspect
```

- Call the method `Kernel#lambda` and associate a block with it. Notice the appended `(lambda)` when you inspect the object. 

```ruby
block = lambda { |arg| puts "a block with argument: #{arg}" }

#<Proc:0x00007fa77f04d8b8 main.rb:1 (lambda)>
puts block.inspect
```

- Using the `->` syntax. 

```ruby
block_arrow = -> (arg) { puts arg }

# #<Proc:0x00007fb388830fc0 main.rb:7 (lambda)>
puts block_arrow.inspect
```

Once you have a Proc object, you can execute its code by invoking its methods `call`,  `yield`, or `[]`. 

```ruby
block = proc { |arg| puts "a block with argument: #{arg}" }

# a block with argument: 10
block.call 10
```

**Lambda**

The `Proc` objects created with the lambda syntax (3rd and 4th option above) are called lambdas. To check if a `Proc` object is a lambda, call the `Proc#lambda?` method on it. 

```ruby
block = proc { |arg| puts "a block with argument: #{arg}" }
puts block.lambda?		# false

block_lamb = lambda { |arg| puts "a block with argument: #{arg}" }
puts block_lamb.lambda?		# true

block_arrow = -> (arg) { puts "a block with argument: #{arg}" }
puts block_arrow.lambda?		# true
```

The lambdas differ from the `Proc` objects created any other way. We will see the differences in a future post. 

**Method**

The `Kernel#method` returns a method itself as a `Method` object. You can later execute this method object by invoking the `call` method on it, similar to a `Proc`. 

```ruby
class Animal
  def greet
    puts "Hello World"
  end
end

bunny = Animal.new
greet_method = bunny.method(:greet)
greet_method.call   # Hello World
```

You can convert a `Method` to a `Proc` by calling `Method#to_proc`. You can also convert a block to a method by using  `define_method` and associating the block with it. 

An important difference between the lambdas and methods is that Ruby evaluates a lambda in the scope it's defined it. In contrast, a `Method` is evaluated in the scope of its object. 
