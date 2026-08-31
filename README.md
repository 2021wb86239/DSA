# 12-Week FAANG DSA Roadmap

This roadmap is organized so that each week builds on the concepts from the previous week. The goal is not only to learn individual data structures and algorithms, but also to understand how they connect and when to combine them.

Each week includes:

* Core concepts
* Connection to the previous week
* Main patterns
* Practice focus
* LeetCode problems by pattern
* Suggested outcome

---

# Week 1: Arrays, Strings, and Complexity Foundations

## Builds On

This is the starting point for the entire roadmap. Arrays provide the foundation for indexing, traversal, searching, sorting, prefix techniques, dynamic programming, and graph representations.

## Topics

### Complexity Foundations

* Big-O notation
* Time complexity
* Space complexity
* Best, average, and worst case
* In-place algorithms
* Input constraints and complexity selection

### Arrays

* Array fundamentals
* Traversal and indexing
* In-place modification
* Subarrays and subsequences
* Array rotation
* Matrix / 2D arrays
* Basic greedy array problems

### Strings

* String basics
* String traversal
* Character arrays
* Palindrome basics
* Anagram basics

## Patterns

* Single-pass traversal
* Counting
* In-place updates
* Reverse traversal
* Matrix traversal
* Basic two-pointer thinking

## Practice Focus

* Find maximum/minimum
* Reverse an array
* Rotate an array
* Move zeroes
* Remove duplicates
* Valid palindrome
* Valid anagram
* Matrix traversal
* Spiral matrix

## LeetCode Problems by Pattern

### Array Traversal

* 1. Two Sum
* 121. Best Time to Buy and Sell Stock
* 136. Single Number
* 217. Contains Duplicate
* 268. Missing Number

### In-Place Modification

* 26. Remove Duplicates from Sorted Array
* 27. Remove Element
* 283. Move Zeroes
* 189. Rotate Array
* 75. Sort Colors

### Strings and Character Counting

* 125. Valid Palindrome
* 242. Valid Anagram
* 387. First Unique Character in a String
* 409. Longest Palindrome
* 205. Isomorphic Strings

### Matrix Traversal

* 54. Spiral Matrix
* 48. Rotate Image
* 73. Set Matrix Zeroes
* 289. Game of Life
* 498. Diagonal Traverse

## Outcome

You should be comfortable processing arrays and strings in O(n), O(n²), and O(1) extra space when appropriate.

---

# Week 2: Two Pointers, Sliding Window, and Prefix Sum

## Builds On

Week 2 extends array and string traversal from Week 1. Instead of repeatedly scanning the same data, you learn how to maintain a moving range or two coordinated positions.

## Topics

### Two Pointers

* Opposite-direction pointers
* Same-direction pointers
* Fast and slow pointers on arrays
* Pair-sum problems
* Removing duplicates
* Partitioning arrays

### Sliding Window

* Fixed-size window
* Variable-size window
* Longest substring problems
* Minimum window problems
* Frequency-based windows
* Window with HashMap / HashSet

### Prefix Sum

* One-dimensional prefix sum
* Range sum queries
* Prefix sum + HashMap
* Prefix sum + frequency counting
* Difference array
* Two-dimensional prefix sum
* Subarray sum problems

## Patterns

* Expand and shrink a window
* Maintain a running sum
* Maintain a frequency map
* Convert repeated range work into O(1) queries
* Use prefix sum differences

## Practice Focus

* Two Sum in a sorted array
* Container With Most Water
* Remove duplicates from sorted array
* Longest substring without repeating characters
* Minimum size subarray sum
* Maximum sum subarray of size K
* Subarray Sum Equals K
* Range Sum Query
* Corporate Flight Bookings using a difference array

## LeetCode Problems by Pattern

### Opposite-Direction Two Pointers

* 167. Two Sum II - Input Array Is Sorted
* 11. Container With Most Water
* 15. 3Sum
* 16. 3Sum Closest
* 18. 4Sum

### Same-Direction Two Pointers

* 26. Remove Duplicates from Sorted Array
* 27. Remove Element
* 283. Move Zeroes
* 392. Is Subsequence
* 844. Backspace String Compare

### Fixed-Size Sliding Window

* 643. Maximum Average Subarray I
* 567. Permutation in String
* 438. Find All Anagrams in a String
* 1052. Grumpy Bookstore Owner
* 1343. Number of Sub-arrays of Size K and Average Greater than or Equal to Threshold

### Variable-Size Sliding Window

* 3. Longest Substring Without Repeating Characters
* 209. Minimum Size Subarray Sum
* 424. Longest Repeating Character Replacement
* 904. Fruit Into Baskets
* 1004. Max Consecutive Ones III

### Prefix Sum

* 303. Range Sum Query - Immutable
* 560. Subarray Sum Equals K
* 525. Contiguous Array
* 974. Subarray Sums Divisible by K
* 1109. Corporate Flight Bookings
* 304. Range Sum Query 2D - Immutable

## Outcome

