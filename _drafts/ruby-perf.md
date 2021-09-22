80% of performance improvements come from memory optimization. 

Two common reasons for poor performance:

1. Extra memory allocation
2. Data structure copying

**Measure**

We need some way to know that the changes we make really improve performance. Use this [wrapper script](https://gist.github.com/akshayKhot/5950a03d942fa7e36210ac2ef1988af8) to measure.  

**Save Memory**

The first step to make your app faster is to save memory. Every time you create or copy something in memory, you add work for GC. Here are some best practices to write code without using too much memory. 

- [Modify Objects In-Place](/modify-objects-in-place)

- 

