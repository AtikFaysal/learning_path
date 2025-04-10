As dive deeper into algorithm & data structure, one concept that keeps coming up is time complexity. At first, it seems intimidating, but as i broke it down, it's become much clearer. In this post I'll share my understanding on time complexity, why it matters and how to analyze it. 
### What is time complexity
> `Time complexity` is a way to describe how the running time of an algorithm increases relative to the size of its input. Instead of measuring the exact execution time (which can vary based on hardware and environment), we use `Big-O` notation to express an algorithm’s efficiency in terms of input size `n`.
> Time complexity helps us analyze and compare the performance of different algorithms by estimating how quickly their execution time grows as input size increases. Common notations include `O(1)`, `O(n)`, `O(n²)`, etc., which represent the `worst-case` or `upper bound` of an algorithm’s growth rate, while ignoring constant factors and less significant terms.

`This graph illustrates how different time complexity classes grow as the input size (`n`) increases. The curves represent the number of operations or computations an algorithm performs, from the most efficient to the least efficient.`

![[1_dWet_YU-5072Kcko7LzsuQ.jpg]]

`Some of common time comlexity are explained in the given below`
### Constants time - O(1)
>Constant time complexity means that execution time of the algorithm does not depend on input size, it always takes same time to execute the algorithm, no matter how large input size is. 
>This is the most efficient type of time complexity — it's fast and predictable.
### Common use case
* Accessing an array element by index
* Inserting/removing element at last index of an array 
* Pushing/Popping from stack 
* Enqueuing/Dequeuing from an queue (with proper implementation)
* Hash table lookup (in ideal cases)
* Swiping variable 
* Basic arithmetic or assignment 
* Early return conditions
### Example

 ✅ 1. **Accessing `Map` Keys**
```
val cache = hashMapOf("A" to 1, "B" to 2) 
val value = cache["B"] // O(1) on average
```

✅ 2. **Set Membership Test**
```
val seen = hashSetOf("apple", "banana")
if ("banana" in seen) {
    println("Already seen") // O(1)
}
```

✅ 3. **Deque Operations**
```
val deque: ArrayDeque<Int> = ArrayDeque()
deque.addFirst(10)  // O(1)
deque.removeLast()  // O(1)
```

✅ 4. **Bit Manipulation Tricks**
```
val x = 42
val isEven = x and 1 == 0  // O(1) bitwise check
```

✅ 5. **Math with Constant Formulas**
```
fun triangleNumber(n: Int): Int = n * (n + 1) / 2  // O(1)
```

✅ 6. **Using Memoized Results**
```
val memo = listOf(1, 1, 2, 3, 5, 8, 13) // Precomputed Fibonacci
fun getFibonacci(n: Int): Int = memo[n] // O(1)
```
### Summary
- **O(1)** = Same time no matter the input
- Ideal for: lookups, math, logic, hashing
- **Advanced uses**: HashMaps, Sets, memoization, bit tricks, deque

### Linear time - O(n)
> Linear time complexity denoted as `O(n)`, describe an algorithm whose execution time grows directly proportional to the input size. In simple word if your input size double, time takes double 

```
val list = listOf(1, 2, 3, 4, 5)
for (item in list) {
    println(item)  // O(n)
}
```
### Common use case 
* Scanning/Searching data in array or list
* Calculating sum/average of elements 
* Copying an array 
* Most basic search operation in unsorted array 
* Finding min/max element

### Example

✅ 1. **Searching for an Element in a List**
```
fun containsValue(list: List<Int>, target: Int): Boolean {
    for (num in list) {
        if (num == target) return true // Still O(n) in worst case
    }
    return false
}
//Even if it returns early, worst-case time is O(n).
```

✅ 2. **Counting Frequencies Using a HashMap**
```
fun countFrequencies(words: List<String>): Map<String, Int> {
    val freq = mutableMapOf<String, Int>()
    for (word in words) {
        freq[word] = freq.getOrDefault(word, 0) + 1
    }
    return freq
}
```
- One pass through the list → O(n)
- HashMap operations are O(1) on average

✅ 3. **Filtering and Mapping (Functional Style)**
```
val evenSquares = (1..1_000_000)
    .filter { it % 2 == 0 }
    .map { it * it }
```

✅ 4. **Removing Duplicates While Preserving Order**
```
fun removeDuplicates(list: List<String>): List<String> {
    val seen = mutableSetOf<String>()
    val result = mutableListOf<String>()
    for (item in list) {
        if (item !in seen) {
            seen.add(item)
            result.add(item)
        }
    }
    return result
}
```

✅ 5. **Reading Files Line by Line**
```
File("data.txt").useLines { lines ->
    for (line in lines) {
        println(line) // O(n) where n = number of lines
    }
}
```

*Quadratic time - O(n²)*
*Logarithm time - O(log(n))*
*Linearithmic - O(n log(n))*
*Exponential time - O(2ⁿ)*
*Square root time - O(√n)*
*Factorial time - O(n!)*