You should recognize when a problem can be solved by avoiding nested loops through two pointers, sliding windows, or prefix sums.

---

# Week 3: Hashing, Sorting, and Binary Search

## Builds On

Week 3 combines the traversal and range-processing techniques from Weeks 1 and 2 with faster lookup and ordered search.

Hashing provides fast memory-based lookup. Sorting creates order. Binary search exploits that order.

## Topics

### Hashing

* HashSet
* HashMap
* Frequency counting
* Duplicate detection
* Grouping problems
* Anagram problems
* Custom hashing
* Prefix sum + HashMap

### Sorting

* Built-in sorting
* Sorting with custom comparators
* Merge sort
* Quick sort
* Counting sort
* Bucket sort
* Radix sort
* Inversion count
* Dutch National Flag

### Binary Search

* Basic binary search
* First occurrence / last occurrence
* Lower bound / upper bound
* Floor / ceil problems
* Binary search on rotated arrays
* Binary search on matrix
* Peak element problems
* Search in an infinite array
* Binary search on answer

## Patterns

* Store previously seen values
* Sort before applying two pointers
* Search for a boundary instead of an exact value
* Search over a feasible answer range
* Use frequency maps to avoid repeated counting

## Practice Focus

* Two Sum
* Group Anagrams
* Longest Consecutive Sequence
* Sort Colors
* Merge Sort inversion count
* First and last position of an element
* Search in Rotated Sorted Array
* Find Minimum in Rotated Sorted Array
* Koko Eating Bananas
* Capacity to Ship Packages

## LeetCode Problems by Pattern

### HashMap and HashSet

* 1. Two Sum
* 49. Group Anagrams
* 128. Longest Consecutive Sequence
* 347. Top K Frequent Elements
* 380. Insert Delete GetRandom O(1)
* 560. Subarray Sum Equals K

### Sorting

* 75. Sort Colors
* 56. Merge Intervals
* 179. Largest Number
* 315. Count of Smaller Numbers After Self
* 493. Reverse Pairs

### Basic Binary Search

* 704. Binary Search
* 35. Search Insert Position
* 34. Find First and Last Position of Element in Sorted Array
* 69. Sqrt(x)
* 367. Valid Perfect Square

### Rotated Arrays and Boundaries

* 33. Search in Rotated Sorted Array
* 81. Search in Rotated Sorted Array II
* 153. Find Minimum in Rotated Sorted Array
* 162. Find Peak Element
* 852. Peak Index in a Mountain Array

### Binary Search on Answer

* 875. Koko Eating Bananas
* 1011. Capacity To Ship Packages Within D Days
* 410. Split Array Largest Sum
* 1482. Minimum Number of Days to Make m Bouquets
* 774. Minimize Max Distance to Gas Station

## Outcome

You should be able to choose between:

```text
HashMap → fast lookup
Sorting → create order
Binary Search → exploit sorted or monotonic conditions
```

---

# Week 4: Linked Lists, Stacks, Queues, and Deques

## Builds On

Week 4 applies pointer and ordering ideas to dynamic structures.

The fast and slow pointer technique extends the two-pointer ideas from Week 2. Stacks and queues introduce LIFO and FIFO processing, which will later support recursion, BFS, monotonic structures, and tree traversal.

## Topics

### Linked Lists

* Singly linked list
* Doubly linked list
* Circular linked list
* Fast and slow pointer
* Reverse linked list
* Merge linked lists
* Cycle detection
* Middle of linked list
* Remove Nth node
* Intersection of linked lists
* Palindrome linked list
* Add two numbers
* Copy list with random pointer
* Linked list design problems
* LRU Cache using Linked List + HashMap

### Stack

* Stack fundamentals
* Parentheses problems
* Expression evaluation
* Min Stack
* Stack simulation
* Stack with queue

### Queue and Deque

* Queue fundamentals
* Circular queue
* Deque
* Queue design problems
* Basic BFS queue usage

## Patterns

* Dummy node
* Pointer rewiring
* Fast and slow pointers
* LIFO processing
* FIFO processing
* Store order of unresolved elements

## Practice Focus

* Reverse Linked List
* Merge Two Sorted Lists
* Linked List Cycle
* Remove Nth Node From End
* Reorder List
* Copy List with Random Pointer
* Valid Parentheses
* Min Stack
* Implement Queue Using Stacks
* Design LRU Cache

## LeetCode Problems by Pattern

### Linked List Reversal and Rewiring

* 206. Reverse Linked List
* 92. Reverse Linked List II
* 24. Swap Nodes in Pairs
* 25. Reverse Nodes in k-Group
* 143. Reorder List

### Fast and Slow Pointers

* 141. Linked List Cycle
* 142. Linked List Cycle II
* 876. Middle of the Linked List
* 234. Palindrome Linked List
* 287. Find the Duplicate Number

### Linked List Merging

* 21. Merge Two Sorted Lists
* 23. Merge k Sorted Lists
* 148. Sort List
* 1669. Merge In Between Linked Lists

### Linked List Design

