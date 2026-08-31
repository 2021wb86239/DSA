# Data Structures by DSA Pattern

## Purpose

From a FAANG interview perspective, data structures should not be learned as isolated tools. They should be learned through the **DSA patterns in which they are commonly used**.

The same data structure can solve very different problems depending on the pattern:

* A `HashMap` can support frequency counting, prefix-sum counting, or last-seen-index tracking.
* A `Deque` can act as a queue, stack, or monotonic queue.
* An array can represent input data, prefix sums, dynamic programming states, or a difference array.
* A stack can support ordinary LIFO processing or a monotonic-stack boundary algorithm.

This document explains each major pattern using the same framework:

* **What is it?**
* **Why use it?**
* **When to use it?**
* **How to use it?**
* **Common Java snippets**
* **Common pattern variations**
* **Recognition signals**
* **Invariant**
* **Complexity**
* **Tradeoffs**

The goal is not to memorize solutions. The goal is to recognize the required state and choose the simplest data structure that maintains it efficiently.

---

# 1. One-Pass Scan and Running State

## What is it?

A one-pass scan processes the input from left to right while maintaining a small amount of state.

The state may be:

* a running sum
* a current minimum or maximum
* a count
* the best answer so far
* the current streak
* the best profit or score

The main data structures are usually:

```text
Variables
Arrays
```

---

## Why use it?

Use this pattern when the answer can be built incrementally without remembering all previous elements.

It often gives:

```text
O(n) time
O(1) extra space
```

This is usually the first solution to consider because it is simple, fast, and cache-friendly.

---

## When to use it?

Use a one-pass scan for:

* Largest Element
* Smallest Element
* Array Sum
* Running Maximum
* Running Minimum
* Maximum Profit
* Maximum Subarray
* Counting values
* Longest current streak
* Greedy accumulation

---

## How to use it?

Define the state before coding.

Example:

```text
bestEndingHere = best answer ending at the current index
bestSoFar = best answer seen anywhere so far
```

Example: maximum subarray

```java
int bestEndingHere = nums[0];
int bestSoFar = nums[0];

for (int i = 1; i < nums.length; i++) {
    bestEndingHere = Math.max(nums[i], bestEndingHere + nums[i]);
    bestSoFar = Math.max(bestSoFar, bestEndingHere);
}
```

The key decision is whether the current element should:

* extend the previous state, or
* start a new state

---

## Common Java snippets

```java
int max = Integer.MIN_VALUE;

for (int x : nums) {
    max = Math.max(max, x);
}
```

```java
long sum = 0;

for (int x : nums) {
    sum += x;
}
```

```java
int count = 0;
for (int x : nums) {
    if (x > 0) count++;
}
```

```java
int streak = 0;
int best = 0;

for (int x : nums) {
    if (x == 1) {
        streak++;
        best = Math.max(best, streak);
    } else {
        streak = 0;
    }
}
```

---

## Common patterns

* Running best / worst
* Kadane's algorithm
* Greedy scan
* Counting
* State compression
* Local-to-global optimization

---

## Recognition signals

```text
One pass
Running answer
Best so far
Current streak
Maximum/minimum
No need to revisit old elements
```

---

## Invariant

At every index, the maintained variables correctly describe the required state for the portion of the input processed so far.

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

unless helper storage is used.

---

## Tradeoffs

Advantages:

* Minimal memory
* Usually optimal time
* Simple implementation

Limitations:

* Cannot answer arbitrary historical queries
* Cannot recover detailed information unless it is explicitly stored
* Does not work when future decisions require many previous values

---

# 2. Two Pointers

## What is it?

Two pointers uses two indices to process an array or string while maintaining a relationship between them.

Common forms include:

```text
Left / right
Fast / slow
Read / write
```

The pointers may move:

* in the same direction
* toward each other
* at different speeds

---

## Why use it?

Two pointers often reduces a brute-force O(n²) solution to O(n).

It is especially useful when:

* the input is sorted
* the operation is in-place
* elements can be discarded permanently
* the answer depends on a left and right boundary
* a pair or interval is being examined

---

## When to use it?

Use two pointers for:

* Two Sum in a sorted array
* Three Sum after sorting
* Remove Duplicates
* Move Zeroes
* Partitioning
* Reverse Array
* Valid Palindrome
* Container With Most Water
* Fast/slow linked-list traversal
* In-place filtering

---

## How to use it?

First identify the pointer roles.

### Opposite-direction pointers

Use when the answer depends on both ends.

```java
int left = 0;
int right = nums.length - 1;

while (left < right) {
    int sum = nums[left] + nums[right];

    if (sum == target) {
        return new int[]{left, right};
    } else if (sum < target) {
        left++;
    } else {
        right--;
    }
}
```

This works because the array is sorted. Moving `left` increases the sum, and moving `right` decreases it.

### Read/write pointers

Use when compacting or modifying an array in place.

```java
int write = 0;

for (int read = 0; read < nums.length; read++) {
    if (nums[read] != 0) {
        nums[write++] = nums[read];
    }
}

while (write < nums.length) {
    nums[write++] = 0;
}
```

### Fast/slow pointers

Use when one pointer explores and another tracks a valid position.

```java
int slow = 0;

for (int fast = 0; fast < nums.length; fast++) {
    if (nums[fast] != 0) {
        nums[slow++] = nums[fast];
    }
}
```

---

## Common Java snippets

```java
int left = 0;
int right = nums.length - 1;

while (left < right) {
    // process nums[left] and nums[right]
}
```

```java
int slow = 0;

for (int fast = 0; fast < nums.length; fast++) {
    if (condition(nums[fast])) {
        nums[slow++] = nums[fast];
    }
}
```

```java
while (left < right && nums[left] == nums[right]) {
    left++;
    right--;
}
```

---

## Common patterns

* Sorted pair search
* In-place compaction
* Partitioning
* Reversal
* Palindrome checking
* Fast/slow traversal
* Boundary shrinking
* Three Sum

---

## Recognition signals

```text
Sorted array
In-place
Pair
Two ends
Remove duplicates
Move zeroes
Partition
Read/write
```

---

## Invariant

The pointer positions divide the input into regions whose meaning remains correct throughout the scan.

For example:

```text
[0 ... write - 1] contains all valid elements
[write ... read - 1] is already processed
[read ... end] is unprocessed
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

excluding sorting or output storage.

---

## Tradeoffs

Advantages:

* Very low memory
* Often linear time
* Excellent for in-place problems

Limitations:

* Usually requires sorted data or a strong movement invariant
* Pointer movement must be justified carefully
* A wrong movement rule can skip valid answers

---

# 3. Sliding Window

## What is it?

A sliding window maintains a contiguous range:

```text
[left ... right]
```

The right pointer expands the window, and the left pointer contracts it when the window becomes invalid or no longer optimal.

The window may be:

* fixed-size
* variable-size
* based on a sum
* based on distinct values
* based on character counts
* based on a constraint

---

## Why use it?

Sliding window avoids recomputing every subarray or substring from scratch.

Instead of checking all O(n²) ranges, it updates the current window incrementally.

Typical complexity:

```text
O(n)
```

---

## When to use it?

Use sliding window for:

* Longest Substring Without Repeating Characters
* Minimum Window Substring
* Longest Subarray With At Most K Distinct Values
* Maximum Sum Subarray of Size K
* Minimum Size Subarray Sum
* Permutation in String
* Anagram windows
* Fixed-size window statistics

---

## How to use it?

### Fixed-size window

The window always has size `k`.

```java
long windowSum = 0;
long best = Long.MIN_VALUE;

