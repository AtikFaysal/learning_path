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
> An algorithm has quadratic time complexity when the running time is proportional to the square of the input size. That means if input size `n` doubles, the number of operations becomes four times more (`n²`).

### Common use case
* Nested loop 
* Brute-force search 
* Bubble sort, selection sort, insertion sort
* Checking all pairs in an array 
* Naive search in 2D matrix 
* Generating all possible ordered pairs 
* Transposing a matrix(with nested loops)
### Example

✅ 1. **Detecting Duplicate Pairs (Brute-force)**
```
fun hasDuplicatePair(list: List<Int>): Boolean {
    for (i in list.indices) {
        for (j in i + 1 until list.size) {
            if (list[i] == list[j]) return true
        }
    }
    return false
}
```

✅ 2. **All Unique Pairs of a List**
```
fun generatePairs(items: List<String>): List<Pair<String, String>> {
    val pairs = mutableListOf<Pair<String, String>>()
    for (i in items.indices) {
        for (j in i + 1 until items.size) {
            pairs.add(Pair(items[i], items[j]))
        }
    }
    return pairs
}
```

✅ 3. **Simple Matrix Multiplication**
```
fun multiplyMatrices(a: Array<IntArray>, b: Array<IntArray>): Array<IntArray> {
    val rows = a.size
    val cols = b[0].size
    val result = Array(rows) { IntArray(cols) }
    
    for (i in 0 until rows) {
        for (j in 0 until cols) {
            for (k in b.indices) {
                result[i][j] += a[i][k] * b[k][j]
            }
        }
    }
    return result
}
```

✅ 4. **Longest Common Substring (Dynamic Programming)**
```
fun longestCommonSubstring(a: String, b: String): Int {
    val dp = Array(a.length + 1) { IntArray(b.length + 1) }
    var maxLen = 0

    for (i in 1..a.length) {
        for (j in 1..b.length) {
            if (a[i - 1] == b[j - 1]) {
                dp[i][j] = dp[i - 1][j - 1] + 1
                maxLen = maxOf(maxLen, dp[i][j])
            }
        }
    }
    return maxLen
}
```

✅ 5. **Graph Representation via Adjacency Matrix**
```
val graph = Array(n) { BooleanArray(n) }

fun connect(i: Int, j: Int) {
    graph[i][j] = true
    graph[j][i] = true
}
```

**📊 Summary Table**

| Use Case                           | Code Pattern       | Complexity |
| ---------------------------------- | ------------------ | ---------- |
| Brute-force pair checking          | Double `for` loop  | O(n²)      |
| Generating all pairs               | Nested iteration   | O(n²)      |
| DP with 2D table                   | Matrix fill        | O(n²)      |
| Simple sorting (bubble, insertion) | Nested swaps       | O(n²)      |
| Adjacency matrix operations        | 2D graph traversal | O(n²)      |

*Logarithm time - O(log(n))*
> Logarithm time complexity, denoted as `O(log n)`, describes algorithms that reduce the problem size by a constant factor with each operation. These algorithms becomes slightly slower as the input grows, making them extremely efficient for large datasets.
> 
### Common use case
* Binary search 
* Searching in BSTs or Heaps
* Divide and conquer algorithm(like merge sort)
* Bit manipulation/ shifting
* Recursive halving patterns
* Finding elements on sorted matrix

### Example 

✅ 1. **Binary Search in a Sorted List**
```
fun binarySearch(arr: List<Int>, target: Int): Int {
    var low = 0
    var high = arr.lastIndex
    while (low <= high) {
        val mid = (low + high) / 2
        when {
            arr[mid] == target -> return mid
            arr[mid] < target -> low = mid + 1
            else -> high = mid - 1
        }
    }
    return -1
}
```

✅ 2. **Binary Search for First True in a Boolean Function**
```
fun findFirstTrue(n: Int, isGood: (Int) -> Boolean): Int {
    var low = 0
    var high = n
    while (low < high) {
        val mid = (low + high) / 2
        if (isGood(mid)) high = mid else low = mid + 1
    }
    return low
}
```