* 146. LRU Cache
* 707. Design Linked List
* 430. Flatten a Multilevel Doubly Linked List
* 138. Copy List with Random Pointer

### Stack and Parentheses

* 20. Valid Parentheses
* 155. Min Stack
* 150. Evaluate Reverse Polish Notation
* 224. Basic Calculator
* 394. Decode String

### Queue and Deque

* 232. Implement Queue using Stacks
* 225. Implement Stack using Queues
* 622. Design Circular Queue
* 641. Design Circular Deque
* 933. Number of Recent Calls

## Outcome

You should understand how to select between arrays, linked lists, stacks, queues, and deques based on access order and update requirements.

---

# Week 5: Monotonic Structures, Recursion, and Backtracking

## Builds On

Week 5 extends the stack and deque concepts from Week 4.

A monotonic stack uses stack behavior while maintaining sorted order. Recursion uses the call stack. Backtracking uses recursion to explore and undo choices.

## Topics

### Monotonic Stack

* Increasing monotonic stack
* Decreasing monotonic stack
* Next greater element
* Next smaller element
* Previous greater element
* Previous smaller element
* Stock span
* Largest rectangle in histogram
* Daily temperatures

### Monotonic Queue

* Sliding window maximum
* Sliding window minimum
* Maintaining candidates in a deque

### Recursion

* Basic recursion
* Recursion trees
* Divide and conquer
* Tail recursion
* Recursive state design
* Memoization foundation

### Backtracking

* Subsets
* Subsets II
* Combinations
* Combination Sum
* Permutations
* Permutations II
* Palindrome partitioning
* Word Search
* Rat in a Maze
* N Queens
* Sudoku Solver

## Patterns

* Push and pop while maintaining an invariant
* Choose, explore, undo
* Define a recursive state
* Stop at a base case
* Prune invalid branches
* Avoid duplicate choices

## Practice Focus

* Daily Temperatures
* Next Greater Element
* Largest Rectangle in Histogram
* Sliding Window Maximum
* Subsets
* Permutations
* Combination Sum
* Word Search
* N Queens

## LeetCode Problems by Pattern

### Monotonic Stack

* 496. Next Greater Element I
* 503. Next Greater Element II
* 739. Daily Temperatures
* 901. Online Stock Span
* 84. Largest Rectangle in Histogram
* 85. Maximal Rectangle
* 402. Remove K Digits
* 456. 132 Pattern

### Monotonic Deque

* 239. Sliding Window Maximum
* 1438. Longest Continuous Subarray With Absolute Diff Less Than or Equal to Limit
* 862. Shortest Subarray with Sum at Least K
* 1696. Jump Game VI

### Recursion and Divide and Conquer

* 50. Pow(x, n)
* 53. Maximum Subarray
* 108. Convert Sorted Array to Binary Search Tree
* 148. Sort List
* 912. Sort an Array

### Subsets and Combinations

* 78. Subsets
* 90. Subsets II
* 77. Combinations
* 39. Combination Sum
* 40. Combination Sum II
* 216. Combination Sum III

### Permutations and Constraint Search

* 46. Permutations
* 47. Permutations II
* 51. N-Queens
* 37. Sudoku Solver
* 79. Word Search
* 131. Palindrome Partitioning

## Outcome

You should recognize:

```text
Nearest greater/smaller → Monotonic Stack
Window maximum/minimum → Monotonic Deque
Explore all valid choices → Backtracking
```

---

# Week 6: Trees and Heaps

## Builds On

Week 6 uses recursion from Week 5 to process hierarchical data. It also introduces heaps, which combine array representation with priority-based access.

## Topics

### Trees

* Binary tree
* Tree node structure
* Preorder traversal
* Inorder traversal
* Postorder traversal
* Level order traversal
* Binary Search Tree
* Lowest Common Ancestor
* Tree construction
* Tree views
* Diameter of tree
* Balanced tree
* Path sum problems
* Serialization / deserialization
* Morris traversal
* Tree DP introduction

### Heap / Priority Queue

* Min heap
* Max heap
* Heap operations
* Top K problems
* Kth largest / smallest
* Merge K sorted structures
* Median from data stream
* Task scheduling problems

## Patterns

* Recursive tree decomposition
* DFS on trees
* BFS using a queue
* Inorder traversal for sorted BST values
* Use a heap when repeatedly selecting the smallest or largest item
* Maintain only the most important K elements

## Practice Focus

* Maximum Depth of Binary Tree
* Binary Tree Level Order Traversal
* Validate Binary Search Tree
* Lowest Common Ancestor
* Diameter of Binary Tree
* Serialize and Deserialize Binary Tree
* Kth Smallest Element in a BST
* Kth Largest Element
* Top K Frequent Elements
* Merge K Sorted Lists
* Find Median from Data Stream

## LeetCode Problems by Pattern

### Tree DFS Traversal

* 144. Binary Tree Preorder Traversal
* 94. Binary Tree Inorder Traversal
* 145. Binary Tree Postorder Traversal
* 104. Maximum Depth of Binary Tree
* 543. Diameter of Binary Tree
* 124. Binary Tree Maximum Path Sum

