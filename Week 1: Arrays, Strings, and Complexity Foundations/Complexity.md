## Complexity Analysis for DSA: From Scratch

This is the core idea behind judging whether a solution is efficient enough for a problem.

### 1) What is complexity analysis?
Complexity analysis tells us how the runtime and memory usage of an algorithm grow as the input size increases.

- Input size is usually denoted as n, m, k, etc.
- We care about how performance changes when n becomes large.
- We do not care about constant-time differences like 2n vs 3n in big-O notation.

Example:
- If an algorithm takes 1000n operations, it is O(n)
- If it takes n² + 5n + 7, it is O(n²)

---

### 2) Why complexity matters in DSA
A correct solution may still fail if it is too slow.

The main goal:
- Find the fastest algorithm that fits the problem constraints
- Avoid brute force when n can be 10⁵ or 10⁶

If the input size is large, an algorithm with O(n²) may be too slow even if it is logically correct.

---

### 3) The most important parameters to learn

#### a) Input size
This is the main parameter.

Common notation:
- n = size of array or number of elements
- m = second dimension or another array size
- k = number of operations / groups / distinct values
- s = string length

Example:
- For an array of length n, complexity often depends on n
- For a matrix of size n × m, complexity depends on both

#### b) Time complexity
Measures how many basic operations are performed.

Typical questions:
- Does the algorithm loop over input once?
- Does it loop nested?
- Does it divide the problem in half?
- Does it revisit the same data repeatedly?

#### c) Space complexity
Measures extra memory used besides the input itself.

Examples:
- O(1) = constant extra memory
- O(n) = linear extra memory
- O(log n) = logarithmic extra memory
- O(n²) = quadratic extra memory

#### d) Constraints
Constraints tell us the maximum possible input size.

This is critical because it tells us what complexity is acceptable.

Examples:
- n ≤ 10³ → O(n²) may be okay
- n ≤ 10⁵ → O(n²) is too slow
- n ≤ 10⁶ → O(n log n) or O(n) is usually needed

---

### 4) Big-O, Big-Ω, and Big-Θ

#### Big-O: worst-case upper bound
This is the most common notation in DSA interviews.

We write:
- f(n) = O(g(n))

This means:
- f(n) grows no faster than g(n) asymptotically
- It gives an upper bound

Example:
- 3n + 5 = O(n)
- 2n² + 7n + 9 = O(n²)

#### Big-Ω: best-case lower bound
This is the lower bound.

Example:
- If an algorithm must at least inspect all n elements, then it is Ω(n)

#### Big-Θ: tight bound
This means both upper and lower bounds match.

Example:
- A loop running exactly n times is Θ(n)
- A sorting algorithm with exact average complexity may be Θ(n log n)

In practice:
- Interview problems usually focus on Big-O
- Big-Θ is more theoretical
- Big-O is what you should mostly use

---

### 5) Common complexity classes

#### O(1) — constant time
The work does not depend on input size.

Examples:
- Access array element by index
- Check if a number is even
- Compare two values

#### O(log n) — logarithmic time
Usually from dividing the problem in half.

Examples:
- Binary search
- Jumping through a sorted range
- Repeated halving

#### O(n) — linear time
One pass over the input.

Examples:
- Scan array once
- Find max in an array
- Count frequency in a single loop

#### O(n log n) — linearithmic
Very common and efficient for large data.

Examples:
- Merge sort
- Quick sort average case
- Heap sort
- Most efficient general sorting algorithms

#### O(n²) — quadratic time
Nested loops over data.

Examples:
- Checking all pairs
- Bubble sort
- Selection sort
- Insertion sort
- Brute force two-pointer nested scans

#### O(n³) — cubic time
Three nested loops.

Examples:
- Triple nested brute force
- Some matrix multiplication naive algorithms

#### O(2^n), O(n!) — exponential / factorial
Usually impossible for large n.

These appear in:
- subset generation
- permutation generation
- naive TSP-style brute force

---

### 6) How to analyze loops

#### Single loop
If a loop runs n times, complexity is usually O(n)