for (int right = 0; right < nums.length; right++) {
    windowSum += nums[right];

    if (right >= k) {
        windowSum -= nums[right - k];
    }

    if (right >= k - 1) {
        best = Math.max(best, windowSum);
    }
}
```

### Variable-size window

Expand with `right`, then shrink with `left` while invalid.

```java
int left = 0;
int best = 0;
Map<Integer, Integer> freq = new HashMap<>();

for (int right = 0; right < nums.length; right++) {
    freq.put(nums[right], freq.getOrDefault(nums[right], 0) + 1);

    while (freq.size() > k) {
        int value = nums[left++];
        freq.put(value, freq.get(value) - 1);

        if (freq.get(value) == 0) {
            freq.remove(value);
        }
    }

    best = Math.max(best, right - left + 1);
}
```

---

## Common Java snippets

```java
int left = 0;

for (int right = 0; right < nums.length; right++) {
    add(nums[right]);

    while (windowIsInvalid()) {
        remove(nums[left]);
        left++;
    }

    updateAnswer(left, right);
}
```

```java
Map<Character, Integer> count = new HashMap<>();

for (int right = 0; right < s.length(); right++) {
    char c = s.charAt(right);
    count.put(c, count.getOrDefault(c, 0) + 1);

    while (count.get(c) > 1) {
        char leftChar = s.charAt(left++);
        count.put(leftChar, count.get(leftChar) - 1);
    }
}
```

---

## Common patterns

* Fixed-size window
* Variable-size window
* At most K
* Exactly K using subtraction
* Longest valid window
* Shortest valid window
* Frequency-based window
* Window sum
* Window distinctness

---

## Recognition signals

```text
Contiguous subarray
Contiguous substring
Longest
Shortest
At most K
Exactly K
Window of size K
Current range
```

---

## Invariant

After the shrinking phase, the current window satisfies the problem's validity condition.

For example:

```text
The window contains at most K distinct values.
```

or:

```text
The window contains no duplicate characters.
```

---

## Complexity

Time:

```text
O(n)
```

because each element enters and leaves the window at most once.

Space:

```text
O(k)
```

or:

```text
O(alphabet size)
```

depending on the state being stored.

---

## Tradeoffs

Advantages:

* Converts many subarray problems to O(n)
* Maintains only the current range
* Works well with HashMap, HashSet, or frequency arrays

Limitations:

* Usually requires a monotonic validity condition
* Standard shrinking logic may fail when negative numbers destroy monotonicity
* Must distinguish “at most,” “at least,” and “exactly”

---

# 4. Prefix Sum and Difference Array

## What is it?

Prefix sum stores cumulative information from the beginning of the array.

For an array:

```text
[2, 4, 1, 3]
```

the prefix sums may be:

```text
[0, 2, 6, 7, 10]
```

A difference array stores changes between adjacent positions and is useful for efficient range updates.

---

## Why use it?

Prefix sums make range queries fast.

Difference arrays make range updates fast.

They are opposite forms of preprocessing:

```text
Prefix Sum:
many queries, few updates

Difference Array:
many updates, final reconstruction
```

---

## When to use it?

Use prefix sums for:

* Range Sum Query
* Subarray Sum Equals K
* Longest Subarray With Sum K
* Repeated interval sums
* 2D range sums

Use difference arrays for:

* Range increment operations
* Booking or scheduling updates
* Flight seat reservations
* Interval additions
* Applying many updates before reading the final array

---

## How to use it?

### Prefix sum

```java
int[] prefix = new int[nums.length + 1];

for (int i = 0; i < nums.length; i++) {
    prefix[i + 1] = prefix[i] + nums[i];
}
```

Range sum from `left` to `right`:

```java
int sum = prefix[right + 1] - prefix[left];
```

### Prefix sum with HashMap

For subarray sum counting:

```java
Map<Integer, Integer> countByPrefix = new HashMap<>();
countByPrefix.put(0, 1);

int prefix = 0;
int answer = 0;

for (int x : nums) {
    prefix += x;

    answer += countByPrefix.getOrDefault(prefix - k, 0);

    countByPrefix.put(
        prefix,
        countByPrefix.getOrDefault(prefix, 0) + 1
    );
}
```

### Difference array

To add `value` to every index from `left` through `right`:

```java
int[] diff = new int[n + 1];

diff[left] += value;
diff[right + 1] -= value;
```

Reconstruct the final values:

```java
int running = 0;

for (int i = 0; i < n; i++) {
    running += diff[i];
    result[i] = running;
}
```

---

## Common Java snippets

```java
int[] prefix = new int[n + 1];

for (int i = 0; i < n; i++) {
    prefix[i + 1] = prefix[i] + nums[i];
}
```

```java
int rangeSum = prefix[right + 1] - prefix[left];
```

```java
int[] diff = new int[n + 1];
diff[left] += value;
diff[right + 1] -= value;
```

---

## Common patterns

* Range sum
* Subarray sum
* Prefix sum plus HashMap
* Difference array
* Range updates
* 2D prefix sum
* Prefix balance

---

## Recognition signals

```text
Range sum
Subarray sum
Repeated interval queries
Many range updates
Cumulative balance
```

---

## Invariant

For prefix sums:

```text
prefix[i] equals the sum of elements before index i.
```

For difference arrays:

```text
The running sum of diff represents the total updates affecting the current index.
```

---

## Complexity

Prefix sum:

```text
Build: O(n)
Query: O(1)
Space: O(n)
```

Difference array:

```text
Each update: O(1)
Reconstruction: O(n)
Space: O(n)
```

---

## Tradeoffs

Advantages:

* Extremely fast range queries or updates
* Simple formulas
* Useful with HashMap for subarray problems

Limitations:

* Prefix sums do not handle arbitrary updates efficiently
* Difference arrays require a final reconstruction
* Integer overflow is common; use `long` when necessary

---

# 5. Hashing and Frequency Counting

## What is it?

Hashing stores information so that values can be found quickly.

The main structures are:

```text
HashMap<K, V>
HashSet<T>
Frequency Array
```

The correct choice depends on what must be remembered.

---

## Why use it?

Hashing is useful when the problem requires fast access to previous information.

Typical stored state includes:

```text
value → count
value → index
prefix sum → count
prefix sum → first index
value → custom state
```

---

## When to use it?

Use hashing for:

* Two Sum
* Frequency Counting
* Duplicate Detection
* Grouping
* Prefix Sum problems
* Longest Consecutive Sequence
* Last Seen Index
* First Seen Index
* Anagram problems
* Memoization

---

## How to use it?

### Frequency map

```java
Map<Integer, Integer> frequency = new HashMap<>();

