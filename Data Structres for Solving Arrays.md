# Data Structures for Array Problems

## Purpose

From a FAANG interview perspective, most array problems are not really about the array itself. They are about **what state you need to remember while scanning the array**.

This document answers the most important interview question:

> **Which data structure should I use for this array problem, and why?**

In strong interviews, you should be able to explain:

* **What** the data structure is
* **Why** it fits the problem
* **When** to use it
* **How** to use it correctly
* **Which pattern** it belongs to
* **What invariant** it maintains
* **What tradeoff** you are making in time and space

The goal is not to memorize solutions. The goal is to recognize the pattern quickly and choose the right tool.

---

# 1. Variables

## What is it?

A variable stores a single piece of state.

Examples:

```java
int max;
int min;
int sum;
int count;
int best;
```

In FAANG interviews, variables are often the simplest and most powerful tool when the problem only needs a **running answer**.

---

## Why use it?

Use variables when you only need to remember:

* the current best value
* the current running total
* the current count
* the current minimum or maximum
* a local invariant while scanning once

This is the foundation of many one-pass array problems.

---

## When to use it?

Use variables when the problem asks for:

* Largest Element
* Smallest Element
* Sum of Array
* Average
* Running Maximum
* Running Minimum
* Kadane's Algorithm
* Count Positive Numbers
* Best profit so far
* Current streak / current window state

---

## How to use it?

1. Initialize the variable correctly.
2. Scan the array once.
3. Update the variable using the current element.
4. Maintain a clear invariant.

Example: running maximum

```java
int max = Integer.MIN_VALUE;
for (int x : nums) {
    max = Math.max(max, x);
}
```

Example: Kadane's algorithm

```java
int bestEndingHere = nums[0];
int bestSoFar = nums[0];

for (int i = 1; i < nums.length; i++) {
    bestEndingHere = Math.max(nums[i], bestEndingHere + nums[i]);
    bestSoFar = Math.max(bestSoFar, bestEndingHere);
}
```

---

## Common Java snippets

```java
int sum = 0;
for (int x : nums) sum += x;
```

```java
int count = 0;
for (int x : nums) {
    if (x > 0) count++;
}
```

```java
int min = Integer.MAX_VALUE;
for (int x : nums) min = Math.min(min, x);
```

```java
double avg = (double) sum / nums.length;
```

---

## Common patterns

* One-pass scan
* Running best / running worst
* Kadane-style DP
* Counting pattern
* Greedy accumulation

---

## Recognition signals

```text
Maintain one answer
Running total
Running best
Single-pass optimization
```

---

## Complexity

Space:

```text
O(1)
```

Time:

```text
O(n)
```

---

# 2. Array

## What is it?

An array is a fixed-size contiguous block of memory with indexed access.

In interviews, arrays are often used in two ways:

1. **As the input**
2. **As a helper structure** for precomputation

---

## Why use it?

Arrays are ideal when you need:

* random access in O(1)
* compact memory usage
* indexed storage
* precomputed helper values
* fast lookup for bounded domains

Arrays are also the base structure behind many advanced techniques like prefix sums, suffix arrays, difference arrays, and dynamic programming tables.

---

## When to use it?

Use arrays when the problem involves:

* Prefix Sum Array
* Suffix Maximum Array
* Difference Array
* Frequency Array
* DP Tables
* Matrix Problems
* Indexed state storage
* Small bounded value ranges

---

## How to use it?

Use arrays as helper storage when you want to trade extra memory for faster queries or simpler logic.

Examples:

Prefix sum helper array:

```java
int[] prefix = new int[nums.length + 1];
for (int i = 0; i < nums.length; i++) {
    prefix[i + 1] = prefix[i] + nums[i];
}
```

Suffix maximum helper array:

```java
int n = nums.length;
int[] suffixMax = new int[n];
suffixMax[n - 1] = nums[n - 1];
for (int i = n - 2; i >= 0; i--) {
    suffixMax[i] = Math.max(suffixMax[i + 1], nums[i]);
}
```

