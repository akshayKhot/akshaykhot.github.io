---
layout: post
title: Scope Flattening
tags: ruby
---

In C# and Java,  variables from the outer scope are visible to the inner scope. In Ruby, scopes are sharply separated, and nested visibility is not allowed. As soon as the control enters a new scope, i.e. a `class`, `module`, or a `method`, the previous bindings are replaced by a new set of bindings. 

The following example illustrates the above point. When the program control enters the class `Runner`, the variable `num` falls out of scope and is no longer visible inside the class or the method. 

```ruby
num = 1

class Runner
  puts "#{num} from class"

  def run
    puts "#{num} from method"
  end
end

Runner.new.run

# (NameError): undefined local variable or method `num' for Runner:Class
```

A workaround is to use Ruby's powerful meta-programming features. In Ruby, you can define new classes and methods on the fly, using `Class.new` and `define_method`, respectively, and passing a block. 

```ruby
num = 1

Runner = Class.new do
  puts "#{num} from class"

  define_method :run do
    puts "#{num} from method"
  end
end

Runner.new.run

# Output
# ==============
# 1 from class
# 1 from method
```

Replacing the scope gates (class, method, etc.) with a method call allows one scope to see variables from the outside scope. This is also known as **"flattening the scope"**.

*from: [Metaprogramming Ruby 2](https://learning.oreilly.com/library/view/metaprogramming-ruby-2/9781941222751/)*