Example:
- for i in 0..n-1: do something
- Time: O(n)

#### Nested loops
If one loop is inside another, multiply.

Example:
- for i in 0..n-1:
    for j in 0..n-1:
        work

This is O(n²)

#### Inner loop depends on i
Example:
- for i in 0..n-1:
    for j in 0..i:
        work

This is O(n²) in total, not O(n³)

#### Loop with doubling / halving
Example:
- while n > 1:
    n = n / 2

This is O(log n)

---

### 7) Recursion complexity

Recursion introduces both:
- Time complexity
- Space complexity due to call stack

#### Example: factorial recursion
- Each call reduces n by 1
- Total calls = n + 1
- Time: O(n)
- Space: O(n) stack

#### Example: binary recursion
- Each call reduces problem size by half
- Time: O(log n)
- Space: O(log n) stack

#### Example: recursive tree
If each level branches into 2 and depth is n, then:
- Time can be O(2^n)
- Space can be O(n)

This is where exponential behavior comes from.

---

### 8) Space complexity explained clearly

Space complexity measures the extra memory used by the algorithm beyond the input.

#### O(1) space
No extra data structure grows with n.

Examples:
- swapping variables
- in-place operations
- constant counters

#### O(n) space
Extra memory proportional to input size.

Examples:
- new array of size n
- hash map storing n entries
- recursion stack of depth n

#### O(log n) space
Usually recursion dividing the problem.

#### O(n²) space
Usually 2D matrix or table.

---

### 9) Time complexity of common operations

These are the “building blocks” you must know.

#### Arrays
- Access by index: O(1)
- Search linear: O(n)
- Insert/delete in middle: O(n)
- Append at end: O(1) amortized in dynamic arrays

#### Strings
- Access character by index: O(1)
- Substring creation: O(length)
- Reversal of string: O(n)
- Checking every character: O(n)

#### Hash maps / sets
- Insert: average O(1)
- Lookup: average O(1)
- Delete: average O(1)

#### Sorting
- Merge sort: O(n log n)
- Quick sort average: O(n log n)
- Heap sort: O(n log n)
- Bubble sort: O(n²)
- Insertion sort: O(n²)

#### Searching
- Linear search: O(n)
- Binary search: O(log n)
- Hash lookup: average O(1)

---

### 10) How to reason about constraints

This is one of the most important skills.

#### Rule 1: Check the maximum n
If n ≤ 10³, then O(n²) is often okay.
If n ≤ 10⁵, O(n²) is usually impossible.
If n ≤ 10⁶, O(n log n) or O(n) is expected.

#### Rule 2: Look for the “must-have” complexity
If the problem says:
- n up to 10⁵
- you need to answer many queries
Then O(n log n) is usually the target.

If:
- n up to 10⁷
Then O(n) is preferred.

#### Rule 3: Exponential is only for very small n
If n > 25, exponential algorithms are generally not acceptable.

#### Rule 4: Use the constraint to reject bad solutions
A brute-force solution may be logically correct but still wrong for large input.

Examples:
- O(n²) for n = 10⁵ → impossible
- O(2^n) for n = 30 → impossible
- O(n log n) for n = 10⁷ → usually acceptable depending on language and constant factors

---

### 11) Typical constraint ranges and expected complexity

#### Small constraints: n ≤ 10² or 10³
Allowed:
- O(n²)
- O(n³) sometimes
- Brute force is often fine

#### Medium constraints: n ≤ 10⁵
Expected:
- O(n log n)
- O(n)
- O(n log² n) sometimes

#### Large constraints: n ≤ 10⁶ or more
Expected:
- O(n)
- O(n log n)
- avoid O(n²)

#### Very large or many repeated operations
Expected:
- O(log n)
- O(1) per query
- Preprocessing + fast lookup

---

### 12) Important concept: hidden constants

Big-O ignores constants and lower-order terms.

Example:
- 5n + 1000 = O(n)
- 2n² + 7n + 3 = O(n²)