Difference array for range updates:

```java
int[] diff = new int[n + 1];
diff[l] += val;
diff[r + 1] -= val;
```

---

## Common Java snippets

```java
int[] arr = new int[n];
```

```java
int[] prefix = new int[n + 1];
```

```java
int[] freq = new int[26];
```

```java
int[][] dp = new int[m][n];
```

---

## Common patterns

* Prefix sum
* Suffix precomputation
* Difference array
* Frequency counting
* Dynamic programming
* Matrix traversal
* Range update / range query preprocessing

---

## Recognition signals

```text
Need random access
Need precomputation
Need indexed storage
Need compact memory
```

---

## Complexity

Access:

```text
O(1)
```

Traversal:

```text
O(n)
```

---

# 3. Two Pointers

## What is it?

Two pointers means using two indices that move through the array with a clear invariant.

Common forms:

* **Fast/slow pointers**
* **Left/right pointers**
* **Read/write pointers**

This is one of the most important FAANG patterns for array problems.

---

## Why use it?

Two pointers often turns an O(n²) brute-force solution into O(n).

It is especially useful when you want:

* in-place modification
* pair search in sorted arrays
* partitioning
* compaction
* boundary movement
* subarray/window logic

---

## When to use it?

Use two pointers when the problem involves:

* Sorted array
* In-place
* Pair search
* Compaction
* Partition
* Reverse
* Remove duplicates
* Move zeroes
* Container With Most Water
* Fast/slow traversal

---

## How to use it?

First decide the pointer strategy:

### Same direction

One pointer reads, the other writes.

Example: remove duplicates

```java
int write = 1;
for (int read = 1; read < nums.length; read++) {
    if (nums[read] != nums[read - 1]) {
        nums[write++] = nums[read];
    }
}
```

### Opposite direction

Pointers move toward each other.

Example: reverse array

```java
int left = 0, right = nums.length - 1;
while (left < right) {
    int temp = nums[left];
    nums[left] = nums[right];
    nums[right] = temp;
    left++;
    right--;
}
```

Example: two sum in sorted array

```java
int left = 0, right = nums.length - 1;
while (left < right) {
    int sum = nums[left] + nums[right];
    if (sum == target) return new int[]{left, right};
    if (sum < target) left++;
    else right--;
}
```

---

## Common Java snippets

```java
int left = 0, right = nums.length - 1;
while (left < right) {
    // move pointers based on condition
}
```

```java
int slow = 0;
for (int fast = 0; fast < nums.length; fast++) {
    if (condition) {
        nums[slow++] = nums[fast];
    }
}
```

---

## Common patterns

* Sorted pair search
* In-place filtering
* Partitioning
* Reversal
* Sliding window expansion/contraction
* Fast/slow traversal
* Palindrome-like checks

---

## Recognition signals

```text
Sorted array
In-place
Pair search
Compaction
Partition
```

---

## Complexity

Time:

```text
O(n)
```

Space:

```text
O(1)
```

---

# 4. HashMap

## What is it?

A HashMap stores key-value pairs.

Example:

```text
Key → Value
```

In Java, `HashMap` gives average O(1) insert, lookup, and update.

---

## Why use it?

Use a HashMap when you need fast access to previously seen information.

This is one of the most common FAANG interview tools for arrays because many problems require remembering:

* counts
* indices
* prefix sums
* last seen positions
* earliest seen positions
* custom mappings

---

## When to use it?

Use HashMap for:

* Frequency Counting
* Prefix Sum problems
* Two Sum
* Grouping
* Counting
* Memoization
* Last seen index
* Earliest index
* Complement lookup

---

## How to use it?

Choose the right key and value:

* `value -> frequency`
* `prefixSum -> count`
* `prefixSum -> first index`
* `element -> last seen index`
* `element -> custom state`

Example: frequency counting

```java
Map<Integer, Integer> map = new HashMap<>();
for (int x : nums) {
    map.put(x, map.getOrDefault(x, 0) + 1);
}
```