### Tree BFS Traversal

* 102. Binary Tree Level Order Traversal
* 103. Binary Tree Zigzag Level Order Traversal
* 199. Binary Tree Right Side View
* 515. Find Largest Value in Each Tree Row
* 116. Populating Next Right Pointers in Each Node

### Binary Search Trees

* 98. Validate Binary Search Tree
* 230. Kth Smallest Element in a BST
* 235. Lowest Common Ancestor of a Binary Search Tree
* 450. Delete Node in a BST
* 700. Search in a Binary Search Tree

### Tree Construction and Serialization

* 105. Construct Binary Tree from Preorder and Inorder Traversal
* 106. Construct Binary Tree from Inorder and Postorder Traversal
* 297. Serialize and Deserialize Binary Tree
* 652. Find Duplicate Subtrees

### Heap and Priority Queue

* 215. Kth Largest Element in an Array
* 347. Top K Frequent Elements
* 23. Merge k Sorted Lists
* 295. Find Median from Data Stream
* 973. K Closest Points to Origin
* 703. Kth Largest Element in a Stream
* 621. Task Scheduler

## Outcome

You should be able to choose between:

```text
Tree recursion → hierarchical decomposition
Tree BFS → level-based processing
Heap → repeated priority selection
```

---

# Week 7: Greedy Algorithms, Intervals, and Advanced Sorting Patterns

## Builds On

Week 7 combines sorting from Week 3 with arrays, heaps from Week 6, and interval processing.

Greedy algorithms require making the best local decision while proving that it leads to a global solution.

## Topics

### Intervals

* Merge intervals
* Insert interval
* Non-overlapping intervals
* Meeting rooms
* Meeting rooms II
* Sweep line
* Line sweep
* Coordinate compression

### Greedy Algorithms

* Activity selection
* Scheduling
* Jump Game
* Gas Station
* Candy distribution
* Huffman concepts
* Greedy proof thinking
* Heap + greedy patterns

### Advanced Sorting Patterns

* Custom comparator
* Sort by start time
* Sort by end time
* Sort by frequency
* Sort by priority
* Partition-based processing

## Patterns

* Sort first, then make local decisions
* Track the farthest reachable position
* Track the earliest finishing interval
* Use a heap for active intervals
* Identify the invariant that makes the greedy choice safe

## Practice Focus

* Merge Intervals
* Insert Interval
* Non-overlapping Intervals
* Meeting Rooms II
* Jump Game
* Jump Game II
* Gas Station
* Candy
* Task Scheduler
* Minimum Number of Arrows to Burst Balloons

## LeetCode Problems by Pattern

### Interval Merging and Insertion

* 56. Merge Intervals
* 57. Insert Interval
* 986. Interval List Intersections
* 1288. Remove Covered Intervals
* 452. Minimum Number of Arrows to Burst Balloons

### Interval Scheduling

* 435. Non-overlapping Intervals
* 252. Meeting Rooms
* 253. Meeting Rooms II
* 646. Maximum Length of Pair Chain
* 1024. Video Stitching

### Sweep Line and Active Intervals

* 218. The Skyline Problem
* 732. My Calendar III
* 1094. Car Pooling
* 1109. Corporate Flight Bookings
* 850. Rectangle Area II

### Greedy Reachability

* 55. Jump Game
* 45. Jump Game II
* 134. Gas Station
* 763. Partition Labels
* 1029. Two City Scheduling

### Greedy Allocation and Scheduling

* 135. Candy
* 621. Task Scheduler
* 406. Queue Reconstruction by Height
* 452. Minimum Number of Arrows to Burst Balloons
* 948. Bag of Tokens

## Outcome

You should understand when sorting plus a local decision is enough and when a greedy strategy requires a proof.

---

# Week 8: Graphs, BFS, DFS, and Union Find

## Builds On

Week 8 generalizes tree traversal from Week 6.

A tree is a special type of graph. The BFS and DFS techniques used on trees now apply to arbitrary relationships, including cycles and multiple paths.

## Topics

### Graph Representation

* Adjacency list
* Adjacency matrix
* Directed graphs
* Undirected graphs
* Weighted graphs
* In-degree and out-degree

### Traversal

* BFS
* DFS
* Visited arrays and sets
* Connected components
* Grid as a graph
* Multi-source BFS

### Topological Sort

* Kahn's algorithm
* DFS-based topological sort
* Course schedule problems
* Dependency ordering

### Union Find

* Disjoint Set Union
* Find
* Union
* Path compression
* Union by rank
* Union by size
* Cycle detection
* Kruskal's algorithm foundation

### Graph Properties

* Bipartite graph
* Cycle detection
* Number of islands
* Flood fill
* Rotting oranges

## Patterns

* Queue for BFS
* Stack or recursion for DFS
* Mark nodes as visited
* Convert grids into graphs
* Use in-degree for dependency problems
* Use DSU for dynamic connectivity