This does not mean constants are irrelevant in real life, but for algorithm analysis they are ignored because asymptotic growth matters more.

---

### 13) Best-case vs average-case vs worst-case

#### Best case
Minimum operations possible.

Example:
- In linear search, best case is O(1) if the target is first element

#### Average case
Expected performance over all inputs

#### Worst case
Maximum operations possible

Example:
- Linear search worst case: O(n)
- Binary search worst case: O(log n)

For many DSA problems, worst-case complexity is the standard metric.

---

### 14) How to estimate complexity for a problem

Ask these questions:

1. What is the input size?
2. How many times is the main loop executed?
3. Are there nested loops?
4. Does recursion divide the problem?
5. Is there repeated scanning or repeated work?
6. Are there hash maps / sets used?
7. Is extra memory proportional to n?

Then summarize:
- Time complexity
- Space complexity
- Worst-case or average-case
- Whether it matches the constraints

---

### 15) Common mistakes beginners make

#### Mistake 1: Counting only visible loops
Sometimes the real complexity comes from repeated operations inside loops.

#### Mistake 2: Forgetting recursion stack
A recursive algorithm may have O(n) space even if time is O(log n) or O(n)

#### Mistake 3: Ignoring constraints
A solution may be “correct” but impossible for the problem size

#### Mistake 4: Confusing total work with per-iteration work
For nested loops, total time is often not just multiplication of max values but the sum over actual iterations

#### Mistake 5: Using O(n²) when the true complexity is O(n log n)

---

### 16) The standard complexity mindset for DSA

When you read a problem, always think:

- “How large can the input be?”
- “What is the likely limit?”
- “Can I pass all values in one scan?”
- “Do I need sorting?”
- “Does repeated searching cause quadratic blow-up?”
- “Can I use a structure with fast lookup?”

This is the key to choosing the right algorithm.

---

### 17) The most important rule to remember

The problem is not only about correctness. It is about correctness under constraints.

A solution is good only if:
- it works
- and its complexity fits the allowed input size

If not, it is not acceptable in competitive programming or interview settings.

---

### 18) Recommended learning order

If you want to study complexity systematically, learn in this order:

1. Growth of functions
2. Big-O notation
3. Constant, log, linear, linearithmic, quadratic
4. Nested loops
5. Recursion and stack
6. Sorting complexity
7. Hash map lookup complexity
8. Constraint-based judgment
9. Estimating complexity from problem statements

---

### 19) One-line summary

Complexity analysis is the method of measuring how an algorithm scales with input size, and the main goal is to choose a solution whose time and space usage are efficient enough for the given constraints.

If you want, I can continue this as a strict study sequence only on complexity analysis, with:
- a chapter-by-chapter breakdown
- solved examples
- common interview questions
- pattern-based complexity recognition
- constraint matching practice

All focused only on complexity analysis.




## Understanding constraints in complexity analysis

A constraint tells you the maximum possible size of the input. It is the most important clue for deciding whether an algorithm is acceptable.

The question is never just:

- “Is the algorithm correct?”

It is also:

- “Can it handle the largest possible input within time and memory limits?”

---

## 1) What constraints really mean

If a problem says:

- n ≤ 10^5

then the algorithm must work efficiently when the array or input size reaches 100,000 elements.

If it says:

- n ≤ 10^3

then a quadratic solution may still be fine.

So constraints are not arbitrary numbers. They define the complexity threshold a solution must satisfy.

---

## 2) Constraint bands and what complexity is acceptable

### A. Very small input: n ≤ 10^2 or 10^3
Typical examples:
- n ≤ 100
- n ≤ 1000

These are small enough that:
- O(n²)
- O(n³)
- even brute-force pair/triple loops may be acceptable

Why?
Because the number of operations is still manageable.

Example:
- n = 10^3
- O(n²) = 10^6 operations
- O(n³) = 10^9 operations

For 10^9 operations, depending on language and environment, it may still be borderline or too slow if repeated many times. But for just one test case, sometimes it is okay.

Example problem:
- Check all pairs in a small array
- brute-force triplets