for (int x : nums) {
    frequency.put(x, frequency.getOrDefault(x, 0) + 1);
}
```

### Complement lookup

```java
Map<Integer, Integer> indexByValue = new HashMap<>();

for (int i = 0; i < nums.length; i++) {
    int need = target - nums[i];

    if (indexByValue.containsKey(need)) {
        return new int[]{indexByValue.get(need), i};
    }

    indexByValue.put(nums[i], i);
}
```

### Set membership

```java
Set<Integer> seen = new HashSet<>();

for (int x : nums) {
    if (!seen.add(x)) {
        return true;
    }
}
return false;
```

### Frequency array

```java
int[] frequency = new int[26];

for (char c : s.toCharArray()) {
    frequency[c - 'a']++;
}
```

---

## Common Java snippets

```java
Map<Integer, Integer> map = new HashMap<>();
map.put(key, map.getOrDefault(key, 0) + 1);
```

```java
Set<Integer> set = new HashSet<>();
set.add(value);
set.contains(value);
set.remove(value);
```

```java
int count = map.getOrDefault(key, 0);
```

---

## Common patterns

* Frequency counting
* Complement search
* Duplicate detection
* Prefix sum plus HashMap
* Last seen index
* First seen index
* Grouping by key
* Memoization

---

## Recognition signals

```text
Have I seen this before?
How many times?
Where was it last seen?
What value belongs to this key?
Find the complement
Group equal properties
```

---

## Invariant

The hash structure contains exactly the information needed from the portion of the input already processed.

For example:

```text
indexByValue contains every previously seen value and its index.
```

---

## Complexity

Average:

```text
Insert: O(1)
Lookup: O(1)
Delete: O(1)
```

Space:

```text
O(n)
```

A frequency array with a fixed domain uses:

```text
O(1)
```

extra space relative to input size.

---

## Tradeoffs

Advantages:

* Fast average lookup
* Flexible state representation
* Excellent for previous-state problems

Limitations:

* Does not maintain sorted order
* Uses extra memory
* Hashing has worst-case degradation
* Must handle collisions conceptually
* HashMap iteration order should not be assumed

---

# 6. Stack and Monotonic Stack

## What is it?

A stack follows LIFO:

```text
Last In, First Out
```

A monotonic stack is a stack whose values or indices remain sorted in increasing or decreasing order.

The Java implementation is usually:

```java
Deque<Integer> stack = new ArrayDeque<>();
```

---

## Why use it?

Use a normal stack when the most recent unresolved item matters.

Use a monotonic stack when you need to find relationships between an element and its nearest greater or smaller neighbor.

It can reduce many nested-loop boundary problems from O(n²) to O(n).

---

## When to use it?

Use a stack for:

* Parentheses
* Expression evaluation
* Undo behavior
* DFS
* Reversal
* Nested structures

Use a monotonic stack for:

* Next Greater Element
* Next Smaller Element
* Previous Greater Element
* Previous Smaller Element
* Daily Temperatures
* Stock Span
* Largest Rectangle in Histogram
* Sum of Subarray Minimums
* Sum of Subarray Ranges

---

## How to use it?

### Basic stack

```java
Deque<Integer> stack = new ArrayDeque<>();

stack.push(10);
stack.push(20);

int top = stack.peek();
int removed = stack.pop();
```

### Next greater element

Scan from right to left.

```java
int[] answer = new int[nums.length];
Deque<Integer> stack = new ArrayDeque<>();

for (int i = nums.length - 1; i >= 0; i--) {
    while (!stack.isEmpty() && stack.peek() <= nums[i]) {
        stack.pop();
    }

    answer[i] = stack.isEmpty() ? -1 : stack.peek();
    stack.push(nums[i]);
}
```

### Index-based monotonic stack

Store indices when you need distances or boundaries.

```java
Deque<Integer> stack = new ArrayDeque<>();

for (int i = 0; i < nums.length; i++) {
    while (!stack.isEmpty() && nums[stack.peek()] >= nums[i]) {
        stack.pop();
    }

    int previousSmallerIndex = stack.isEmpty() ? -1 : stack.peek();
    stack.push(i);
}
```

### Histogram boundaries

```java
Deque<Integer> stack = new ArrayDeque<>();
int bestArea = 0;

for (int i = 0; i <= heights.length; i++) {
    int currentHeight = i == heights.length ? 0 : heights[i];

    while (!stack.isEmpty() && currentHeight < heights[stack.peek()]) {
        int height = heights[stack.pop()];
        int leftBoundary = stack.isEmpty() ? -1 : stack.peek();
        int width = i - leftBoundary - 1;

        bestArea = Math.max(bestArea, height * width);
    }

    stack.push(i);
}
```

---

## Common Java snippets

```java
Deque<Integer> stack = new ArrayDeque<>();

stack.push(value);
stack.peek();
stack.pop();
```

```java
while (!stack.isEmpty() && nums[stack.peek()] <= nums[i]) {
    stack.pop();
}
stack.push(i);
```

---

## Common patterns

* Next greater
* Next smaller
* Previous greater
* Previous smaller
* Boundary discovery
* Histogram
* Stock span
* Parentheses matching
* Expression evaluation

---

## Recognition signals

```text
Nearest
Next greater
Next smaller
Previous greater
Previous smaller
Boundary
Unresolved elements
When does this element become resolved?
```

---

## Invariant

The stack contains unresolved candidates in monotonic order.

When a new element violates the order, the popped elements have found their answer or boundary.

---

## Complexity

Time:

```text
O(n)
```

Each element is pushed and popped at most once.

Space:

```text
O(n)
```

---

## Tradeoffs

Advantages:

* Converts many O(n²) problems to O(n)
* Excellent for nearest-boundary problems
* Can calculate distances and contributions efficiently

Limitations:

* Equality handling is subtle
* You must choose increasing versus decreasing order correctly
* Storing values is insufficient when distances or boundaries are required; store indices instead

---

# 7. Queue, Deque, and Monotonic Queue

## What is it?

A queue follows FIFO:

```text
First In, First Out
```

A deque supports operations at both ends.

A monotonic queue is a deque maintained in increasing or decreasing order so that the best candidate is always at the front.

---

## Why use it?

Use a queue when processing order matters.

Use a deque when elements may expire from the front and weaker candidates should be removed from the back.

This is the standard approach for sliding-window minimum and maximum problems.

---

## When to use it?

Use a queue for:

* BFS
* Level-order traversal
* First negative in a window
* Streaming order
* Scheduling

Use a deque or monotonic queue for:

* Sliding Window Maximum
* Sliding Window Minimum
* Window optimization
* Maximum/minimum over every window
* Shortest path variants with special edge weights

---

## How to use it?

### Basic queue

```java
Queue<Integer> queue = new ArrayDeque<>();

queue.offer(10);
queue.offer(20);

int first = queue.peek();
int removed = queue.poll();
```

### Sliding-window maximum

Store indices in decreasing order of values.

```java
Deque<Integer> deque = new ArrayDeque<>();

