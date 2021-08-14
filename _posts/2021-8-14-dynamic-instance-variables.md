---
layout: post
title: Dynamic Instance Variables in Ruby
tags: ruby
---

Ruby continues to surprise me. 

While reading [Metaprogramming Ruby](https://learning.oreilly.com/library/view/metaprogramming-ruby-2/9781941222751/) this evening, I learned that there is no connection between an object’s class and its instance variables in Ruby, unlike C#. The interpreter creates instance variables on the fly, when you assign them a value. 

For example, a `Task` object won't have the `state` instance variable until I call the `run` method on it. 

```ruby
class Task
  def run
    @state = :running
  end
  
  def stop
    @finished = true
  end
end

> compile = Task.new
> compile.instance_variables
=> []

> compile.run
=> :running

> compile.instance_variables
=> [:@state]
```

It's possible to have objects of the same class with different instance variables. 

For example, if I create another `Task` object and call the `stop` method, it won't have a `@state` instance variable. 

```ruby
> interpret = Task.new
> interpret.instance_variables
=> []

> interpret.stop
=> true

> interpret.instance_variables
=> [:@finished]
```

Very interesting. 