A solution like:
- for i in range(n):
    for j in range(n):
        ...
is okay when n is around 10^3.

But even here, if there are many test cases, O(n²) may become risky.

---

### B. Medium input: n ≤ 10^5
This is the most common range in DSA problems.

Typical accepted complexities:
- O(n)
- O(n log n)

Usually not acceptable:
- O(n²)
- O(n³)
- O(2^n)

Why?
Because the numbers become huge.

Example:
- n = 10^5
- O(n²) = 10^10 operations

That is far too much.

For comparison:
- O(n log n) for n = 10^5
- about 10^5 × 17 ≈ 1.7 × 10^6 operations
- this is very manageable

Example:
- Linear scan over an array: O(n)
- Sorting with merge sort / heap sort: O(n log n)

These are the standard solutions for n up to 10^5.

Why cannot we solve with O(n²)?
Because 100,000² = 10,000,000,000 operations.

Even in optimized languages, that is too slow for most problems.

---

### C. Large input: n ≤ 2 × 10^5 or 10^6
Now the bar is even higher.

Expected solutions:
- O(n)
- O(n log n)

Avoid:
- O(n²)
- O(n² log n)
- exponential

Example:
- n = 10^6
- O(n²) = 10^12 operations

That is impossible.

Example:
- O(n log n)
- about 10^6 × 20 = 2 × 10^7
- this is usually fine

This is why problems with large constraints usually expect:
- sorting
- prefix sums
- hash maps
- two-pointer
- sliding window
- greedy / stack / queue

---

### D. Very large input: n ≤ 10^7 or more
For such constraints, the algorithm must be extremely efficient.

Typical acceptable complexities:
- O(n)
- O(n log n) in some cases with careful optimization

Not acceptable:
- O(n²)
- O(n³)
- most exponential approaches

Example:
- n = 10^7
- O(n²) = 10^14 operations

This is not realistic.

Even O(n log n) may be heavy depending on the environment, but it is still far better than quadratic.

For this range:
- a single-pass linear scan is ideal
- avoid nested loops
- avoid repeated re-scanning

---

## 3) Why some complexities are impossible for certain constraints

### Example 1: O(n²) with n = 10^5
Suppose an algorithm does:
- for i in 1..n:
    for j in 1..n:
        work

Then total work is roughly:
- n² = 10^10

This is around 10 billion iterations.

That is far beyond normal limits. Even if each operation is tiny, 10 billion is too much for most online judges and interviews.

So if the constraint is n ≤ 10^5, O(n²) is not acceptable.

---

### Example 2: O(n³) with n = 10^3
- n = 10^3
- n³ = 10^9

This may still be possible for a single test case in a fast language, but it becomes troublesome quickly.

If there are multiple test cases, or if the constant factor is high, it breaks down.

So for n around 10^3, O(n³) may be okay only in very limited cases, but it is not a scalable algorithm.

---

### Example 3: O(log n) vs O(n)
This is a perfect example of why constraints matter.

Suppose we are searching in an array of size 10^9.

- O(log n) is about log₂(10^9) ≈ 30 checks
- O(n) is up to 10^9 checks

This is why binary search is so powerful.

If the array is sorted:
- binary search works because each step reduces the search range by half
- linear search is too slow on huge inputs

So when constraints are large, logarithmic time becomes essential.

---

### Example 4: Exponential complexity
Suppose an algorithm is O(2^n).

For n = 20:
- 2²⁰ ≈ 1,048,576

This is still okay for very small inputs.

For n = 30:
- 2³⁰ ≈ 1,073,741,824

That is already over a billion operations.

For n = 40:
- 2⁴⁰ ≈ 1.1 × 10^12

This is impossible.

This is why exponential algorithms are only acceptable for very small n, often n ≤ 20 or n ≤ 25.

Typical examples:
- subset generation
- permutation generation
- brute force on all subsets / all masks

These are valid only when n is tiny.

---

## 4) Typical “allowed” complexity by constraint size

