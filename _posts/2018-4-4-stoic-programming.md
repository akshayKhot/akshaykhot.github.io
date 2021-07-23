---
layout: post
title: Stoic Programming
tags: thoughts
---

I have been studying Stoicism for more than 2 years now. The more I read Seneca, Marcus Aurelius and Epictetus, the more I realize how Stoic principles can be valuable when applied to programming. This post is a quick reminder to myself when I am writing software.

**Negative Visualization**

1. What’s the worst that can happen?
2. Imagining everything that can go horribly wrong, before I write even a single line of code.
3. Errors that can happen, bugs that creep in, unexpected exceptions, off-by-one errors, null-pointers, invalid inputs. Thinking on this may enforce reliable, robust code.
4. The software I am working on has failed. Why?
5. The codebase is a giant ball of mud, spaghetti code everywhere.
6. The software project got cancelled, and all the beautiful, clean code that I wrote using TDD is thrown away.
7. As you write code, silently reflect that this might be the last line of code that you might ever write. Might force you to write better code.

**Trichotomy of Control**

1. Things over which I have complete control: Code that I write, patterns and practices that I follow, testing the code I have written
2. Things over which I have no control at all: Underlying framework(.net, jvm), 3rd party libraries, Getting fired from the company
3. Things over which I have some but not complete control: Customer requirements, Management, Working in a team

**Hedonic Adaptation**

1. After you are exposed to a luxurious lifestyle, you might lose your ability to enjoy simple things. Embrace Discomfort.
2. Realizing the fact that I am coding in a programming environment and working with tools that would have been a dream world for programmers in the 80’s. Being grateful that I don’t have to write code in binary(0110101), Assembly(mov dl dh), or even C.
3. I have been programming on Visual Studio/IntelliJ/IDEs for more than 5 years now, and have almost forgotten how painful it was writing big Java programs on a Notepad(or sometimes on paper!) in my first year of college, back in 2009. So, whenever I find myself complaining about Visual Studio, open Notepad and try to code without any intellisense or compile-time errors.
4. Whenever I find myself complaining about C#, fire up 8086 microprocessor simulator, and write some assembly code.
5. Whenever I find myself complaining about TypeScript, write some plain Javascript using Closures, Callback hell, and try to figure out scope of ’this’ variable.

**Simplicity**

1. Not trying to show off how smart you are, by writing complex code when a simple solution would suffice.
2. Not trying to impress anyone, by sounding clever, by showing off how much you know, by using unnecessary complex jargon.
3. Writing the code as simple and readable as possible. Reading code is difficult.

**Stoic Meditation**

1. Taking pause, and reflecting on the code that I just wrote.
2. Not attaching my identity to the code/software I am building. Practicing detachment.
3. Not boasting/taking unnecessary pride at my work, avoiding self-serving biases.
4. Learning to enjoy the fact that I am getting paid to write software, without feeling entitled to it, and without clinging to it.

**Avoiding Intense Ideology**

1. Not getting wrapped in the latest fad/trend/framework in technology. Agile is a software development methodology, not a religion. TDD is a practice, not a rule.
2. Remembering that everything I hear is an opinion, not a fact. Everything I see is a perception, not absolute reality.
3. Being willing to change my mind when new facts emerge which contradict my pre-existing beliefs. e.g. Decision to stop working with Angular/Backbone/Knockout after Aurelia was released.
4. Paraphrasing Marcus Aurelius: “Waste no more time arguing about what a good programmer should be. Be one.”
5. Not having opinions on things that you don’t understand. Not having opinions unless you know the other side’s argument better than they do.

**Having Empathy when reading/reviewing code.**

1. I get frustrated when reading code written by me 2-3 years ago. I also get annoyed when reading buggy code written by other people, e.g. Poorly named variables, long methods, not enough error checking, unnecessary comments, etc.
2. Some techniques I am trying to use when dealing with my/others’ mistakes, which helps me maintain my sanity :
   - Never assume bad intentions when stupidity will suffice.
   - Never assume stupidity when ignorance will suffice.
   - Never assume ignorance when forgivable error will suffice.
   - Never assume error when information you hadn’t adequately accounted for will suffice.