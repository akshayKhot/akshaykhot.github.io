---
layout: post
title: Joining Arrays in Ruby
tags: ruby
excerpt_separator: <!--more-->
---

While reading one of David's old [blog](https://weblog.rubyonrails.org/2006/3/1/new-in-rails-enumerable-group_by-and-array-in_groups_of/) posts from the [Riding Rails](https://weblog.rubyonrails.org/) weblog, I came across a nifty way to join the values in an array. 

Typically, you'd do this to join arrays:

```ruby
> %w(1 2 3).join(", ")
=> "1, 2, 3"
```

However, multiplying an array with a separator accomplishes the same.

```ruby
> %w(a b c d e) * "-"
=> "a-b-c-d-e"

> %w(a b c d e) * ", "
=> "a, b, c, d, e"
```

Is it concise? Definitely. Radable and expressive? I am not sure. However, it rhymes with the Ruby way of giving the programmer [freedom to choose](https://akshaykhot.com/presence-in-array/). 