Example: Two Sum

```java
Map<Integer, Integer> map = new HashMap<>();
for (int i = 0; i < nums.length; i++) {
    int need = target - nums[i];
    if (map.containsKey(need)) {
        return new int[]{map.get(need), i};
    }
    map.put(nums[i], i);
}
```

Example: prefix sum count

```java
Map<Integer, Integer> map = new HashMap<>();
map.put(0, 1);

int sum = 0;
int count = 0;
for (int x : nums) {
    sum += x;
    count += map.getOrDefault(sum - k, 0);
    map.put(sum, map.getOrDefault(sum, 0) + 1);
}
```

---

## Common Java snippets

```java
Map<Integer, Integer> map = new HashMap<>();
map.put(key, map.getOrDefault(key, 0) + 1);
```

```java
if (map.containsKey(key)) {
    // use stored value
}
```

```java
int value = map.getOrDefault(key, 0);
```

---

## Common patterns

* Frequency counting
* Complement search
* Prefix sum counting
* Grouping
* Memoization
* Last seen / first seen index
* Duplicate detection with counts

---

## Recognition signals

```text
Need fast lookup
Need counting
Need previous state
Need mapping
Need complement search
```

---

## Complexity

Average time:

```text
O(1)
```

Worst-case time:

```text
O(n)
```

Space:

```text
O(n)
```

---

# 5. HashSet

## What is it?

A HashSet stores unique values only.

It is the right choice when you only care about **existence**, not counts or order.

---

## Why use it?

Use a HashSet when the problem asks:

* Have we seen this before?
* Is this value already present?
* Do we need uniqueness?
* Can we detect duplicates quickly?

This is a very common pattern in array problems where you need O(1) average membership checks.

---

## When to use it?

Use HashSet for:

* Duplicate Detection
* Longest Consecutive Sequence
* Distinct Elements
* Sliding Window uniqueness
* Visited elements
* Existence checking

---

## How to use it?

Add elements as you scan.

Example: duplicate detection

```java
Set<Integer> set = new HashSet<>();
for (int x : nums) {
    if (!set.add(x)) {
        return true; // duplicate found
    }
}
return false;
```

Example: longest consecutive sequence

```java
Set<Integer> set = new HashSet<>();
for (int x : nums) set.add(x);

int best = 0;
for (int x : nums) {
    if (!set.contains(x - 1)) {
        int cur = x;
        int len = 1;
        while (set.contains(cur + 1)) {
            cur++;
            len++;
        }
        best = Math.max(best, len);
    }
}
```

---

## Common Java snippets

```java
Set<Integer> set = new HashSet<>();
set.add(x);
set.contains(x);
set.remove(x);
```

---

## Common patterns

* Duplicate detection
* Distinct count
* Visited tracking
* Sliding window uniqueness
* Consecutive sequence detection

---

## Recognition signals

```text
Unique values
Visited elements
Existence checking
Duplicate detection
```

---

## Complexity

Average time:

```text
O(1)
```

Worst-case time:

```text
O(n)
```

Space:

```text
O(n)
```

---

# 6. Queue

## What is it?

A Queue follows FIFO:

* First In
* First Out

In Java interviews, prefer `ArrayDeque` over `LinkedList` for queue operations unless the problem specifically requires otherwise.

---

## Why use it?

Use a Queue when the order of arrival matters and you need to process elements in the same order they were added.

This is common in:

* BFS
* streaming problems
* level-order processing
* window-based processing where order matters

---

## When to use it?

Use Queue for:

* First Negative Number in Window
* BFS
* Scheduling
* Level order traversal
* Ordered processing of elements

---

## How to use it?

Use `offer`, `poll`, and `peek`.

Example: basic queue

```java
Queue<Integer> q = new ArrayDeque<>();
q.offer(10);
q.offer(20);
int first = q.peek();
int removed = q.poll();
```

Example: first negative number in a window