### Constraint: n ≤ 10
Accepted:
- O(2^n)
- O(n!)
- O(n³)

Why?
Because the input is tiny.

Example:
- n = 10
- 2^10 = 1024
- 10! = 3,628,800

These are still manageable.

---

### Constraint: n ≤ 50
Accepted:
- O(2^n) may still be borderline
- O(n³) may be okay
- O(n²) is fine

Why?
The problem size is still small enough that brute force can work.

Example:
- n = 50
- n² = 2500
- n³ = 125,000
- 2^50 ≈ 1.1 × 10^15

For n = 50, 2^n becomes enormous, so not all exponential solutions are acceptable even here.

This is why the exact constraint is important.

---

### Constraint: n ≤ 10^3
Accepted:
- O(n²) usually okay
- O(n³) may be okay only if few test cases

Not ideal:
- O(n⁴), O(2^n)

Example:
- n = 1000
- O(n²) = 10^6
- O(n³) = 10^9

This is okay for one case in optimized code, but not for many tests.

---

### Constraint: n ≤ 10^5
Accepted:
- O(n log n)
- O(n)

Not accepted:
- O(n²)

Why?
Quadratic blow-up is far too large.

Example:
- 10^5² = 10^10

This is the biggest dividing line for many DSA problems.

---

## 5) Why constraints are used to reject bad solutions

A problem does not just ask for a solution. It asks for a solution under a bound.

So even if an algorithm is logically correct, it may still be rejected if complexity is too high.

Example:
- Problem: find a pair with sum = target
- Naive solution: check every pair → O(n²)

If n = 10^5, that is impossible.

Correct but unacceptable:
- O(n²) is correct, but not feasible

Needed:
- O(n log n) or O(n) using sorting or hash map

This is the real reason constraints matter.

---

## 6) Constraint-based judgment: quick rules

### If n ≤ 10^3
You can often use:
- O(n²)
- O(n³) in some cases

### If n ≤ 10^5
You usually need:
- O(n log n)
- O(n)

### If n ≤ 10^6
You usually need:
- O(n)
- O(n log n)

### If n is large and repeated operations exist
You need:
- O(log n)
- O(1) average operations
- efficient preprocessing

### If n is very small (like 20 to 25)
Exponential may be accepted:
- O(2^n)
- O(n!)

---

## 7) Examples of constraint-to-complexity matching

### Example A: Find maximum value in an array
Constraint: n ≤ 10^5

Possible solution:
- scan once: O(n)

This is perfect.

Why not O(n²)?
Because it would do unnecessary repeated scans.

---

### Example B: Check whether an array contains a pair with sum target
Constraint: n ≤ 10^5

Naive solution:
- nested loops → O(n²)

Why not acceptable?
Because 10^5² is too large.

Better:
- sort and two-pointer → O(n log n)
- or hash set → O(n)

---

### Example C: Count all pairs (i, j) with i < j
Constraint: n ≤ 10^3

Possible solution:
- O(n²)

This is acceptable because:
- 10^3² = 10^6
- very manageable

---

### Example D: Generate all subsets
Constraint: n ≤ 20

Possible solution:
- O(2^n)

Why acceptable?
Because 2²⁰ ≈ 1 million, which is okay.

If n = 50, then 2^50 is unrealistic.

---

## 8) The key idea: constraints determine the allowed complexity

A constraint is not just a number. It tells you the “budget” for work.

If the budget is small, only efficient algorithms survive.

So when solving DSA problems, always ask:

- What is the maximum possible n?
- Can O(n²) handle it?
- Can O(n log n) handle it?
- Can O(n) handle it?
- Is there a faster structure required?

This is the heart of complexity analysis.

---

## 9) Final rule of thumb

Use this mental checklist:

- n ≤ 10^3 → O(n²) often okay
- n ≤ 10^5 → O(n log n) needed
- n ≤ 10^6 → O(n) or O(n log n) expected
- n small (≤ 20 or 25) → exponential may be okay
- any n large + O(n²) → usually impossible

---

If you want, I can continue with the next step and teach this as a structured chapter:

