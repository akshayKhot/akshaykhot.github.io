---
layout: post
title: How to Check if a Variable is Defined?
tags: ruby
---

The `defined?` expression allows you to test if a variable is defined or not. If it isn't defined, it returns `nil`. Otherwise, it returns a string that provides information about the variable. 

```ruby
> defined? a
=> nil

> a = 10
=> 10
> defined? a
=> "local-variable"

> defined? nil
=> "nil"

> defined? Array
=> "constant"
> defined? String
=> "constant"

* class Person
> end
> defined? Person
=> "constant"

> defined? 10
=> "expression"
```

A variable set to `nil` is also initialized. 

```ruby
> b = nil
=> nil

> defined? b
=> "local-variable"
```