```java
Queue<Integer> q = new ArrayDeque<>();
for (int i = 0; i < nums.length; i++) {
    if (nums[i] < 0) q.offer(i);

    while (!q.isEmpty() && q.peek() <= i - k) {
        q.poll();
    }

    if (i >= k - 1) {
        int firstNegative = q.isEmpty() ? 0 : nums[q.peek()];
    }
}
```

---

## Common Java snippets

```java
Queue<Integer> q = new ArrayDeque<>();
q.offer(x);
q.poll();
q.peek();
```

---

## Common patterns

* BFS
* Level order traversal
* First-in-first-out processing
* Window order tracking
* Streaming order problems

---

## Recognition signals

```text
Oldest element matters
Order matters
Process in arrival order
```

---

## Complexity

Time:

```text
O(1)
```

for insert/remove/peek on average.

Space:

```text
O(n)
```

---

# 7. Deque

## What is it?

A Deque is a double-ended queue.

You can insert and remove from both the front and the back.

This is one of the most important structures for sliding window problems.

---

## Why use it?

Use a Deque when you need to maintain a window and efficiently remove elements from either end.

It is especially powerful for:

* sliding window maximum/minimum
* monotonic queue
* maintaining candidates in order

---

## When to use it?

Use Deque for:

* Sliding Window Maximum
* Sliding Window Minimum
* Monotonic Queue
* Window-based optimization
* Maintaining best candidate in a moving window

---

## How to use it?

Store **indices**, not just values, when you need to know whether an element is out of the window.

Example: sliding window maximum

```java
Deque<Integer> dq = new ArrayDeque<>();
for (int i = 0; i < nums.length; i++) {
    while (!dq.isEmpty() && dq.peekFirst() <= i - k) {
        dq.pollFirst();
    }

    while (!dq.isEmpty() && nums[dq.peekLast()] <= nums[i]) {
        dq.pollLast();
    }

    dq.offerLast(i);

    if (i >= k - 1) {
        int maxInWindow = nums[dq.peekFirst()];
    }
}
```

---

## Common Java snippets

```java
Deque<Integer> dq = new ArrayDeque<>();
dq.offerLast(x);
dq.pollFirst();
dq.pollLast();
dq.peekFirst();
dq.peekLast();
```

---

## Common patterns

* Sliding window maximum/minimum
* Monotonic queue
* Best candidate maintenance
* Window optimization
* Range extreme tracking

---

## Recognition signals

```text
Need front and back operations
Maintain best candidate
Window maximum/minimum
```

---

## Complexity

Time:

```text
O(n)
```

Space:

```text
O(k)
```

for a window of size `k`.

---

# 8. Stack

## What is it?

A Stack follows LIFO:

* Last In
* First Out

In Java, prefer `Deque<Integer>` as a stack instead of `Stack`, because `Deque` is the modern interview-friendly choice.

---

## Why use it?

Use a Stack when the most recent unresolved element matters.

This is common when you need to:

* track previous elements
* find boundaries
* reverse order
* match nested structure
* solve nearest greater/smaller problems

---

## When to use it?

Use Stack for:

* Next Greater Element
* Next Smaller Element
* Stock Span
* Daily Temperatures
* Largest Rectangle in Histogram
* Boundary problems
* Undo-like behavior
* Nested matching

---

## How to use it?

Push elements as you scan. Pop when the current element resolves previous ones.

Example: basic stack

```java
Deque<Integer> stack = new ArrayDeque<>();
stack.push(10);
stack.push(20);
int top = stack.peek();
int removed = stack.pop();
```

Example: next greater element

```java
Deque<Integer> stack = new ArrayDeque<>();
for (int i = nums.length - 1; i >= 0; i--) {
    while (!stack.isEmpty() && stack.peek() <= nums[i]) {
        stack.pop();
    }
    int nextGreater = stack.isEmpty() ? -1 : stack.peek();
    stack.push(nums[i]);
}
```

---

## Common Java snippets