✅ 3. **Searching in a Binary Search Tree (BST)**
```
data class Node(val value: Int, val left: Node? = null, val right: Node? = null)

fun searchBST(root: Node?, target: Int): Boolean {
    var current = root
    while (current != null) {
        if (current.value == target) return true
        current = if (target < current.value) current.left else current.right
    }
    return false
}
```

✅ 4. **Heap Insertion or Deletion (Min/Max Heap)**
```
val heap = PriorityQueue<Int>()  // Min heap by default

heap.add(5)  // O(log n)
heap.add(3)
heap.add(7)

val min = heap.poll()  // O(log n)
```

✅ 5. **Bit Manipulation Tricks (Right Shift)**
```
fun countBits(n: Int): Int {
    var count = 0
    var x = n
    while (x > 0) {
        count += x and 1
        x = x shr 1  // divide by 2
    }
    return count
}
```

**📊 Summary Table**

| Algorithm / Technique        | Time Complexity | Notes                             |
| ---------------------------- | --------------- | --------------------------------- |
| Binary search (sorted array) | O(log n)        | Classic example                   |
| Binary search on answer      | O(log n)        | Optimization problems             |
| Search in balanced BST       | O(log n)        | Tree height = log n               |
| Heap insert / delete         | O(log n)        | Used in Dijkstra, priority queues |
| Bitwise shifts or division   | O(log n)        | Efficient number manipulation     |

*Linearithmic - O(n log(n))*
>Linearithmic time complexity, denoted as `O(l log n)`, combines linear `O(n)` and logarithmic `O(log n)` behavior. It's one of the most efficient complexities for sorting and searching problems and is often seen in divide-and-conquer algorithms.

### Common use case 
* Sorting large arrays or lists efficiently 
* Constructing heaps or balanced trees 
* Algorithms that use recursive halving and merging 
* Finding inversion counts or handling range queries 
* Computational geometry(Line insertion, Convex hull)

### Example

✅ 1. **Merge Sort**
```
fun mergeSort(arr: List<Int>): List<Int> {
    if (arr.size <= 1) return arr

    val mid = arr.size / 2
    val left = mergeSort(arr.subList(0, mid))
    val right = mergeSort(arr.subList(mid, arr.size))

    return merge(left, right)
}

fun merge(left: List<Int>, right: List<Int>): List<Int> {
    val result = mutableListOf<Int>()
    var i = 0
    var j = 0
    while (i < left.size && j < right.size) {
        if (left[i] <= right[j]) result.add(left[i++])
        else result.add(right[j++])
    }
    while (i < left.size) result.add(left[i++])
    while (j < right.size) result.add(right[j++])
    return result
}
```

✅ 2. **Heap Sort (Using PriorityQueue)**
```
fun heapSort(arr: List<Int>): List<Int> {
    val heap = PriorityQueue<Int>()
    for (num in arr) heap.add(num) // O(n log n)

    val sorted = mutableListOf<Int>()
    while (heap.isNotEmpty()) {
        sorted.add(heap.poll()) // O(log n)
    }
    return sorted
}
```

✅ 3. **Sorting with Kotlin’s Built-in Sort**
```
val list = mutableListOf(5, 3, 9, 1, 4)
list.sort() // Under the hood: Dual Pivot QuickSort (O(n log n))
```

✅ 4. **Count Inversions in an Array**
Inversions = pairs where `arr[i] > arr[j]` and `i < j`.  
Solved via modified merge sort.
```
fun countInversions(arr: IntArray): Int {
    val temp = IntArray(arr.size)
    return mergeSortCount(arr, temp, 0, arr.size - 1)
}

fun mergeSortCount(arr: IntArray, temp: IntArray, left: Int, right: Int): Int {
    var count = 0
    if (left < right) {
        val mid = (left + right) / 2
        count += mergeSortCount(arr, temp, left, mid)
        count += mergeSortCount(arr, temp, mid + 1, right)
        count += mergeAndCount(arr, temp, left, mid, right)
    }
    return count
}

fun mergeAndCount(arr: IntArray, temp: IntArray, left: Int, mid: Int, right: Int): Int {
    var i = left
    var j = mid + 1
    var k = left
    var count = 0

    while (i <= mid && j <= right) {
        if (arr[i] <= arr[j]) temp[k++] = arr[i++]
        else {
            temp[k++] = arr[j++]
            count += (mid - i + 1)
        }
    }

    while (i <= mid) temp[k++] = arr[i++]
    while (j <= right) temp[k++] = arr[j++]

    for (p in left..right) arr[p] = temp[p]
    return count
}
```

