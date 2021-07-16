---
layout: post
title: Immutable Strings in Ruby
tags: ruby
---

A big difference between other programming languages and Ruby is that strings are mutable in Ruby. That means, one can modify a string in place. 

```ruby
line = "I love programming c-sharp"
puts line   # I love programming c-sharp

line.gsub!("c-sharp", "Ruby")
puts line   # I love programming Ruby
```

Here are some other methods that allow you to modify a string. 

1. `captialize!`: Converts the first character uppercase and remainder to lowercase.

2. `chomp!`: Removes the newline character from the end of the string. 

3. `chop!`: Removes the last character. 

4. `upcase!, downcase!`: Converts all the characters in the string to either uppercase or lowercase. 

5. `gsub!`: Replace all occurrences of pattern with replacement. 

6. `lstrip!, rstrip!, strip!`: Removes the whitespaces from either beginning or ending, or both. 

   