## Practice Focus

* Number of Islands
* Clone Graph
* Course Schedule
* Course Schedule II
* Rotting Oranges
* Pacific Atlantic Water Flow
* Graph Valid Tree
* Number of Connected Components
* Is Graph Bipartite?
* Redundant Connection

## LeetCode Problems by Pattern

### Graph DFS and BFS

* 200. Number of Islands
* 133. Clone Graph
* 733. Flood Fill
* 695. Max Area of Island
* 417. Pacific Atlantic Water Flow
* 130. Surrounded Regions

### Multi-Source BFS

* 994. Rotting Oranges
* 542. 01 Matrix
* 286. Walls and Gates
* 1162. As Far from Land as Possible
* 934. Shortest Bridge

### Topological Sort

* 207. Course Schedule
* 210. Course Schedule II
* 269. Alien Dictionary
* 310. Minimum Height Trees
* 802. Find Eventual Safe States

### Union Find

* 684. Redundant Connection
* 721. Accounts Merge
* 547. Number of Provinces
* 323. Number of Connected Components in an Undirected Graph
* 1319. Number of Operations to Make Network Connected
* 990. Satisfiability of Equality Equations

### Bipartite and Cycle Detection

* 785. Is Graph Bipartite?
* 886. Possible Bipartition
* 261. Graph Valid Tree
* 684. Redundant Connection
* 785. Is Graph Bipartite?

## Outcome

You should be able to model real-world relationships as graphs and select BFS, DFS, topological sort, or DSU appropriately.

---

# Week 9: Shortest Paths, Minimum Spanning Trees, and Advanced Graph Algorithms

## Builds On

Week 9 extends the graph representation and traversal techniques from Week 8 to weighted graphs and more complex connectivity problems.

## Topics

### Shortest Path

* Dijkstra's algorithm
* Bellman-Ford
* Floyd-Warshall
* 0-1 BFS
* Shortest path in a DAG
* Weighted graph modeling

### Minimum Spanning Tree

* Kruskal's algorithm
* Prim's algorithm
* DSU connection to Kruskal
* Minimum cost to connect points

### Strong Connectivity

* Strongly connected components
* Kosaraju's algorithm
* Tarjan's algorithm

### Graph Structure

* Bridges
* Articulation points
* Euler path
* Euler circuit
* A* search concepts

## Patterns

* Use Dijkstra for non-negative weighted edges
* Use Bellman-Ford when negative edges may exist
* Use Floyd-Warshall for all-pairs shortest paths
* Use DSU for Kruskal
* Use priority queues for weighted exploration
* Track discovery and low-link times for bridges and articulation points

## Practice Focus

* Network Delay Time
* Cheapest Flights Within K Stops
* Path With Minimum Effort
* Min Cost to Connect All Points
* Connecting Cities With Minimum Cost
* Critical Connections in a Network
* Reconstruct Itinerary
* Word Ladder
* Swim in Rising Water

## LeetCode Problems by Pattern

### Dijkstra and Priority Queue

* 743. Network Delay Time
* 1631. Path With Minimum Effort
* 1514. Path with Maximum Probability
* 778. Swim in Rising Water
* 787. Cheapest Flights Within K Stops
* 1976. Number of Ways to Arrive at Destination

### Bellman-Ford and Relaxation

* 787. Cheapest Flights Within K Stops
* 743. Network Delay Time
* 1334. Find the City With the Smallest Number of Neighbors at a Threshold Distance
* 787. Cheapest Flights Within K Stops

### Floyd-Warshall and All-Pairs Paths

* 1334. Find the City With the Smallest Number of Neighbors at a Threshold Distance
* 1462. Course Schedule IV
* 399. Evaluate Division
* 2976. Minimum Cost to Convert String I

### Minimum Spanning Tree

* 1584. Min Cost to Connect All Points
* 1135. Connecting Cities With Minimum Cost
* 1489. Find Critical and Pseudo-Critical Edges in Minimum Spanning Tree
* 1168. Optimize Water Distribution in a Village

### Bridges and Strong Connectivity

* 1192. Critical Connections in a Network
* 1568. Minimum Number of Days to Disconnect Island
* 2360. Longest Cycle in a Graph
* 802. Find Eventual Safe States

### Eulerian Paths and Route Reconstruction

* 332. Reconstruct Itinerary
* 753. Cracking the Safe
* 2097. Valid Arrangement of Pairs

### Word and State Graphs

* 127. Word Ladder
* 126. Word Ladder II
* 433. Minimum Genetic Mutation
* 752. Open the Lock

## Outcome

You should understand how graph algorithms change when edges have weights, costs, or dependency constraints.

---

# Week 10: Dynamic Programming

## Builds On

Week 10 uses recursion and memoization from Week 5, arrays and prefix techniques from Weeks 1 and 2, and tree/graph state modeling from Weeks 6 through 9.

Dynamic programming is the process of solving overlapping subproblems while preserving their results.

## Topics

### DP Foundations