✅ 5. **Balanced Tree Construction from Sorted Array**
```
fun sortedArrayToBST(nums: IntArray): TreeNode? {
    fun build(low: Int, high: Int): TreeNode? {
        if (low > high) return null
        val mid = (low + high) / 2
        return TreeNode(nums[mid]).apply {
            left = build(low, mid - 1)
            right = build(mid + 1, high)
        }
    }
    return build(0, nums.lastIndex)
}
```

**📊 Summary Table**

|Algorithm / Technique|Time Complexity|Used For|
|---|---|---|
|Merge Sort|O(n log n)|Efficient sorting|
|Heap Sort / PriorityQueue|O(n log n)|Sorting, scheduling|
|Built-in `sort()`|O(n log n)|Optimized real-world sorting|
|Inversion Count|O(n log n)|Algorithmic interview problems|
|Balanced BST from sorted|O(n log n)|Tree construction, divide and conquer|

*Exponential time - O(2ⁿ)*
> Exponential time complexity, denoted as `O(2ⁿ)`, describes algorithms whose runtime doubles with each additional input element. These algorithms are `computationally expensive` and become `unfeasible` for even moderately sized inputs (n > 30).

### Common use case
* Subset generation
* Permutations
* Recursive Fibonacci (naive)
* Traveling Salesman Problem (TSP)
* Knapsack problem (without DP)

✅ 1. **Naive Recursive Fibonacci**
```
fun fib(n: Int): Int {
    if (n <= 1) return n
    return fib(n - 1) + fib(n - 2) // Two recursive calls
}
```

✅ 2. **Generating All Subsets (Power Set)**
```
fun generateSubsets(nums: List<Int>): List<List<Int>> {
    val result = mutableListOf<List<Int>>()
    
    fun backtrack(index: Int, current: List<Int>) {
        if (index == nums.size) {
            result.add(current)
            return
        }
        // Exclude
        backtrack(index + 1, current)
        // Include
        backtrack(index + 1, current + nums[index])
    }

    backtrack(0, emptyList())
    return result
}
```

✅ 3. **Generating All Permutations**
```
fun <T> generatePermutations(items: List<T>): List<List<T>> {
    val result = mutableListOf<List<T>>()
    val used = BooleanArray(items.size)
    
    fun backtrack(current: MutableList<T>) {
        if (current.size == items.size) {
            result.add(current.toList())
            return
        }
        for (i in items.indices) {
            if (!used[i]) {
                used[i] = true
                current.add(items[i])
                backtrack(current)
                current.removeAt(current.lastIndex)
                used[i] = false
            }
        }
    }

    backtrack(mutableListOf())
    return result
}
```

✅ 4. **Recursive Knapsack (0/1 Problem)** — No memoization
```
fun knapsack(weights: IntArray, values: IntArray, capacity: Int, n: Int): Int {
    if (n == 0 || capacity == 0) return 0
    return if (weights[n - 1] > capacity) {
        knapsack(weights, values, capacity, n - 1)
    } else {
        maxOf(
            knapsack(weights, values, capacity, n - 1),
            values[n - 1] + knapsack(weights, values, capacity - weights[n - 1], n - 1)
        )
    }
}
```

*Square root time - O(√n)*
>Square root time complexity, denoted as `O(√n)`, describes algorithms whose runtime grows proportionally to the square root of the input size. These algorithms are `faster than linear (O(n))` but `slower than logarithmic (O(log n))`, making them useful in specific scenarios like `number theory, searching, and primality testing`.

### Common use case 
* Prime number checking
* Counting or generating factors of a number
* Divisor enumeration
* Square root decomposition algorithms
* Optimization in loops where checking all values isn't necessary
* 1. Factorization (Find all prime factors of a number)
### Example
✅ 1. **Prime Number Check**
```
fun isPrime(n: Int): Boolean {
    if (n <= 1) return false
    for (i in 2..sqrt(n.toDouble()).toInt()) {
        if (n % i == 0) return false
    }
    return true
}
```

