As dive deeper into algorithm & data structure, one concept that keeps coming up is time complexity. At first, it seems intimidating, but as i broke it down, it's become much clearer. In this post I'll share my understanding on time complexity, why it matters and how to analyze it. 

***What is time complexity***
> `Time complexity` is a way to describe how the running time of an algorithm increases relative to the size of its input. Instead of measuring the exact execution time (which can vary based on hardware and environment), we use `Big-O` notation to express an algorithm’s efficiency in terms of input size `n`.
> Time complexity helps us analyze and compare the performance of different algorithms by estimating how quickly their execution time grows as input size increases. Common notations include `O(1)`, `O(n)`, `O(n²)`, etc., which represent the `worst-case` or `upper bound` of an algorithm’s growth rate, while ignoring constant factors and less significant terms.

This graph illustrates how different time complexity classes grow as the input size (`n`) increases. The curves represent the number of operations or computations an algorithm performs, from the most efficient to the least efficient.

![[1_dWet_YU-5072Kcko7LzsuQ.jpg]]


***Common Time Complexities***

*Constants time - O(1)*


