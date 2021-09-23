---
layout: post
title: Bindings in Ruby
tags: ruby
---

A *Binding* is a whole scope packaged as an object. It allows you to encapsulate and carry the scope around. Later, you can execute a piece of code in the context of that binding, using `eval`. 

The `Kernel#binding` method returns the current binding object. A binding object encapsulates the variables, methods, and  `self`. 

You can pass a binding object as the second argument of the `Kernel#eval` method, establishing the environment for the evaluation.  `Kernel#eval` takes a string that contains Ruby code, executes it, and returns the result. 

```ruby
eval %q(
  def run(task)
    puts "running task: #{task}"
  end
)

run "compile"

# Output
# running task: compile
```

The following example illustrates how `eval` returns a different value for the language for different bindings. 

```ruby
language = "JavaScript"

puts eval("puts language", binding)  # JavaScript

def get_binding
  language = "C-Sharp"
  binding
end

net_binding = get_binding
puts eval("puts language", net_binding)  # C-Sharp

class Ruby
  def get_binding
    language = "Ruby"
    binding
  end
end

rails_binding = Ruby.new.get_binding
puts eval("puts language", rails_binding)  # Ruby
```

Ruby provides a constant called `TOPLEVEL_BINDING` that returns the binding of the top-level scope. Use it to access the top-level scope from anywhere in the program. 

```ruby
def run_ruby
  puts "running inside main"
end

class Ruby

  def run_ruby
    puts "running inside Ruby"
  end

  def exec
    eval "run_ruby", binding  # running inside Ruby
    eval "run_ruby", TOPLEVEL_BINDING  # running inside main
  end
end

Ruby.new.exec
```

At its core, `irb` is a simple program that parses standard input or a file and passes each line to `eval`. Even `pry` does something similar. 

*from: [Metaprogramming Ruby 2](https://learning.oreilly.com/library/view/metaprogramming-ruby-2/9781941222751/)*