```java
Deque<Integer> stack = new ArrayDeque<>();
stack.push(x);
stack.pop();
stack.peek();
```

---

## Common patterns

* Next greater / next smaller
* Previous greater / previous smaller
* Stock span
* Histogram boundaries
* Daily temperatures
* Nested structure matching

---

## Recognition signals

```text
Nearest greater
Nearest smaller
Boundary
Undo
Previous unresolved element
```

---

## Complexity

Time:

```text
O(n)
```

Space:

```text
O(n)
```

---

# 9. Monotonic Stack

## What is it?

A Monotonic Stack is a stack that stays:

* increasing, or
* decreasing

This is not a separate Java class. It is a **pattern** built using a stack or `Deque`.

---

## Why use it?

Use a monotonic stack when you need to find:

* next greater element
* next smaller element
* previous greater element
* previous smaller element
* boundaries for each element

It is one of the most powerful O(n) techniques for array boundary problems.

---

## When to use it?

Use Monotonic Stack for:

* Histogram
* Daily Temperatures
* Next Greater
* Previous Smaller
* Stock Span
* Boundary discovery
* Range contribution problems

---

## How to use it?

Maintain the stack so that it always satisfies the monotonic property.

Example: increasing stack for next smaller element

```java
Deque<Integer> stack = new ArrayDeque<>();
for (int i = 0; i < nums.length; i++) {
    while (!stack.isEmpty() && nums[stack.peek()] >= nums[i]) {
        stack.pop();
    }
    int previousSmaller = stack.isEmpty() ? -1 : stack.peek();
    stack.push(i);
}
```

Example: largest rectangle in histogram

```java
Deque<Integer> stack = new ArrayDeque<>();
for (int i = 0; i <= heights.length; i++) {
    int cur = (i == heights.length) ? 0 : heights[i];
    while (!stack.isEmpty() && cur < heights[stack.peek()]) {
        int h = heights[stack.pop()];
        int left = stack.isEmpty() ? -1 : stack.peek();
        int width = i - left - 1;
        int area = h * width;
    }
    stack.push(i);
}
```

---

## Common Java snippets

```java
Deque<Integer> stack = new ArrayDeque<>();
while (!stack.isEmpty() && nums[stack.peek()] < nums[i]) {
    stack.pop();
}
stack.push(i);
```

---

## Common patterns

* Next greater/smaller
* Previous greater/smaller
* Histogram area
* Daily temperatures
* Stock span
* Contribution / boundary problems

---

## Recognition signals

```text
Boundary
Nearest
Greater
Smaller
Contribution
```

---

## Complexity

Time:

```text
O(n)
```

Space:

```text
O(n)
```

---

# 10. Priority Queue / Heap

## What is it?

A Priority Queue is a structure that always gives you the minimum or maximum element efficiently.

In Java, `PriorityQueue` is a **min-heap by default**.

---

## Why use it?

Use a Heap when you need to repeatedly extract the smallest or largest element from a changing set.

This is ideal for:

* top K problems
* streaming extremes
* merging sorted lists
* scheduling
* median maintenance

---

## When to use it?

Use Heap for:

* Top K
* Merge K Sorted Arrays
* Median Problems
* Scheduling
* Kth largest / smallest
* Dynamic best candidate selection

---

## How to use it?

Min-heap:

```java
PriorityQueue<Integer> minHeap = new PriorityQueue<>();
```

Max-heap:

```java
PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder());
```

Example: top K largest

```java
PriorityQueue<Integer> pq = new PriorityQueue<>();
for (int x : nums) {
    pq.offer(x);
    if (pq.size() > k) {
        pq.poll();
    }
}
int kthLargest = pq.peek();
```

Example: running median

```java
PriorityQueue<Integer> left = new PriorityQueue<>(Collections.reverseOrder()); // max-heap
PriorityQueue<Integer> right = new PriorityQueue<>(); // min-heap
```

---

## Common Java snippets

