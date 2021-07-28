---
layout: post
title: Ruby Sweetness
tags: ruby
img: rails/double-splat.png
---

In my journey to learn and master Ruby, I keep coming across new syntactic sugar every day that makes me happy. This morning, I stumbled upon the double-splat `**` operator while learning about the `FileUtils` standard library. 

Now, I'd already seen the splat `*`, which converts one or more arguments to an array, so I was curious what the double-splat did. 

The results were impressive. 

```ruby
def run(a, *b, **c)
  pp [a, b, c]
end

# [10, [], {}]
run 10 

# [10, [20], {}]
run 10, 20 

# [10, [20, 30, 40], {}]
run 10, 20, 30, 40

# [10, [20, 30, 40, [50, 60]], {}]
run 10, 20, 30, 40, [50, 60]

# [10, [20, 30, 40], {:name=>"akshay", :age=>29}]
run 10, 20, 30, 40, name: "akshay", age: 29

# [10, [], {:name=>"akshay", :age=>29}]
run 10, name: "akshay", age: 29
```

The double-splat operator was introduced in Ruby 2.0. It does the same thing for keyword arguments what the splat operator does for plain arguments. It converts all the key-value pairs to a single hash. 

<a target="_blank" href="{{ site.images }}/{{ page.img }}">
  <img src="{{ site.images }}/{{ page.img }}" alt="Are you not entertained?">
</a>  