for (int right = 0; right < nums.length; right++) {
    while (!deque.isEmpty() && deque.peekFirst() <= right - k) {
        deque.pollFirst();
    }

    while (!deque.isEmpty() && nums[deque.peekLast()] <= nums[right]) {
        deque.pollLast();
    }

    deque.offerLast(right);

    if (right >= k - 1) {
        int maximum = nums[deque.peekFirst()];
    }
}
```

The front always contains the index of the maximum value in the current window.

---

## Common Java snippets

```java
Queue<Integer> queue = new ArrayDeque<>();
queue.offer(value);
queue.peek();
queue.poll();
```

```java
Deque<Integer> deque = new ArrayDeque<>();
deque.offerLast(index);
deque.pollFirst();
deque.pollLast();
deque.peekFirst();
deque.peekLast();
```

---

## Common patterns

* BFS
* Level-order traversal
* First-in-first-out processing
* Sliding-window maximum
* Sliding-window minimum
* Monotonic queue
* Expiring candidates

---

## Recognition signals

```text
First in, first out
Level by level
Sliding-window maximum
Sliding-window minimum
Candidate expires
Need front and back operations
```

---

## Invariant

For a monotonic maximum queue:

```text
Indices are increasing from front to back.
Values are decreasing from front to back.
The front is the maximum candidate.
```

---

## Complexity

Basic queue operations:

```text
O(1)
```

Monotonic queue over an array:

```text
O(n)
```

Space:

```text
O(k)
```

for a window of size `k`.

---

## Tradeoffs

Advantages:

* Linear-time sliding-window extremes
* Efficient expiration of old elements
* Avoids recomputing each window

Limitations:

* Usually stores indices, not values
* Equality rules must be chosen carefully
* More complex than a normal queue

---

# 8. Heap and Priority Queue

## What is it?

A heap is a tree-based structure that keeps the smallest or largest element accessible at the top.

Java's `PriorityQueue` is a min-heap by default.

```java
PriorityQueue<Integer> minHeap = new PriorityQueue<>();
```

A max-heap can be created with:

```java
PriorityQueue<Integer> maxHeap =
    new PriorityQueue<>(Collections.reverseOrder());
```

---

## Why use it?

Use a heap when you repeatedly need the smallest or largest element from a changing collection.

A heap is especially useful when you do not need the entire collection sorted.

---

## When to use it?

Use a heap for:

* Top K Largest
* Top K Smallest
* Kth Largest
* Kth Smallest
* Merge K Sorted Lists
* Merge K Sorted Arrays
* Running Median
* Scheduling
* Repeatedly selecting the best candidate
* Dijkstra's algorithm

---

## How to use it?

### Top K largest

Maintain a min-heap of size `k`.

```java
PriorityQueue<Integer> minHeap = new PriorityQueue<>();

for (int x : nums) {
    minHeap.offer(x);

    if (minHeap.size() > k) {
        minHeap.poll();
    }
}

int kthLargest = minHeap.peek();
```

The heap contains the largest `k` values, and the smallest among them is at the top.

### Custom objects

```java
PriorityQueue<int[]> pq =
    new PriorityQueue<>((a, b) -> Integer.compare(a[0], b[0]));
```

### Running median

Use two heaps:

```java
PriorityQueue<Integer> lower =
    new PriorityQueue<>(Collections.reverseOrder());

PriorityQueue<Integer> upper =
    new PriorityQueue<>();
```

The lower half is a max-heap, and the upper half is a min-heap.

---

## Common Java snippets

```java
PriorityQueue<Integer> minHeap = new PriorityQueue<>();
minHeap.offer(value);
minHeap.peek();
minHeap.poll();
```

```java
PriorityQueue<Integer> maxHeap =
    new PriorityQueue<>(Collections.reverseOrder());
```

```java
PriorityQueue<int[]> pq =
    new PriorityQueue<>((a, b) -> Integer.compare(a[0], b[0]));
```

---

## Common patterns

* Top K
* Kth element
* Merge K sorted sources
* Running median
* Best-first search
* Scheduling
* Dynamic minimum/maximum

---

## Recognition signals

```text
Top K
Kth largest
Kth smallest
Repeated minimum
Repeated maximum
Priority
Best next candidate
```

---

## Invariant

For a top-K-largest min-heap:

```text
The heap contains the largest K elements seen so far.
```

For a running median:

```text
All values in the lower heap are less than or equal to all values in the upper heap.
```

---

## Complexity

For a heap of size `h`:

```text
Insert: O(log h)
Remove top: O(log h)
Peek: O(1)
```

Top K with heap size `k`:

```text
Time: O(n log k)
Space: O(k)
```

---

## Tradeoffs

Advantages:

* Avoids sorting the entire input
* Excellent for streaming data
* Supports dynamic best-candidate selection

Limitations:

* Does not provide fast arbitrary lookup
* Does not maintain full sorted order
* Heap operations are slower than HashMap lookup
* Comparator overflow must be avoided

Prefer:

```java
Integer.compare(a, b)
```

over:

```java
a - b
```

when values may be large.

---

# 9. Binary Search

## What is it?

Binary search repeatedly eliminates half of the search space.

It is commonly implemented on:

* sorted arrays
* monotonic answer spaces
* rotated sorted arrays
* index ranges
* feasible/infeasible decision spaces

---

## Why use it?

Binary search reduces a linear search to logarithmic time.

It is also a powerful optimization technique when the answer can be tested with a monotonic predicate.

---

## When to use it?

Use binary search for:

* Search in Sorted Array
* First or Last Occurrence
* Lower Bound / Upper Bound
* Search in Rotated Sorted Array
* Minimum Eating Speed
* Capacity to Ship Packages
* Kth Smallest by Answer Search
* Any monotonic feasibility problem

---

## How to use it?

### Standard search

```java
int left = 0;
int right = nums.length - 1;

while (left <= right) {
    int mid = left + (right - left) / 2;

    if (nums[mid] == target) {
        return mid;
    } else if (nums[mid] < target) {
        left = mid + 1;
    } else {
        right = mid - 1;
    }
}

return -1;
```

### Lower bound

Find the first index where `nums[index] >= target`.

```java
int left = 0;
int right = nums.length;

while (left < right) {
    int mid = left + (right - left) / 2;

    if (nums[mid] < target) {
        left = mid + 1;
    } else {
        right = mid;
    }
}

int firstAtLeast = left;
```

### Binary search on answer

```java
int left = minimumPossible;
int right = maximumPossible;

while (left < right) {
    int mid = left + (right - left) / 2;

    if (canFinish(mid)) {
        right = mid;
    } else {
        left = mid + 1;
    }
}