```java
PriorityQueue<Integer> pq = new PriorityQueue<>();
pq.offer(x);
pq.poll();
pq.peek();
```

```java
PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> a[0] - b[0]);
```

---

## Common patterns

* Top K
* Kth element
* Merge K sorted arrays/lists
* Running median
* Scheduling
* Best-first processing

---

## Recognition signals

```text
Top K
Largest
Smallest
Priority
Repeated min/max extraction
```

---

## Complexity

Insert:

```text
O(log n)
```

Remove top:

```text
O(log n)
```

Peek:

```text
O(1)
```

---

# 11. Prefix Sum Array

## What is it?

A Prefix Sum Array stores cumulative sums.

If `prefix[i]` is the sum of the first `i` elements, then any range sum can be answered quickly.

---

## Why use it?

Prefix sums are one of the most important array techniques in FAANG interviews because they convert repeated range-sum work into O(1) queries.

They are also the foundation for many subarray counting problems.

---

## When to use it?

Use Prefix Sum for:

* Range Sum Query
* Count Subarrays Sum K
* Longest Subarray Sum K
* Repeated range queries
* Subarray sum problems
* 2D range sum problems

---

## How to use it?

Build a prefix array with one extra slot so that range formulas are clean.

Example:

```java
int n = nums.length;
int[] prefix = new int[n + 1];
for (int i = 0; i < n; i++) {
    prefix[i + 1] = prefix[i] + nums[i];
}
```

Range sum from `l` to `r`:

```java
int rangeSum = prefix[r + 1] - prefix[l];
```

Example: count subarrays with sum `k`

```java
Map<Integer, Integer> map = new HashMap<>();
map.put(0, 1);

int sum = 0;
int count = 0;
for (int x : nums) {
    sum += x;
    count += map.getOrDefault(sum - k, 0);
    map.put(sum, map.getOrDefault(sum, 0) + 1);
}
```

Example: longest subarray with sum `k`

```java
Map<Integer, Integer> firstIndex = new HashMap<>();
firstIndex.put(0, -1);

int sum = 0;
int best = 0;
for (int i = 0; i < nums.length; i++) {
    sum += nums[i];
    if (!firstIndex.containsKey(sum)) {
        firstIndex.put(sum, i);
    }
    if (firstIndex.containsKey(sum - k)) {
        best = Math.max(best, i - firstIndex.get(sum - k));
    }
}
```

---

## Common Java snippets

```java
int[] prefix = new int[n + 1];
prefix[i + 1] = prefix[i] + nums[i];
```

```java
int rangeSum = prefix[r + 1] - prefix[l];
```

---

## Common patterns

* Range sum query
* Subarray sum equals K
* Longest subarray with sum K
* Counting subarrays
* 2D prefix sum
* Difference between two positions

---

## Recognition signals

```text
Subarray sum
Range sum
Repeated queries
Need fast interval sum
```

---

## Complexity

Build:

```text
O(n)
```

Query:

```text
O(1)
```

Space:

```text
O(n)
```

---

## Important FAANG note

If the array is **mutable** and you need many updates plus many range queries, prefix sum alone is not enough.

In that case, consider:

* Fenwick Tree (Binary Indexed Tree)
* Segment Tree

That is a strong follow-up point in interviews.

---

# 12. Frequency Array

## What is it?

A Frequency Array is an array used as a counting table instead of a HashMap.

Example:

```java
int[] freq = new int[26];
```

---

## Why use it?

Use a frequency array when the value range is small and bounded.

Compared to HashMap, it is:

* faster
* simpler
* more memory-efficient for small domains

---

## When to use it?

Use Frequency Array for:

* Characters
* Digits
* Small value ranges
* ASCII / lowercase letters
* Counting sort style problems
* Anagram checks
* Small bounded integer frequencies

---

## How to use it?

Map each value to an index.

Example: lowercase letters

```java
int[] freq = new int[26];
for (char c : s.toCharArray()) {
    freq[c - 'a']++;
}
```

Example: digits

