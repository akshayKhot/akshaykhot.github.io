---
layout: post
title: Programming Pearls
date: 2021-8-24
img: programming_pearls.jpeg
---

This books contains Jon Bentley's essays from his column in Communications of the Association for Computing Machinery. It describes practical programming techniques and fundamental design principles. 

<div class="book">
<a target="_blank" href="{{ site.bookshelf }}/{{ page.img }}">
  <img src="{{ site.bookshelf }}/{{ page.img }}" alt="{{page.title}}">
</a>
</div>

Careful analysis of a small problem can sometimes yield tremendous practical benefits. 

Sometimes, defining the problem constitutes about ninety percent of the battle. 

Simple programs are usually more reliable, secure, robust, and efficient than their complex cousins, and easier to build and maintain. 

Determining what the user really wants to do is an essential part of programming. 

**Algorithms and Data Structures**

Coding skill is just one small part of writing correct programs. The majority of the work happens in **problem definition, algorithm design**, and **data structure selection**. 

Data structures are important. A proper view of the data does indeed structure programs. Programs can be made smaller and better by restructuring their internal data. Good data structures can also reduce space-time complexity and increase portability and maintainability. 

> Don't write a big program when a little one will do. 

Before writing code, good programmers thoroughly understand the input, the output, and the intermediate data structures around which their programs are built. 

Bitmap: Represents a dense set over a finite domain when each element occurs at most once and no other data is associated with the element. Even if there are multiple elements or extra data, you can use a key from the finite domain in a hash. 

**Writing Correct Programs**

Most programmers grew up with "write your code, throw it over the wall, and have QA deal with the bugs".

When you debug, fix both the code and the false assertion. Understand the code at all times, and resist the urges to *just change it until it works*. 

Assertions are crucial during the maintenance of a program. When you pick up unfamiliar code, assertions about the program state give valuable insights. 

**Integration**

It's tempting to take the easy path: write the function, slip it into the system, and hope it runs. Sometimes, it works; most of the time, it leads to buggy systems. One has to grope around in the huge system to manipulate the little function. 

Wise programmers instead build scaffolding to give them easy access to the function. 

**Performance**

A computer system is designed at many levels, ranging from high-level software structure to the transistors in hardware. You can optimize at various levels. 

- Problem definition. The battle for a fast system can be won or lost in specifying the problem it is to solve. 
- System structure. The decomposition of a large system into modules is probably the single most important factor in determining its performance. 
- Algorithms and Data Structures. The keys to a fast module are usually the structures that represent its data and the algorithms that operate on the data. 
- Code tuning, system software, hardware can also result in significant performance enhancements. 

> The cheapest, fastest, and most reliable components of a computer system are those that aren't there. - Gordon Bell, DEC

These missing components never make mistakes, can't be broken into, and are easiest to design, document, test, and maintain. 

Before you dive into tuning the code for speedup, consider all possible levels and choose the one that delivers the most speedup for the least effort. 

> A good engineer knows enough to know what he doesn't know. 

John Roebling (builder of Brooklyn Bridge) was a good engineer, and he built a good bridge by employing a huge safety factor to compensate for his ignorance. Do we do that?

We should have a margin of safety while estimating performance, reliability, cost, size, and schedule to compensate for our ignorance. 

Code tuning locates the expensive parts of an existing program and then makes little changes to improve its speed.  

**Recommended Books**

- Conceptual Blockbusting: A Guide to Better Ideas: James L. Adams
- Code Complete: A Practical Handbook of Software Construction by Steve McConnell
- The Medical Detectives by Berton Rouche
- How to Lie with Statistics by Darrell Huff
- Data Structures and Algorithms by Aho, Hopcraft, and Ullman