return left;
```

---

## Common Java snippets

```java
int mid = left + (right - left) / 2;
```

```java
while (left < right) {
    int mid = left + (right - left) / 2;
}
```

---

## Common patterns

* Exact search
* Lower bound
* Upper bound
* First true
* Last true
* Rotated array search
* Binary search on answer

---

## Recognition signals

```text
Sorted
First occurrence
Last occurrence
Minimum possible maximum
Maximum possible minimum
Can we do it with X?
Feasibility is monotonic
```

---

## Invariant

The answer remains inside the current search interval.

For answer search:

```text
All values below left are impossible.
All values at or above right are possible.
```

---

## Complexity

Time:

```text
O(log n)
```

or:

```text
O(log R)
```

for an answer range of size `R`.

Space:

```text
O(1)
```

---

## Tradeoffs

Advantages:

* Very fast
* Constant extra space
* Works on huge answer ranges

Limitations:

* Requires sorted data or a monotonic predicate
* Boundary errors are common
* The feasibility function must be correct and monotonic

---

# 10. Sorting and Ordered Structures

## What is it?

Sorting transforms data into an ordered form so that other patterns become possible.

Ordered structures maintain sorted order dynamically.

Common Java structures include:

```text
Arrays.sort
TreeSet
TreeMap
```

---

## Why use it?

Sorting can expose relationships that are hidden in arbitrary input.

After sorting, you can often use:

* two pointers
* greedy selection
* binary search
* interval merging
* duplicate grouping

Use `TreeSet` or `TreeMap` when values change dynamically but sorted access is still required.

---

## When to use it?

Use sorting for:

* Two Sum or Three Sum
* Merge Intervals
* Meeting Rooms
* Grouping duplicates
* Greedy scheduling
* Coordinate compression
* Binary search preparation

Use ordered structures for:

* Floor and ceiling
* Next greater dynamic value
* Previous smaller dynamic value
* Sorted insertion and deletion
* Dynamic interval boundaries

---

## How to use it?

### Sort an array

```java
Arrays.sort(nums);
```

### Sort objects

```java
Arrays.sort(intervals, (a, b) -> Integer.compare(a[0], b[0]));
```

### TreeSet

```java
TreeSet<Integer> set = new TreeSet<>();

set.add(10);
set.add(20);

Integer floor = set.floor(15);
Integer ceiling = set.ceiling(15);
Integer higher = set.higher(10);
Integer lower = set.lower(20);
```

### TreeMap

```java
TreeMap<Integer, Integer> map = new TreeMap<>();

map.put(10, 1);
map.put(20, 2);

Integer key = map.floorKey(15);
```

---

## Common Java snippets

```java
Arrays.sort(nums);
```

```java
TreeSet<Integer> set = new TreeSet<>();
```

```java
TreeMap<Integer, Integer> map = new TreeMap<>();
```

---

## Common patterns

* Sort then two pointers
* Sort then greedy
* Interval merging
* Coordinate compression
* Dynamic predecessor/successor
* Ordered frequency map

---

## Recognition signals

```text
Sorted order helps
Merge intervals
Next greater dynamic value
Floor
Ceiling
Predecessor
Successor
```

---

## Invariant

The data remains ordered after every insertion or deletion.

---

## Complexity

Sorting:

```text
O(n log n)
```

TreeSet / TreeMap operations:

```text
O(log n)
```

Space:

```text
O(n)
```

depending on the structure.

---

## Tradeoffs

Advantages:

* Enables binary search and two pointers
* Maintains sorted dynamic state
* Supports floor and ceiling operations

Limitations:

* Sorting destroys original order unless indices are preserved
* Usually slower than hashing for pure membership checks
* Ordered structures use more overhead than arrays

---

# 11. Dynamic Programming Tables and Memoization

## What is it?

Dynamic Programming stores answers to previously solved states.

The storage may be:

```text
Array
2D array
HashMap
```

The key idea is:

```text
state → best answer for that state
```

---

## Why use it?

Use DP when:

* subproblems overlap
* the problem has optimal substructure
* recomputing the same state would be expensive

Memoization stores results top-down.

Tabulation builds results bottom-up.

---

## When to use it?

Use DP for:

* House Robber
* Coin Change
* Longest Increasing Subsequence
* Knapsack
* Grid Paths
* Edit Distance
* Partition problems
* Subset Sum
* Interval DP

---

## How to use it?

Define the state precisely.

Example: House Robber

```java
int prevTwo = 0;
int prevOne = 0;

for (int money : nums) {
    int current = Math.max(prevOne, prevTwo + money);
    prevTwo = prevOne;
    prevOne = current;
}

return prevOne;
```

This is space-optimized DP.

Example: memoization with an array:

```java
int[] memo = new int[n];
Arrays.fill(memo, -1);

int solve(int index) {
    if (index >= n) return 0;
    if (memo[index] != -1) return memo[index];

    int skip = solve(index + 1);
    int take = nums[index] + solve(index + 2);

    return memo[index] = Math.max(skip, take);
}
```

Example: 2D DP:

```java
int[][] dp = new int[m + 1][n + 1];

for (int i = 1; i <= m; i++) {
    for (int j = 1; j <= n; j++) {
        // compute dp[i][j]
    }
}
```

---

## Common Java snippets

```java
int[] dp = new int[n + 1];
```

```java
int[][] dp = new int[m + 1][n + 1];
```

```java
Map<State, Integer> memo = new HashMap<>();
```

---

## Common patterns

* One-dimensional DP
* Two-dimensional DP
* Knapsack
* Grid DP
* Interval DP
* Memoized recursion
* State compression
* Rolling-array optimization

---

## Recognition signals

```text
Choose or skip
Minimum cost
Maximum profit
Number of ways
Repeated states
Overlapping subproblems
```

---

## Invariant

Each DP entry represents the correct answer for one precisely defined state.

---

## Complexity

Depends on the number of states and transitions.

Typical:

```text
Time: O(number of states × transitions per state)
Space: O(number of states)
```

Space can sometimes be reduced to:

```text
O(1)
```

or:

```text
O(n)
```

with rolling-state optimization.

---

## Tradeoffs

Advantages:

* Avoids repeated computation
* Handles optimization and counting problems
* Can be optimized through state compression

Limitations:

* State definition can be difficult
* Memory usage may be large
* Incorrect transitions produce plausible but wrong answers

---

# 12. Recursion, Backtracking, and Explicit Stack

## What is it?

Recursion uses the call stack to explore a decision tree.

Backtracking explores a choice, recursively continues, then undoes the choice.

An explicit `Deque` can replace recursion when depth may be large.

---

## Why use it?

Use recursion or backtracking when the problem naturally branches into choices.

Typical examples:

* subsets
* permutations
* combinations
* word search
* maze exploration
* tree traversal
* DFS

---

## When to use it?

Use recursion/backtracking for:

* Generate all subsets
* Generate permutations
* Combination Sum
* N-Queens
* Word Search
* DFS
* Tree traversal
* Constraint satisfaction

---

## How to use it?

A backtracking function usually contains:

1. a base case
2. a choice
3. a recursive call
4. an undo operation

Example: subsets

```java
void backtrack(
    int index,
    int[] nums,
    List<Integer> path,
    List<List<Integer>> result
) {
    if (index == nums.length) {
        result.add(new ArrayList<>(path));
        return;
    }

    path.add(nums[index]);
    backtrack(index + 1, nums, path, result);
    path.remove(path.size() - 1);

    backtrack(index + 1, nums, path, result);
}
```

Example: iterative DFS

```java
Deque<Integer> stack = new ArrayDeque<>();
Set<Integer> visited = new HashSet<>();