```java
int[] freq = new int[10];
for (int x : nums) {
    freq[x]++;
}
```

Example: compare two strings

```java
int[] freq = new int[26];
for (char c : s.toCharArray()) freq[c - 'a']++;
for (char c : t.toCharArray()) freq[c - 'a']--;
```

---

## Common Java snippets

```java
int[] freq = new int[26];
freq[c - 'a']++;
```

```java
int[] freq = new int[128]; // ASCII
```

---

## Common patterns

* Character counting
* Anagram checking
* Counting sort
* Small-range frequency tracking
* Fixed-domain frequency problems

---

## Recognition signals

```text
Small bounded values
ASCII
Lowercase letters
Digits
Fixed domain
```

---

## Complexity

Time:

```text
O(n)
```

Space:

```text
O(1)
```

for fixed-size domains.

---

# 13. Matrix

## What is it?

A Matrix is a 2D array.

In array problems, matrices usually represent:

* grids
* boards
* image-like data
* 2D DP tables

---

## Why use it?

Use a matrix when the problem naturally has rows and columns.

Matrices are common in FAANG interviews because they combine:

* indexing
* traversal
* boundary checks
* BFS/DFS
* dynamic programming
* in-place transformation

---

## When to use it?

Use Matrix for:

* Grid BFS
* Grid DFS
* DP
* Prefix Sum 2D
* Rotation
* Spiral Traversal
* Flood fill
* Island problems
* Path problems

---

## How to use it?

Use row/column loops, direction arrays, and boundary checks.

Example: direction array

```java
int[][] dirs = {{1,0}, {-1,0}, {0,1}, {0,-1}};
```

Example: visited matrix

```java
boolean[][] visited = new boolean[m][n];
```

Example: 2D prefix sum

```java
int[][] prefix = new int[m + 1][n + 1];
for (int i = 0; i < m; i++) {
    for (int j = 0; j < n; j++) {
        prefix[i + 1][j + 1] = prefix[i + 1][j] + prefix[i][j + 1]
                             - prefix[i][j] + grid[i][j];
    }
}
```

---

## Common Java snippets

```java
int[][] grid = new int[m][n];
```

```java
for (int i = 0; i < m; i++) {
    for (int j = 0; j < n; j++) {
        // process grid[i][j]
    }
}
```

```java
int[][] dirs = {{1,0}, {-1,0}, {0,1}, {0,-1}};
```

---

## Common patterns

* Grid traversal
* BFS / DFS on grid
* 2D DP
* Spiral traversal
* Rotation
* Flood fill
* 2D prefix sum

---

## Recognition signals

```text
Grid
Rows
Columns
Neighbors
Boundary checks
```

---

## Complexity

Depends on the traversal, but commonly:

```text
O(m * n)
```

Space depends on visited / DP / helper arrays.

---

# 14. Recursion Stack

## What is it?

The recursion stack is the implicit stack created by function calls.

You do not write it explicitly, but it behaves like a stack.

---

## Why use it?

Use recursion when the problem is naturally defined by smaller subproblems or branching choices.

This is common in:

* DFS
* tree traversal
* backtracking
* divide and conquer
* recursive exploration of arrays and grids

---

## When to use it?

Use recursion stack for:

* DFS
* Tree Traversal
* Backtracking
* Recursive search
* Permutations
* Subsets
* Recursive grid exploration

---

## How to use it?

Define:

1. a base case
2. a recursive step
3. a backtracking step if needed

Example: recursive DFS on a grid

```java
void dfs(int r, int c, int[][] grid, boolean[][] visited) {
    if (r < 0 || c < 0 || r >= grid.length || c >= grid[0].length) return;
    if (visited[r][c]) return;

    visited[r][c] = true;

    dfs(r + 1, c, grid, visited);
    dfs(r - 1, c, grid, visited);
    dfs(r, c + 1, grid, visited);
    dfs(r, c - 1, grid, visited);
}
```

Example: backtracking

