---
layout: post
title: When to Create a Custom Class
tags: ruby
---

These are my notes from the second chapter of [Polished Ruby Programming](/polished-ruby-programming) by Jeremy Evans. It explores when creating a custom class or a data structure is a good idea and when it's not. 

How you design and structure your classes has a huge effect on how intuitive and maintainable your code is. 

Choosing to create a custom class is always a trade-off, in that all classes result in some conceptual overhead. Everyone who works with the code now has to learn how to use the class correctly and be productive while using it. 

**Benefits of creating a custom class**

1. It encapsulates state and logic and controls access to its data.
2. It provides a simple way for calling functions on the instances of that class.

If others are going to access the data and the logic, then it makes sense to encapsulate it into a custom class. However, if it's just an internal implementation detail used by another class with its own implementation, then creating a custom class is probably unnecessary, especially if one of the core classes in Ruby provides the same features or API.

Another thing to keep in mind is how many places you will be using this class. If multiple places in the codebase will need it, a custom class is appropriate. However, if it's only used at a single location and doesn't need to be directly accessed by others, you shouldn't create a custom class for it (yet). 

(I don't necessarily agree with the above point, being a big fan of domain-driven design. I think custom classes reduce the conceptual overhead and let you express the concepts in a more powerful way. I prefer to introduce new classes even if they are used once internally)