1. Big-O basics
2. Common complexity classes
3. Constraint-to-complexity mapping
4. Real DSA examples with “why this is allowed / not allowed”
5. Practice questions on complexity only

This will stay strictly focused on complexity analysis.


## Growth of functions

Growth of functions tells us how the work done by an algorithm increases as the input size increases.

We compare functions like:
- $1$
- $\log n$
- $n$
- $n \log n$
- $n^2$
- $2^n$

The important idea:
- small changes in the constant do not matter much
- the shape of the function matters more than the exact coefficient

Example:
- $3n + 5$ grows like $n$
- $100n^2 + 7n + 9$ grows like $n^2$

So we usually say:
- $3n + 5 = O(n)$
- $100n^2 + 7n + 9 = O(n^2)$

### Ordering by growth
From smallest to largest:
- $O(1)$
- $O(\log n)$
- $O(n)$
- $O(n \log n)$
- $O(n^2)$
- $O(2^n)$
- $O(n!)$

This ordering tells us how quickly the algorithm slows down as input grows.

---

## Big-O notation

Big-O gives the upper bound of an algorithm’s runtime.

If:
- $f(n) = O(g(n))$

then $f(n)$ grows no faster than $g(n)$ for large $n$.

### Example
- $f(n) = 5n + 10$
- $f(n) = O(n)$

Why?
Because:
- $5n + 10$ is dominated by $n$ when $n$ becomes large
- constants and lower-order terms are ignored

### Important rule
We ignore:
- constant multipliers
- lower-order terms

So:
- $7n^2 + 3n + 9 = O(n^2)$
- $50 \log n + 1000 = O(\log n)$
- $2n + 1 = O(n)$

### Big-O is used for:
- worst-case time complexity
- space complexity
- comparing algorithms

### Notation examples
- Accessing an array index: $O(1)$
- Binary search: $O(\log n)$
- Linear search: $O(n)$
- Merge sort: $O(n \log n)$
- Nested loops over array: $O(n^2)$

---

## Constant, log, linear, linearithmic, quadratic

These are the main complexity classes you must know.

### 1) O(1) — Constant time
The runtime does not depend on input size.

Examples:
- checking if a number is even
- accessing array element by index
- comparing two values

Example:
```text
if x % 2 == 0:
    return true
```
This is $O(1)$.

---

### 2) O(log n) — Logarithmic time
The work reduces by a constant factor each step.

Examples:
- binary search
- repeated halving
- divide-and-conquer on sorted data

Example:
```text
while low <= high:
    mid = (low + high) // 2
```
This is $O(\log n)$.

Why?
Each step reduces the search space by half.

---

### 3) O(n) — Linear time
One pass through the input.

Examples:
- scanning an array
- finding the maximum
- counting frequencies in one loop

Example:
```text
for i in range(n):
    total += arr[i]
```
This is $O(n)$.

---

### 4) O(n log n) — Linearithmic time
Very common and efficient for large inputs.

Examples:
- merge sort
- heap sort
- quicksort average case
- efficient sorting of large arrays

This is often the best general-purpose sorting complexity.

Example:
- sorting 1,000,000 elements with $O(n \log n)$ is feasible
- sorting with $O(n^2)$ is usually not

---

### 5) O(n²) — Quadratic time
Nested loops or checking all pairs.

Examples:
- bubble sort
- insertion sort
- selection sort
- brute-force pair checking

Example:
```text
for i in range(n):
    for j in range(n):
        doSomething()
```
This is $O(n^2)$.

Reason:
- outer loop runs $n$ times
- inner loop runs $n$ times
- total work is $n \times n = n^2$

---

## Nested loops

Nested loops are one of the most common sources of quadratic complexity.

### Single loop
```text
for i in range(n):
    print(i)
```
Time: $O(n)$

---

### Two nested loops
```text
for i in range(n):
    for j in range(n):
        print(i, j)
```
Time: $O(n^2)$

Why?
- outer loop has $n$ iterations
- inner loop also has $n$ iterations
- total = $n \times n$

