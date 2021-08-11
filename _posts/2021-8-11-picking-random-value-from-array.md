---
layout: post
title: Picking Random Value from an Array
tags: ruby
---

Often you want to pick a random value from an array of variable length. Typically, you would first find a random integer between zero and length of the array, and then use that as an index to pick the value. For example,

```ruby
> languages = %w(ruby c-sharp java python cpp golang javascript)
=> ["ruby", "c-sharp", "java", "python", "cpp", "golang", "javascript"]
> languages[rand(languages.length)]
=> "c-sharp"
> languages[rand(languages.length)]
=> "javascript"
> languages[rand(languages.length)]
=> "java"
```

**Is there an idiomatic way to do this in Ruby?** Something that abstracts how we are generating a random number and using it as an index? 

It turns out, there is. 

Just use [`Array#sample`](https://ruby-doc.org/core-3.0.1/Array.html#method-i-sample). When no arguments are given, `sample` returns a random element from the array. 

```ruby
> languages.sample
=> "java"
> languages.sample
=> "c-sharp"
> languages.sample
=> "golang"
```

It returns `nil` if the array is empty. 

```ruby
> [].sample
=> nil
```

If you pass a number `n`,  it returns a new array that contains `n` random elements from the original array. 

```ruby
> languages.sample(3)
=> ["c-sharp", "ruby", "javascript"]
> languages.sample(1)
=> ["javascript"]
> languages.sample(4)
=> ["javascript", "java", "golang", "python"]
```

If `n` is larger than the length of the array, `sample` returns a new array that contains all elements from the original array in shuffled order. No duplicates are introduced. 

```ruby
> languages.sample(10)
=> ["golang", "javascript", "ruby", "python", "cpp", "java", "c-sharp"]
```

Ruby makes me happy. 
