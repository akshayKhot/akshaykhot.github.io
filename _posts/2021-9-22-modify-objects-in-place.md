---
layout: post
title: Modify Objects In-Place
tags: ruby
---

Every time you create or copy something in memory, you add work for GC. Here are some tips from the book [Ruby Performance Optimization](https://learning.oreilly.com/library/view/ruby-performance-optimization/9781680501681/) to write code without using too much memory. 

- Modify strings in-place. 

Instead of making a changed copy, you change the original string. Look for "bang!" functions, such as `trim!`, `gsub!`, `slice!` etc. Use them when you don't need the original string. 

```ruby
require_relative "./wrapper" # see above for wrapper script

def modify_strings_in_place
  str = "X" * 1024 * 1024 * 10
  measure("copy") { tmp = str.downcase }
  measure("in-place") { str.downcase! }
end

modify_strings_in_place

# Output
# {"3.0.2":{"gc":"disabled","time":0.01,"gc_count":0,"memory":"10 MB"}}
# {"3.0.2":{"gc":"disabled","time":0.01,"gc_count":0,"memory":"0 MB"}}
```

- Use the shift operator `<<` to append strings, instead of using `+=`. 

```ruby
def append_to_string
  measure do
    x = "foo"
    100_000.times { x += "bar" }
  end

  measure do
    x = "foo"
    100_000.times { x << "bar" }
  end
end

append_to_string

# Output
# {"3.0.2":{"gc":"disabled","time":9.42,"gc_count":0,"memory":"6412 MB"}}
# {"3.0.2":{"gc":"disabled","time":0.01,"gc_count":0,"memory":"-2 MB"}}
```

When you use `+=`, Ruby creates an intermediate string and assigns it to the original string after appending. 

- Modify Arrays in-place. Do not create a modified copy of the same array unless really necessary. 

```ruby
def modify_array_in_place
  data = Array.new(100) { "x" * 1024 * 1024 }

  measure { data.map { |str| str.upcase } }
  measure { data.map { |str| str.upcase! } }
end

modify_array_in_place

# Output
# {"3.0.2":{"gc":"disabled","time":0.12,"gc_count":0,"memory":"100 MB"}}
# {"3.0.2":{"gc":"disabled","time":0.1,"gc_count":0,"memory":"0 MB"}}
```