* Identifying states
* Defining transitions
* Base cases
* Memoization
* Tabulation
* Space optimization
* Top-down vs bottom-up

### Common DP Patterns

* 1D DP
* 2D DP
* Grid DP
* Knapsack pattern
* DP on subsequences
* String DP
* Longest Increasing Subsequence
* Partition DP
* Interval DP
* Tree DP
* Bitmask DP

## Practice Focus

### 1D DP

* Climbing Stairs
* House Robber
* Decode Ways
* Coin Change

### Grid DP

* Unique Paths
* Minimum Path Sum
* Dungeon Game

### Knapsack

* 0/1 Knapsack
* Partition Equal Subset Sum
* Target Sum
* Coin Change II

### Subsequences

* Longest Increasing Subsequence
* Longest Common Subsequence
* Edit Distance

### Interval DP

* Burst Balloons
* Matrix Chain Multiplication

### Tree DP

* House Robber III
* Diameter variations
* Maximum path sum

## Patterns

```text
State → What changes?
Transition → How do previous states create this state?
Base case → What is already known?
Order → In what sequence should states be computed?
```

## LeetCode Problems by Pattern

### 1D Dynamic Programming

* 70. Climbing Stairs
* 198. House Robber
* 213. House Robber II
* 91. Decode Ways
* 322. Coin Change
* 746. Min Cost Climbing Stairs
* 139. Word Break

### Grid Dynamic Programming

* 62. Unique Paths
* 63. Unique Paths II
* 64. Minimum Path Sum
* 120. Triangle
* 174. Dungeon Game
* 931. Minimum Falling Path Sum

### Knapsack and Subset DP

* 416. Partition Equal Subset Sum
* 494. Target Sum
* 518. Coin Change II
* 1049. Last Stone Weight II
* 474. Ones and Zeroes
* 879. Profitable Schemes

### Subsequence DP

* 300. Longest Increasing Subsequence
* 1143. Longest Common Subsequence
* 72. Edit Distance
* 516. Longest Palindromic Subsequence
* 673. Number of Longest Increasing Subsequence

### Interval DP

* 312. Burst Balloons
* 1039. Minimum Score Triangulation of Polygon
* 1547. Minimum Cost to Cut a Stick
* 1000. Minimum Cost to Merge Stones

### Tree and Graph DP

* 337. House Robber III
* 124. Binary Tree Maximum Path Sum
* 834. Sum of Distances in Tree
* 968. Binary Tree Cameras
* 1377. Frog Position After T Seconds

## Outcome

You should be able to convert recursive solutions into memoized and tabulated dynamic programming solutions.

---

# Week 11: Tries, Bit Manipulation, Strings, and Mathematics

## Builds On

Week 11 combines the string-processing foundation from Week 1, hashing from Week 3, recursion from Week 5, and graph/tree ideas from previous weeks.

## Topics

### Tries

* Trie basics
* Prefix search
* Word dictionary
* Autocomplete
* XOR Trie
* Trie-based string matching

### Bit Manipulation

* Bit basics
* XOR tricks
* Bitmasking
* Subset enumeration
* Count set bits
* Power of two / four checks
* Bitwise AND / OR / XOR problems

### Advanced Strings

* KMP algorithm
* Rabin-Karp
* Z algorithm
* Manacher's algorithm
* String hashing
* Pattern matching

### Mathematics

* GCD / LCM
* Prime numbers
* Sieve of Eratosthenes
* Modular arithmetic
* Fast exponentiation
* Combinatorics
* Catalan numbers
* Inclusion-exclusion
* Number theory basics

## Patterns

* Trie for prefix-based lookup
* Bitmask for compact state representation
* KMP/Z algorithm for linear-time pattern matching
* Modular arithmetic for large values
* GCD for divisibility and cycle-related problems
* Sieve for repeated prime queries

## Practice Focus

* Implement Trie
* Design Add and Search Words
* Word Search II
* Single Number
* Counting Bits
* Subsets using bitmasks
* Repeated DNA Sequences
* Implement strStr using KMP
* Longest Palindromic Substring
* GCD of Strings
* Count Primes
* Fast Power

## LeetCode Problems by Pattern

### Trie

* 208. Implement Trie
* 211. Design Add and Search Words Data Structure
* 212. Word Search II
* 648. Replace Words
* 677. Map Sum Pairs
* 720. Longest Word in Dictionary
* 421. Maximum XOR of Two Numbers in an Array

### Bit Manipulation

* 136. Single Number
* 191. Number of 1 Bits
* 338. Counting Bits
* 190. Reverse Bits
* 231. Power of Two
* 260. Single Number III
* 371. Sum of Two Integers
* 201. Bitwise AND of Numbers Range

### Bitmask and Subset Enumeration

* 78. Subsets
* 90. Subsets II
* 1239. Maximum Length of a Concatenated String with Unique Characters
* 847. Shortest Path Visiting All Nodes
* 1125. Smallest Sufficient Team
* 698. Partition to K Equal Sum Subsets