stack.push(start);

while (!stack.isEmpty()) {
    int node = stack.pop();

    if (!visited.add(node)) continue;

    for (int next : graph[node]) {
        stack.push(next);
    }
}
```

---

## Common Java snippets

```java
void backtrack(...) {
    if (baseCase) return;

    makeChoice();
    backtrack(...);
    undoChoice();

    backtrack(...);
}
```

```java
Deque<Integer> stack = new ArrayDeque<>();
stack.push(start);
```

---

## Common patterns

* DFS
* Subsets
* Permutations
* Combinations
* Constraint search
* Tree traversal
* Grid exploration

---

## Recognition signals

```text
All possible choices
Generate every arrangement
Choose or skip
Explore and undo
Recursive structure
Depth-first exploration
```

---

## Invariant

The current path represents a valid partial solution, and every recursive call extends that path consistently.

---

## Complexity

Depends on the branching factor and depth.

Common examples:

```text
Subsets: O(2^n)
Permutations: O(n!)
```

Space:

```text
O(depth)
```

excluding the output.

---

## Tradeoffs

Advantages:

* Natural representation of branching problems
* Concise DFS implementation
* Easy to express recursive state

Limitations:

* Can cause `StackOverflowError`
* May repeat states without memoization
* Output size itself may be exponential

---

# 13. Graph Representation and Traversal

## What is it?

A graph represents relationships between entities.

The main representations are:

```text
Adjacency List
Adjacency Matrix
Edge List
```

For most interview problems, an adjacency list is the default.

---

## Why use it?

Use graphs when the problem describes:

* connections
* dependencies
* routes
* relationships
* transitions
* reachable states

Graphs may be:

* directed or undirected
* weighted or unweighted
* cyclic or acyclic
* connected or disconnected

---

## When to use it?

Use graph structures for:

* Course Schedule
* Number of Islands
* Clone Graph
* Network Connectivity
* Shortest Path
* Word Ladder
* Dependency Resolution
* Connected Components

---

## How to use it?

### Adjacency list

```java
List<List<Integer>> graph = new ArrayList<>();

for (int i = 0; i < n; i++) {
    graph.add(new ArrayList<>());
}

graph.get(from).add(to);
```

### BFS

```java
Queue<Integer> queue = new ArrayDeque<>();
boolean[] visited = new boolean[n];

queue.offer(start);
visited[start] = true;

while (!queue.isEmpty()) {
    int node = queue.poll();

    for (int next : graph.get(node)) {
        if (!visited[next]) {
            visited[next] = true;
            queue.offer(next);
        }
    }
}
```

### DFS

```java
void dfs(
    int node,
    List<List<Integer>> graph,
    boolean[] visited
) {
    if (visited[node]) return;

    visited[node] = true;

    for (int next : graph.get(node)) {
        dfs(next, graph, visited);
    }
}
```

---

## Common Java snippets

```java
List<List<Integer>> graph = new ArrayList<>();
```

```java
int[][] edges;
```

```java
boolean[] visited = new boolean[n];
```

```java
int[][] directions = {
    {1, 0},
    {-1, 0},
    {0, 1},
    {0, -1}
};
```

---

## Common patterns

* BFS
* DFS
* Topological sort
* Connected components
* Cycle detection
* Shortest path
* Grid graph traversal
* Union Find

---

## Recognition signals

```text
Connected
Reachable
Dependency
Prerequisite
Route
Neighbor
Cycle
Network
```

---

## Invariant

Every visited node has already been processed or scheduled for processing, and no node is processed more than once when using a visited structure.

---

## Complexity

Adjacency list traversal:

```text
O(V + E)
```

Adjacency matrix traversal:

```text
O(V²)
```

Space:

```text
O(V + E)
```

for an adjacency list.

---

## Tradeoffs

### Adjacency list

Advantages:

* Efficient for sparse graphs
* Uses O(V + E) space
* Fast neighbor traversal

Limitations:

* Checking whether a specific edge exists may take O(degree)

### Adjacency matrix

Advantages:

* O(1) edge lookup
* Simple for dense graphs

Limitations:

* O(V²) memory
* Expensive neighbor traversal for sparse graphs

---

# 14. Union Find / Disjoint Set Union

## What is it?

Union Find maintains a collection of disjoint groups.

It supports:

```text
find(x)
union(a, b)
```

`find` identifies the representative of a group.

`union` merges two groups.

---

## Why use it?

Use Union Find when connectivity changes over time and you need to know whether two elements belong to the same component.

With path compression and union by size or rank, operations are almost constant time.

---

## When to use it?

Use DSU for:

* Number of Connected Components
* Dynamic Connectivity
* Cycle Detection in Undirected Graphs
* Kruskal's Minimum Spanning Tree
* Redundant Connection
* Group merging

---

## How to use it?

```java
class UnionFind {
    private final int[] parent;
    private final int[] size;

    UnionFind(int n) {
        parent = new int[n];
        size = new int[n];

        for (int i = 0; i < n; i++) {
            parent[i] = i;
            size[i] = 1;
        }
    }

    int find(int x) {
        if (parent[x] != x) {
            parent[x] = find(parent[x]);
        }
        return parent[x];
    }