✅ 2. **Find All Divisors of a Number**
```
fun findDivisors(n: Int): List<Int> {
    val divisors = mutableListOf<Int>()
    for (i in 1..sqrt(n.toDouble()).toInt()) {
        if (n % i == 0) {
            divisors.add(i)
            if (i != n / i) divisors.add(n / i)
        }
    }
    return divisors.sorted()
}
```

✅ 3. **Perfect Square Detection**
```
fun isPerfectSquare(n: Int): Boolean {
    val root = sqrt(n.toDouble()).toInt()
    return root * root == n
}
```

✅ 4. **Count Prime Factors (Brute-Optimized)**
```
fun countPrimeFactors(n: Int): Int {
    var num = n
    var count = 0

    // Divide out factor 2 first
    while (num % 2 == 0) {
        count++
        num /= 2
    }

    // Try odd factors from 3 to sqrt(n)
    var i = 3
    while (i * i <= num) {
        while (num % i == 0) {
            count++
            num /= i
        }
        i += 2
    }

    // Remaining prime factor (if any)
    if (num > 2) count++

    return count
}
```

*Factorial time - O(n!)*
>Factorial time complexity, denoted as `O(n!)`, describes algorithms whose runtime grows proportionally to the factorial of the input size `n`.
>
>`n! = n × (n - 1) × (n - 2) × ... × 2 × 1 `
>
> These algorithms are `extremely inefficient` and become `unusable for n > 20` (since 20! ≈ 2.4 × 10¹⁸ operations).

### Common use case
* Permutation generation
* Traveling Salesman Problem (TSP) — brute force
* N-Queens Problem (naive solution)
* Anagram generation
* Sudoku solvers (brute-force backtracking)
* Combinatorial Problems (Subset generation, graph coloring)
### Example 

✅ 1. **Generating All Permutations of a List**
```
fun <T> generatePermutations(items: List<T>): List<List<T>> {
    val result = mutableListOf<List<T>>()
    val used = BooleanArray(items.size)

    fun backtrack(current: MutableList<T>) {
        if (current.size == items.size) {
            result.add(current.toList())
            return
        }
        for (i in items.indices) {
            if (!used[i]) {
                used[i] = true
                current.add(items[i])
                backtrack(current)
                current.removeAt(current.lastIndex)
                used[i] = false
            }
        }
    }

    backtrack(mutableListOf())
    return result
}
```

✅ 2. **Solving the Traveling Salesman Problem (Brute Force)**
```
fun tsp(cost: Array<IntArray>, visited: BooleanArray, pos: Int, count: Int, costSoFar: Int, n: Int, minCost: Int): Int {
    if (count == n && cost[pos][0] > 0) {
        return costSoFar + cost[pos][0]
    }

    var min = minCost
    for (i in 0 until n) {
        if (!visited[i] && cost[pos][i] > 0) {
            visited[i] = true
            val newCost = tsp(cost, visited, i, count + 1, costSoFar + cost[pos][i], n, min)
            min = minOf(min, newCost)
            visited[i] = false
        }
    }
    return min
}
```

✅ 3. **N-Queens Problem (Backtracking)**
```
fun solveNQueens(n: Int): List<List<String>> {
    val solutions = mutableListOf<List<String>>()
    val board = MutableList(n) { CharArray(n) { '.' } }

    fun isSafe(row: Int, col: Int): Boolean {
        for (i in 0 until row) {
            if (board[i][col] == 'Q') return false
            if (col - row + i >= 0 && board[i][col - row + i] == 'Q') return false
            if (col + row - i < n && board[i][col + row - i] == 'Q') return false
        }
        return true
    }

    fun backtrack(row: Int) {
        if (row == n) {
            solutions.add(board.map { it.joinToString("") })
            return
        }
        for (col in 0 until n) {
            if (isSafe(row, col)) {
                board[row][col] = 'Q'
                backtrack(row + 1)
                board[row][col] = '.'
            }
        }
    }

    backtrack(0)
    return solutions
}
```