### String Matching

* 28. Find the Index of the First Occurrence in a String
* 459. Repeated Substring Pattern
* 686. Repeated String Match
* 1392. Longest Happy Prefix
* 214. Shortest Palindrome

### String Hashing and Frequency

* 187. Repeated DNA Sequences
* 49. Group Anagrams
* 438. Find All Anagrams in a String
* 567. Permutation in String
* 1044. Longest Duplicate Substring

### Mathematics and Number Theory

* 50. Pow(x, n)
* 204. Count Primes
* 202. Happy Number
* 1071. Greatest Common Divisor of Strings
* 365. Water and Jug Problem
* 1201. Ugly Number III
* 149. Max Points on a Line

## Outcome

You should recognize when a problem requires specialized string, bit, or mathematical techniques instead of general-purpose structures.

---

# Week 12: Advanced Data Structures, Advanced DP, and Interview Patterns

## Builds On

Week 12 combines the entire roadmap.

You will use arrays, hashing, binary search, trees, graphs, heaps, recursion, DP, and greedy reasoning as components of larger interview patterns.

## Topics

### Advanced Data Structures

* Segment Tree
* Lazy propagation
* Fenwick Tree / Binary Indexed Tree
* Sparse Table
* Ordered Set / Ordered Map
* Disjoint interval structures

### Advanced Dynamic Programming

* Digit DP
* State compression DP
* Probability DP
* DP optimizations
* Convex Hull Trick
* Bitset DP
* Game DP

### Interview Patterns

* Merge intervals
* Sweep line
* Line sweep
* Meet in the middle
* Coordinate compression
* Binary search on answer
* Prefix sum + hashing
* Monotonic stack
* Sliding window
* Two pointers
* Heap + greedy
* DSU patterns

### Advanced Graph Review

* Dijkstra
* Bellman-Ford
* Floyd-Warshall
* Tarjan's algorithm
* Kosaraju's algorithm
* A* search
* Bridges and articulation points
* Minimum cost flow

## Patterns

### Range Query Pattern

```text
Static range query
        ↓
Prefix Sum / Sparse Table

Dynamic range query
        ↓
Fenwick Tree / Segment Tree
```

### Connectivity Pattern

```text
Static traversal
        ↓
BFS / DFS

Dynamic merging
        ↓
DSU
```

### Optimization Pattern

```text
Monotonic answer condition
        ↓
Binary Search on Answer

Overlapping subproblems
        ↓
Dynamic Programming

Local optimal choice with proof
        ↓
Greedy
```

### Selection Pattern

```text
Repeated minimum/maximum
        ↓
Heap

Nearest greater/smaller
        ↓
Monotonic Stack

Window minimum/maximum
        ↓
Monotonic Deque
```

## Practice Focus

* Range Sum Query with updates
* Count of Smaller Numbers After Self
* Range Minimum Query
* My Calendar problems
* Skyline problem
* Median of two sorted arrays
* Word Break variations
* Digit DP counting problems
* Meet in the Middle subset problems
* Advanced shortest path problems
* Mixed mock interview problems

## LeetCode Problems by Pattern

### Fenwick Tree and Segment Tree

* 307. Range Sum Query - Mutable
* 308. Range Sum Query 2D - Mutable
* 315. Count of Smaller Numbers After Self
* 327. Count of Range Sum
* 493. Reverse Pairs
* 715. Range Module
* 732. My Calendar III

### Sparse Table and Static Range Queries

* 239. Sliding Window Maximum
* RMQ-style range minimum and maximum problems
* 1649. Create Sorted Array through Instructions
* 1906. Minimum Absolute Difference Queries

### Ordered Set and Ordered Map

* 220. Contains Duplicate III
* 352. Data Stream as Disjoint Intervals
* 729. My Calendar I
* 731. My Calendar II
* 732. My Calendar III
* 715. Range Module

### Sweep Line and Coordinate Compression

* 218. The Skyline Problem
* 850. Rectangle Area II
* 391. Perfect Rectangle
* 1094. Car Pooling
* 732. My Calendar III

### Binary Search on Answer

* 4. Median of Two Sorted Arrays
* 410. Split Array Largest Sum
* 774. Minimize Max Distance to Gas Station
* 1011. Capacity To Ship Packages Within D Days
* 1482. Minimum Number of Days to Make m Bouquets

### Meet in the Middle

* 1755. Closest Subsequence Sum
* 2035. Partition Array Into Two Arrays to Minimize Sum Difference
* 805. Split Array With Same Average
* 1434. Number of Ways to Wear Different Hats to Each Other

### Advanced Dynamic Programming

* digit DP problems such as 1012. Numbers With Repeated Digits
* digit DP problems such as 233. Number of Digit One
* state compression DP such as 847. Shortest Path Visiting All Nodes
* game DP such as 877. Stone Game
* probability DP such as 688. Knight Probability in Chessboard

### Mixed Interview Problems