---

### Triangular nested loop
```text
for i in range(n):
    for j in range(i):
        print(i, j)
```
This is still $O(n^2)$, not $O(n^3)$.

Why?
The total number of iterations is:
$$1 + 2 + 3 + \dots + (n-1) = \frac{n(n-1)}{2}$$
So it is proportional to $n^2$.

---

### Three nested loops
```text
for i in range(n):
    for j in range(n):
        for k in range(n):
            print(i, j, k)
```
Time: $O(n^3)$

This grows extremely fast.

---

### Key idea
If loops are nested:
- one loop → $O(n)$
- two nested loops → $O(n^2)$
- three nested loops → $O(n^3)$

The level of nesting directly affects the complexity.

---

## Recursion and stack

Recursion adds both:
- time complexity
- space complexity from the call stack

### Example: factorial
```text
def fact(n):
    if n == 0:
        return 1
    return n * fact(n - 1)
```

#### Time:
- one call for each value from $n$ down to $1$
- total calls = $n + 1$

So:
- time = $O(n)$

#### Space:
- recursion depth = $n$

So:
- space = $O(n)$

---

### Example: binary recursion
```text
def search(arr, left, right, x):
    if left > right:
        return -1
    mid = (left + right) // 2
    if arr[mid] == x:
        return mid
    if arr[mid] > x:
        return search(arr, left, mid - 1, x)
    return search(arr, mid + 1, right, x)
```

#### Time:
- each call reduces the range by half

So:
- time = $O(\log n)$

#### Space:
- recursion depth is proportional to $\log n$

So:
- space = $O(\log n)$

---

### Tree recursion
```text
def fib(n):
    if n <= 1:
        return n
    return fib(n - 1) + fib(n - 2)
```

This is not efficient.

Why?
Because the same values are recomputed many times.

Time becomes exponential:
- $O(2^n)$

Space:
- recursion stack depth = $O(n)$

This is a classic example of recursion causing exponential blow-up.

---

## Sorting complexity

Sorting is central to DSA because many problems become easy when data is arranged.

### Comparison sorting algorithms

#### Bubble sort
- time: $O(n^2)$
- space: $O(1)$

Used for understanding sorting, but not efficient for large inputs.

---

#### Insertion sort
- time: $O(n^2)$ worst-case
- space: $O(1)$

Works well for small inputs or nearly sorted arrays.

---

#### Selection sort
- time: $O(n^2)$
- space: $O(1)$

Always quadratic.

---

#### Merge sort
- time: $O(n \log n)$
- space: $O(n)$

Efficient and stable, commonly used in theoretical analysis.

---

#### Quick sort
- average time: $O(n \log n)$
- worst time: $O(n^2)$
- space: $O(\log n)$ average

Very good in practice but worst-case can degrade.

---

#### Heap sort
- time: $O(n \log n)$
- space: $O(1)$

Good when extra memory is limited.

---

### Why sorting matters in complexity
If a problem allows sorting first, it may turn a hard problem into a manageable one.

Example:
- Checking if two numbers sum to target:
  - brute force: $O(n^2)$
  - sorted + two pointers: $O(n \log n)$

This is why sorting is often a key optimization.

---

## Hash map lookup complexity

Hash maps and sets are important because they often provide near-constant-time operations.

### Average case
- insert: $O(1)$
- lookup: $O(1)$
- delete: $O(1)$

This is the standard assumption in DSA problems.

Example:
```text
hashMap.get(key)
```
Average time: $O(1)$

---

### Why is it O(1)?
Because:
- key is transformed into an index using a hash function
- direct access is possible in the table

This is true only under good hash distribution and average conditions.

---

### Worst-case behavior
In rare cases:
- many collisions
- poor hashing
- hash table degradation

Then lookup can become:
- $O(n)$

So:
- average case: $O(1)$
- worst case: $O(n)$

For most standard problems, we assume average-case complexity.

---

### Where it is useful
Hash maps are used for:
- frequency counting
- checking duplicates
- mapping values to indices
- quick existence checks