```java
void backtrack(int index, int[] nums, List<Integer> path) {
    if (index == nums.length) {
        // process path
        return;
    }

    path.add(nums[index]);
    backtrack(index + 1, nums, path);
    path.remove(path.size() - 1);

    backtrack(index + 1, nums, path);
}
```

---

## Common Java snippets

```java
void dfs(...) {
    if (baseCase) return;
    dfs(...);
}
```

---

## Common patterns

* DFS
* Backtracking
* Recursive exploration
* Divide and conquer
* Tree / grid traversal

---

## Recognition signals

```text
Recursive structure
Choices
Decision tree
Subproblem decomposition
```

---

## Complexity

Time depends on the branching factor and recursion tree.

Space:

```text
O(depth)
```

for the recursion stack.

---

## Important FAANG note

Java recursion depth can overflow on large inputs.

If the recursion depth may be large, consider:

* iterative DFS with an explicit stack
* BFS with a queue
* tail-recursive alternatives where possible

---

# Decision Guide

## Question

Need one running answer?

Use

```text
Variables
```

---

Need previous values quickly?

Use

```text
HashMap
```

---

Need uniqueness or visited tracking?

Use

```text
HashSet
```

---

Need ordered removal or FIFO processing?

Use

```text
Queue
```

---

Need nearest greater/smaller or boundaries?

Use

```text
Stack
```

---

Need maximum/minimum while a window moves?

Use

```text
Deque
```

---

Need top K or repeated min/max extraction?

Use

```text
Heap
```

---

Need cumulative sums or range sum queries?

Use

```text
Prefix Sum Array
```

---

Need compact array in-place?

Use

```text
Two Pointers
```

---

Need many indexed values or bounded counts?

Use

```text
Array
```

---

Need small-domain counting?

Use

```text
Frequency Array
```

---

Need grid or 2D traversal?

Use

```text
Matrix
```

---

Need recursive exploration?

Use

```text
Recursion Stack
```

---

# Quick Recognition Table

| Problem Signal        | Data Structure            |
| --------------------- | ------------------------- |
| Running best          | Variables                 |
| Sorted pair search    | Two Pointers              |
| Frequency             | HashMap / Frequency Array |
| Distinct values       | HashSet                   |
| Range Sum             | Prefix Sum                |
| Range Update          | Difference Array          |
| Window Maximum        | Deque                     |
| First Negative        | Queue                     |
| Next Greater          | Stack                     |
| Boundary              | Monotonic Stack           |
| Top K                 | Heap                      |
| Grid                  | Matrix                    |
| Recursive exploration | Recursion Stack           |

---

# Important FAANG Add-On

A strong interview answer is not just “use X.” It is:

1. **Why X fits the constraint**
2. **What invariant X maintains**
3. **What complexity you get**
4. **Why other choices are worse**

A few high-value interview reminders:

* If the array is **sorted**, think about **Two Pointers** or **Binary Search**
* If you need **counts or previous state**, think **HashMap**
* If you need **existence only**, think **HashSet**
* If you need **window extremes**, think **Deque / Monotonic Queue**
* If you need **nearest greater/smaller**, think **Monotonic Stack**
* If you need **top K**, think **Heap**
* If you need **range sums**, think **Prefix Sum**
* If you need **range updates**, think **Difference Array**
* If you need **many updates + many queries**, think **Fenwick Tree / Segment Tree**
* If you need **grid traversal**, think **Matrix + BFS/DFS**
* If you need **recursive branching**, think **Recursion Stack**

Also remember:

* Use `long` when sums can overflow `int`
* In Java, prefer `ArrayDeque` over `Stack` and often over `LinkedList`
* Store **indices** instead of values when you need window boundaries or distances
* Always state the **invariant** out loud in interviews

---

# Final Interview Mindset

Before writing code, ask:

```text
What information do I need to remember?

Which data structure remembers exactly that information efficiently?

What invariant will I maintain while scanning the array?
```

Choose the data structure first.

The algorithm usually follows naturally.