* 42. Trapping Rain Water
* 76. Minimum Window Substring
* 84. Largest Rectangle in Histogram
* 239. Sliding Window Maximum
* 295. Find Median from Data Stream
* 297. Serialize and Deserialize Binary Tree
* 743. Network Delay Time
* 146. LRU Cache

## Outcome

You should be able to identify the underlying pattern in unfamiliar problems and combine multiple techniques.

---

# Weekly Study Structure

Use the following structure every week.

## Day 1: Learn the Concept

* Understand the data structure or algorithm
* Study its operations
* Learn time and space complexity
* Implement it from scratch

## Day 2: Basic Problems

* Solve easy problems
* Focus on syntax and mechanics
* Avoid looking at solutions too early

## Day 3: Core Patterns

* Solve standard medium problems
* Identify repeated problem structures
* Write down the invariant or state

## Day 4: Mixed Problems

* Combine the week's topic with previous topics
* Practice choosing the data structure independently
* Solve without knowing the pattern beforehand

## Day 5: Timed Practice

* Solve two or three problems under time limits
* Explain your approach aloud
* Analyze complexity

## Day 6: Review and Reimplementation

* Reimplement the main technique
* Review mistakes
* Revisit one difficult problem
* Create a short pattern summary

## Day 7: Rest or Light Review

* Review notes
* Read editorials
* Avoid heavy new material
* Prepare for the next week

---

# Concept Dependency Chain

The roadmap follows this dependency structure:

```text
Arrays
  ↓
Two Pointers
  ↓
Sliding Window
  ↓
Prefix Sum
  ↓
Hashing
  ↓
Sorting
  ↓
Binary Search
  ↓
Linked Lists
  ↓
Stacks and Queues
  ↓
Monotonic Structures
  ↓
Recursion
  ↓
Backtracking
  ↓
Trees
  ↓
Heaps
  ↓
Greedy Algorithms
  ↓
Graphs
  ↓
Shortest Paths and MST
  ↓
Dynamic Programming
  ↓
Tries, Bits, Strings, and Math
  ↓
Advanced Data Structures
  ↓
Advanced DP and Interview Patterns
```

---

# How the Topics Connect

## Arrays → Two Pointers

Arrays provide indexed access. Two pointers reduce unnecessary repeated scanning.

## Two Pointers → Sliding Window

A sliding window is a structured two-pointer technique where the range expands and contracts.

## Sliding Window → Prefix Sum

Both optimize repeated range calculations. Sliding windows work well for dynamic ranges, while prefix sums work well for fast static range queries.

## Prefix Sum → Hashing

Prefix sums become more powerful when combined with a HashMap to find previous sums and subarray relationships.

## Hashing → Sorting

Hashing provides fast lookup without order. Sorting creates order, which enables binary search, interval processing, and greedy decisions.

## Sorting → Binary Search

Binary search depends on sorted or monotonic structure.

## Arrays → Linked Lists

Both represent sequences, but arrays provide fast indexing while linked lists provide flexible pointer-based insertion and deletion.

## Linked Lists → Stacks and Queues

Stacks and queues can be implemented using arrays or linked lists. Their behavior is defined by access order rather than random access.

## Stacks and Queues → Monotonic Structures

Monotonic stacks and queues preserve LIFO/FIFO behavior while maintaining an ordering invariant.

## Recursion → Trees

Trees are naturally recursive because every subtree is itself a tree.

## Recursion → Backtracking

Backtracking uses recursion to explore choices and undo them.

## Trees → Graphs

A tree is a restricted graph with no cycles and exactly one path between connected nodes.

## Graphs → Shortest Paths

Once graph representation and traversal are understood, weighted graph algorithms become natural extensions.

## Recursion → Dynamic Programming

Dynamic programming begins with recursive state definitions and improves them using memoization or tabulation.

## Hashing and Trees → Tries

A Trie combines tree structure with string-prefix processing.

## Arrays and Prefix Sum → Advanced Data Structures

Segment Trees, Fenwick Trees, and Sparse Tables optimize range queries and updates.

---

# Final Problem-Solving Checklist

Before coding, ask:

```text
1. What is the input size?

2. What information must I remember?

3. Do I need fast index access?

4. Do I need key-to-value lookup?

5. Do I need uniqueness?

6. Do I need sorted order?

7. Do I need LIFO or FIFO processing?

8. Do I need nearest greater or smaller values?

9. Do I need a sliding window?

10. Do I need prefix or range information?

11. Do I need repeated minimum or maximum selection?

12. Is the data hierarchical?

13. Is the data connected as a graph?

14. Do I need connectivity queries?

15. Are there overlapping subproblems?

16. Is the answer condition monotonic?

17. Can sorting simplify the problem?

18. What invariant, state, or recurrence defines the solution?
```

The objective of this 12-week plan is to move from basic data access to advanced problem-solving patterns:

```text
Understand the data
        ↓
Choose the right structure
        ↓
Identify the pattern
        ↓
Build the invariant or state
        ↓
Implement efficiently
        ↓
Prove correctness
        ↓
Analyze complexity
```