Example:
- “Is this value present in the array?”
- use a set → average $O(n)$ total

This is much faster than checking all pairs.

---

## Constraint-based judgment

Constraints tell us which complexity is acceptable.

This is the most important practical skill.

### If n ≤ 10
Then:
- $O(n^3)$, $O(2^n)$, and even $O(n!)$ may be okay

Example:
- $n = 10$
- $2^{10} = 1024$

This is tiny.

---

### If n ≤ 10^2 or 10^3
Then:
- $O(n^2)$ is usually fine
- $O(n^3)$ may be okay for a few test cases

Example:
- $n = 1000$
- $n^2 = 10^6$

This is manageable.

---

### If n ≤ 10^5
Then:
- $O(n)$ and $O(n \log n)$ are expected
- $O(n^2)$ is usually too slow

Example:
- $n = 100000$
- $n^2 = 10^{10}$

This is far too large.

---

### If n ≤ 10^6
Then:
- $O(n)$ or $O(n \log n)$ is generally required
- avoid nested loops

Example:
- $10^6 \log 10^6 \approx 2 \times 10^7$ operations
- acceptable in many languages

---

### If n is very large
Then:
- linear or logarithmic algorithms are preferred
- $O(n^2)$ is usually not feasible

---

### Example: why a brute-force solution fails
Problem:
- find whether there is a pair with sum $x$

Constraint:
- $n \le 10^5$

Brute force:
```text
for i in range(n):
    for j in range(n):
        if arr[i] + arr[j] == x:
            return true
```
This is $O(n^2)$.

But with $n = 10^5$:
- $10^{10}$ checks
- impossible.

So we need:
- hash map: $O(n)$ average
- or sorting + two pointers: $O(n \log n)$

---

## Estimating complexity from problem statements

This is a standard skill in DSA.

You should ask:

1. What is the input size?
2. Is the input array or matrix?
3. Are there nested loops?
4. Does recursion divide the problem?
5. Is sorting required?
6. Are there repeated searches or scans?
7. Is a dictionary or set possible?
8. Is it a one-pass problem or a pair-check problem?

### Problem pattern guide

#### One pass through array
Likely:
- $O(n)$

Example:
- find max
- count frequency
- sum elements

---

#### Nested loops over same array
Likely:
- $O(n^2)$

Example:
- pair sum checking
- all pair traversal
- matrix scan without optimization

---

#### Repeated halving
Likely:
- $O(\log n)$

Example:
- binary search
- divide and conquer recursive structure

---

#### Sorting then scanning
Likely:
- $O(n \log n)$

Example:
- sorted pair sum
- merge intervals
- sorting before processing

---

#### Hash map lookup
Likely:
- average $O(n)$ total

Example:
- frequency maps
- checking presence of values
- counting duplicates

---

### Example: “Given an array of n integers, find whether any value appears twice.”

If you do:
- nested loops: $O(n^2)$

If you do:
- set/hash map: $O(n)$ average

So the second approach is correct for large constraints.

---

### Example: “Find the median of a sorted array.”

If the array is sorted:
- direct access can give median in $O(1)$

If unsorted:
- sort first: $O(n \log n)$

So the final complexity depends on the data condition and the problem statement.

---

## Final summary

Complexity analysis is about understanding how much work an algorithm does as input size grows.

The main complexity classes:
- $O(1)$
- $O(\log n)$
- $O(n)$
- $O(n \log n)$
- $O(n^2)$
- $O(2^n)$

The most important skill is matching:
- algorithm complexity
- with problem constraints

If the constraint is large, an $O(n^2)$ solution usually fails. If the constraint is tiny, brute force may be completely acceptable.

This is the foundation of choosing the correct DSA approach.

---

### Quick memory rule
- small input → brute force may work
- medium input → $O(n^2)$ often becomes risky
- large input → need $O(n)$ or $O(n \log n)$
- tiny special cases → exponential may be allowed

If you want, I can continue with the next section as a practice set of 10 complexity questions with answers, all focused only on complexity analysis.