    boolean union(int a, int b) {
        int rootA = find(a);
        int rootB = find(b);

        if (rootA == rootB) {
            return false;
        }

        if (size[rootA] < size[rootB]) {
            int temp = rootA;
            rootA = rootB;
            rootB = temp;
        }

        parent[rootB] = rootA;
        size[rootA] += size[rootB];

        return true;
    }
}
```

---

## Common Java snippets

```java
int root = find(x);
```

```java
if (find(a) == find(b)) {
    // already connected
}
```

```java
union(a, b);
```

---

## Common patterns

* Connectivity
* Component counting
* Cycle detection
* Group merging
* Minimum spanning tree

---

## Recognition signals

```text
Are these connected?
Merge groups
Same component
Dynamic connectivity
Cycle in an undirected graph
```

---

## Invariant

Each element belongs to exactly one component, and every component has a representative root.

---

## Complexity

With path compression and union by size/rank:

```text
Amortized time: O(α(n))
```

where `α(n)` is effectively constant for practical input sizes.

Space:

```text
O(n)
```

---

## Tradeoffs

Advantages:

* Extremely efficient for dynamic connectivity
* Simpler than repeated graph searches for component merging

Limitations:

* Does not naturally provide shortest paths
* Does not preserve full graph structure
* Standard DSU is mainly for undirected connectivity

---

# 15. Tree and Trie Structures

## What is it?

A tree represents hierarchical relationships.

A binary tree allows at most two children per node.

A binary search tree maintains an ordering rule.

A Trie stores strings by shared prefixes.

---

## Why use it?

Use trees when the data is hierarchical.

Use a Trie when the problem is about prefixes rather than complete-key equality.

---

## When to use it?

Use trees for:

* Hierarchical data
* Binary tree traversal
* Search trees
* Range structures
* Recursive decomposition

Use Tries for:

* Prefix search
* Autocomplete
* Dictionary matching
* Word Search
* Starts-with queries

---

## How to use it?

### Binary tree node

```java
class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;

    TreeNode(int val) {
        this.val = val;
    }
}
```

### Inorder traversal

```java
void inorder(TreeNode node) {
    if (node == null) return;

    inorder(node.left);
    System.out.println(node.val);
    inorder(node.right);
}
```

### Trie node

```java
class TrieNode {
    TrieNode[] children = new TrieNode[26];
    boolean isWord;
}
```

### Trie insertion

```java
void insert(TrieNode root, String word) {
    TrieNode current = root;

    for (char c : word.toCharArray()) {
        int index = c - 'a';

        if (current.children[index] == null) {
            current.children[index] = new TrieNode();
        }

        current = current.children[index];
    }

    current.isWord = true;
}
```

---

## Common Java snippets

```java
Deque<TreeNode> queue = new ArrayDeque<>();
```

```java
TrieNode[] children = new TrieNode[26];
```

```java
TreeSet<Integer> sorted = new TreeSet<>();
```

---

## Common patterns

* Preorder traversal
* Inorder traversal
* Postorder traversal
* Level-order traversal
* Binary search tree
* Trie prefix search
* Tree recursion
* Tree BFS

---

## Recognition signals

```text
Hierarchy
Parent and child
Root
Subtree
Prefix
Starts with
Autocomplete
```

---

## Invariant

For a BST:

```text
All values in the left subtree satisfy the ordering rule relative to the node.
All values in the right subtree satisfy the ordering rule.
```

For a Trie:

```text
Each path from the root represents a prefix.
```

---

## Complexity

Binary tree traversal:

```text
O(n)
```

Trie operation for word length `L`:

```text
O(L)
```

Balanced BST operations:

```text
O(log n)
```

Unbalanced BST operations:

```text
O(n)
```

---

## Tradeoffs

Advantages:

* Natural representation of hierarchy
* Efficient prefix operations with Trie
* Ordered search with balanced trees

Limitations:

* Pointer overhead
* Recursive depth can be large
* Trie memory usage can be high
* A plain BST can become unbalanced

---

# 16. Range Query Structures

## What is it?

Range-query structures support queries over intervals while also allowing updates.

The main structures are:

```text
Fenwick Tree
Segment Tree
Sparse Table
```

---

## Why use it?

Prefix sums are excellent for static range sums, but they become inefficient when values change.

Use a range-query structure when you need:

```text
many range queries
+
many updates
```

---

## When to use it?

Use a Fenwick Tree for:

* Dynamic prefix sums
* Dynamic range sums
* Frequency prefix queries
* Inversion counting

Use a Segment Tree for:

* Range minimum
* Range maximum
* Range sum
* Complex merge operations
* Lazy range updates

Use a Sparse Table for:

* Static range minimum
* Static range maximum
* Static GCD queries

---

## How to use it?

### Fenwick Tree

```java
class FenwickTree {
    private final int[] tree;

    FenwickTree(int n) {
        tree = new int[n + 1];
    }

    void add(int index, int delta) {
        index++;

        while (index < tree.length) {
            tree[index] += delta;
            index += index & -index;
        }
    }

    int prefixSum(int index) {
        index++;
        int sum = 0;

        while (index > 0) {
            sum += tree[index];
            index -= index & -index;
        }

        return sum;
    }

    int rangeSum(int left, int right) {
        if (left == 0) {
            return prefixSum(right);
        }

        return prefixSum(right) - prefixSum(left - 1);
    }
}
```

### Segment Tree concept

```java
class SegmentTree {
    private final int[] tree;
    private final int n;

    SegmentTree(int[] nums) {
        n = nums.length;
        tree = new int[4 * n];
        build(1, 0, n - 1, nums);
    }

    void build(int node, int left, int right, int[] nums) {
        if (left == right) {
            tree[node] = nums[left];
            return;
        }

        int mid = left + (right - left) / 2;
        build(node * 2, left, mid, nums);
        build(node * 2 + 1, mid + 1, right, nums);

        tree[node] = tree[node * 2] + tree[node * 2 + 1];
    }
}
```

---

## Common Java snippets

```java
int[] tree = new int[4 * n];
```

```java
index += index & -index;
```

```java
index -= index & -index;
```

---

## Common patterns

* Dynamic range sum
* Range minimum
* Range maximum
* Inversion counting
* Coordinate compression plus Fenwick Tree
* Lazy propagation

---

## Recognition signals

```text
Many range queries
Many updates
Range minimum
Range maximum
Dynamic prefix sum
```

---

## Invariant

Each tree node stores the correct aggregate information for its represented interval.

---

## Complexity

Fenwick Tree:

```text
Build: O(n) or O(n log n)
Update: O(log n)
Query: O(log n)
Space: O(n)
```

Segment Tree:

```text
Build: O(n)
Update: O(log n)
Query: O(log n)
Space: O(n)
```

Sparse Table:

```text
Preprocessing: O(n log n)
Query: O(1) for supported operations
Update: Not efficient
```

---

## Tradeoffs

Advantages:

* Supports dynamic range operations
* Much faster than recomputing ranges
* Fenwick Tree is compact and relatively simple

Limitations:

* More complex than prefix sums
* Segment Trees require careful interval logic
* Sparse Tables are unsuitable for frequent updates

---

# 17. Matrix and Grid Patterns

## What is it?

A matrix is a two-dimensional array.

A grid can also be viewed as an implicit graph where each cell is a node and neighboring cells are edges.

---

## Why use it?

Matrices support:

* row and column indexing
* local neighbor traversal
* dynamic programming
* BFS and DFS
* in-place transformations
* 2D prefix sums

---

## When to use it?

Use matrix/grid structures for:

* Number of Islands
* Flood Fill
* Rotting Oranges
* Word Search
* Spiral Matrix
* Rotate Image
* Grid DP
* Shortest Path in a Grid
* 2D range sums

---

## How to use it?

### Direction vectors

```java
int[][] directions = {
    {1, 0},
    {-1, 0},
    {0, 1},
    {0, -1}
};
```

### Grid BFS

```java
Queue<int[]> queue = new ArrayDeque<>();
boolean[][] visited = new boolean[m][n];

queue.offer(new int[]{startRow, startCol});
visited[startRow][startCol] = true;

while (!queue.isEmpty()) {
    int[] cell = queue.poll();
    int row = cell[0];
    int col = cell[1];

    for (int[] direction : directions) {
        int nextRow = row + direction[0];
        int nextCol = col + direction[1];

        if (nextRow < 0 || nextRow >= m ||
            nextCol < 0 || nextCol >= n) {
            continue;
        }

        if (!visited[nextRow][nextCol]) {
            visited[nextRow][nextCol] = true;
            queue.offer(new int[]{nextRow, nextCol});
        }
    }
}
```

### In-place rotation

```java
for (int i = 0; i < n; i++) {
    for (int j = i; j < n; j++) {
        int temp = matrix[i][j];
        matrix[i][j] = matrix[j][i];
        matrix[j][i] = temp;
    }
}

