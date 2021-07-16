---
layout: post
title: Things C# Programmers Should Know About Ruby
tags: ruby
---

While reading one of DHH's old [blog post](https://weblog.rubyonrails.org/2005/1/30/10-things-every-java-programmer-should-know-about-ruby/) on the [official Rails blog](https://weblog.rubyonrails.org/), I came across the following article from the late Jim Weirich, who lists [10 Things Every Java Programmer Should Know About Ruby](https://weblog.rubyonrails.org/2005/1/30/10-things-every-java-programmer-should-know-about-ruby/). I think it applies equally well to C# developers. 

Here is a list of things that resonated. 

1. Ruby classes are Objects (therefore `String.new`, not `new String()`)
2. Everything is an Object

3. Compared to Java, XML is agile. Compared to Ruby, XML is Heavy.

4. Ruby does not have type casting.

5. **Don't worry about interfaces, enjoy Duck Typing.**
6. No method overloading.

7. Enjoy closures and blocks.

8. Don't worry about early performance optimization.

9. Web-development is possible with other languages besides Java.

10. Ruby has MVC and OO programming and libraries, but drop any preconceptions.

11. Ruby is a language to be used everywhere. You use it even in templates. 

12. Ruby is not a Silver Bullet, unlike Java, right? :-)

13. In Ruby data is strongly typed, but variables are *not*

14. you can have variable number of parameters, and multiple return values

15. Once you start coding Ruby, going back to Java is painful.

16. "." (dot) is a method call operator. "::" (colon-colon) is a scope operator.

17. Java static methods do not (quite) translate to Ruby class methods.

18. CamelCase for class names, names_with_underscores for methods and variables.

19. local_variable, @instance_variable, $global_variable, Constants, (and @@class_variables)

20. Everything is an expression.

21. **stop writing so much code**
22. That you can write Ruby in Java ( http://jruby.sourceforge.net )

23. `ri` is your friend. `irb` is your other friend.
24. Reflection in Ruby is much easier than in Java, and more deeply into the language than the java.lang.reflect tack-on.

25. `eval`
26. the builtin classes are much faster because they're written in C and not Ruby

27. Boolean methods end in `?`. Dangerous methods end in `!`

28. Avoid external utility classes.

29. You probably don't need Factories.

30. Enumerable is your friend.

31. Typing is the enemy.

32. No external configuration files.

33. `method_missing`
34. Ruby classes are always "open".

35. Singleton methods

36. no semi-colons, optional parenthesis

37. Ruby packaging vs Java packaging

38. you can use string interpolation, ex: "x: #{@myvar}" instead of having to say "x:" + myvar'

39. ruby has multiple inheritance through mixins (this is sooo nice to have)

40. ruby has shortcuts for accessor methods which reduces alot of redundant coding in java

41. writing code in ruby, can improve the code you write in java

42. No explicit types. Probably the most disconcerting thing for a javahead

43. you cannot rely on the compiler to catch trivial mistakes

44. Think in terms of methods (behaviors) instead of classes.

45. KISS

46. Discipline. Because of its inherent flexibility, Ruby require more self-discipline

47. Ruby is agile, perfectly suited for XP

48. Ruby is dynamic. You can add, remove and modify objects, classes and methods at runtime.

49. Ruby has extensive reflection capabilities

50. **Ruby is strongly typed, not statically typed**
51. For good (but subtle) reasons, you have to leave the '++' and '--' behind.

52. you can fit in your mind and write code without looking at the docs every six minutes.

53. less syntax and less typing.

54. Fixes what's wrong with Python.

55. It's super productive (like Perl, Python and Smalltalk)- maybe 5-10x Java.

56. Is a lot like Smalltalk, but doesn't look as funny.

57. Is a lot like JavaScript, but more OO and more for full-app development.

58. Blocks and Closures

59. Open Classes

60. Duck Typing

61. Use blocks for transactional behavior like like File.open does.

62. An instance of a class can be extended to be subtly different, without needing to subclass.

63. you can change your mind about whether .foo is a simple property or a complex method call, without affecting the interface to your class.


Hope this helps. 