for (int[] row : matrix) {
    reverse(row);
}
```

---

## Common Java snippets

```java
int[][] grid = new int[m][n];
```

```java
boolean[][] visited = new boolean[m][n];
```

```java
int rows = grid.length;
int cols = grid[0].length;
```

---

## Common patterns

* Grid BFS
* Grid DFS
* Flood fill
* Island counting
* Multi-source BFS
* 2D DP
* Spiral traversal
* Matrix rotation
* 2D prefix sum

---

## Recognition signals

```text
Grid
Board
Rows and columns
Neighbors
Up/down/left/right
Diagonal
Island
Cell
```

---

## Invariant

Every processed cell has been handled according to the traversal rule, and visited cells are not processed repeatedly.

---

## Complexity

For an `m × n` grid:

```text
Time: O(mn)
```

Space:

```text
O(mn)
```

when using a visited matrix or queue in the worst case.

---

## Tradeoffs

Advantages:

* Direct representation of spatial relationships
* Works naturally with BFS, DFS, and DP
* Supports in-place transformations

Limitations:

* Boundary errors are common
* Recursive DFS may overflow
* A separate visited matrix may double memory usage

---

# 18. Choosing the Data Structure by Pattern

## Need one running answer?

Use:

```text
Variables
```

---

## Need a pair or interval with sorted data?

Use:

```text
Two Pointers
```

---

## Need a contiguous range with a validity condition?

Use:

```text
Sliding Window
```

---

## Need repeated range sums?

Use:

```text
Prefix Sum
```

---

## Need many range updates before reconstruction?

Use:

```text
Difference Array
```

---

## Need fast previous-value lookup?

Use:

```text
HashMap
```

---

## Need uniqueness or membership only?

Use:

```text
HashSet
```

---

## Need nearest greater or smaller?

Use:

```text
Monotonic Stack
```

---

## Need minimum or maximum in every moving window?

Use:

```text
Monotonic Deque
```

---

## Need top K or repeated best-element extraction?

Use:

```text
Heap
```

---

## Need sorted dynamic values?

Use:

```text
TreeSet
TreeMap
```

---

## Need logarithmic search?

Use:

```text
Binary Search
```

---

## Need repeated overlapping subproblem results?

Use:

```text
DP Array
Memoization Map
```

---

## Need recursive branching?

Use:

```text
Recursion
Backtracking
Explicit Stack
```

---

## Need connectivity?

Use:

```text
Graph
Union Find
```

---

## Need prefix matching?

Use:

```text
Trie
```

---

## Need dynamic range queries and updates?

Use:

```text
Fenwick Tree
Segment Tree
```

---

# 19. Pattern Recognition Table

| Problem signal           | Pattern             | Typical data structure    |
| ------------------------ | ------------------- | ------------------------- |
| Running best             | One-pass scan       | Variables                 |
| Sorted pair              | Two pointers        | Array indices             |
| In-place filtering       | Two pointers        | Array                     |
| Longest valid subarray   | Sliding window      | HashMap / HashSet         |
| Fixed-size range         | Sliding window      | Variables / Deque         |
| Range sum                | Prefix sum          | Array                     |
| Subarray sum equals K    | Prefix sum counting | HashMap                   |
| Many range updates       | Difference array    | Array                     |
| Frequency                | Hashing             | HashMap / frequency array |
| Duplicate detection      | Membership          | HashSet                   |
| Next greater             | Monotonic stack     | Deque                     |
| Previous smaller         | Monotonic stack     | Deque                     |
| Window maximum           | Monotonic queue     | Deque                     |
| Top K                    | Heap                | PriorityQueue             |
| First occurrence         | Binary search       | Sorted array              |
| Dynamic sorted neighbor  | Ordered structure   | TreeSet / TreeMap         |
| Repeated states          | Dynamic programming | Array / HashMap           |
| All combinations         | Backtracking        | Recursion stack           |
| Reachability             | Graph traversal     | Queue / stack             |
| Dynamic connectivity     | DSU                 | Parent array              |
| Prefix matching          | Trie                | Tree nodes                |
| Range query plus updates | Range tree          | Fenwick / Segment Tree    |
| Grid neighbors           | Matrix traversal    | Queue / stack             |

---

# 20. Interview Explanation Template

When choosing a data structure, explain it in this order:

```text
The problem requires remembering ______.

The operation that must be fast is ______.

I will use ______ because it supports that operation in ______ time.

The invariant is ______.

The total time complexity is ______.

The extra space complexity is ______.

A different structure would be worse because ______.
```

Example:

```text
I need to know whether a value has appeared before, but I do not need its count or index. I will use a HashSet because average membership lookup is O(1). The invariant is that the set contains every value seen so far. The total time is O(n), and the extra space is O(n). A HashMap would store unnecessary information.
```

---

# 21. Important Java Rules

## Use `long` for large sums

```java
long sum = 0;
```

Do not assume that an `int` is safe for cumulative sums, products, or large ranges.

---

## Prefer `ArrayDeque`

Use:

```java
Deque<Integer> stack = new ArrayDeque<>();
Queue<Integer> queue = new ArrayDeque<>();
```

Avoid using the legacy `Stack` class unless required.

---

## Store indices when boundaries matter

For sliding windows, monotonic stacks, and distance calculations, store indices:

```java
Deque<Integer> deque = new ArrayDeque<>();
deque.offerLast(index);
```

Values alone cannot tell you whether an element has expired or how far away it is.

---

## Avoid comparator subtraction

Prefer:

```java
(a, b) -> Integer.compare(a[0], b[0])
```

instead of:

```java
(a, b) -> a[0] - b[0]
```

because subtraction can overflow.

---

## Be precise with equality

These two conditions are not always equivalent:

```java
nums[stack.peek()] <= nums[i]
```

and:

```java
nums[stack.peek()] < nums[i]
```

Equality determines which duplicate element remains and can change the answer in:

* monotonic stacks
* sliding-window deques
* interval boundaries
* contribution problems

---

# Final Mental Model

Before writing code, ask:

```text
What information must survive while I process the input?

Is the problem about:
- a running state?
- two boundaries?
- a contiguous window?
- cumulative information?
- previous values?
- uniqueness?
- nearest boundaries?
- window extremes?
- top K?
- sorted order?
- repeated states?
- connectivity?
- hierarchy?
- range updates?
```

Then choose the data structure that maintains exactly that information.

The most important principle is:

> **Choose the data structure based on the operation that must be fast, then state the invariant that explains why the algorithm works.**

A strong FAANG solution is not merely:

```text
Use a HashMap.
```

It is:

```text
Use a HashMap because I need average O(1) lookup of previously seen prefix sums. The map stores the required historical state, and the invariant is that every prefix sum seen so far is represented with the correct count or earliest index.
```

That is the level of reasoning expected in strong interviews.
