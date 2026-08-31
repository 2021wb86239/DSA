Absolutely. **Chapter 2 is where we move from “process every element” to “process every element while continuously preserving the best answer.”**

The most important idea is not `max()` or `min()`. It is learning to recognize:

> **“The final answer can be built incrementally because I only need to remember the best candidate from the portion I have already processed.”**

# Chapter 2 — Best Answer Tracking

## 2.1 What Is Best Answer Tracking?

Suppose we have:

```text
arr = [7, 2, 9, 4, 6]
```

and we are asked:

> Find the largest element.

A beginner might think:

> “I need to compare every element with every other element.”

But we don't.

We can scan once:

```text
7 → best = 7
2 → best = 7
9 → best = 9
4 → best = 9
6 → best = 9
```

At every point, we maintain:

```text
best = best answer seen so far
```

This gives us the central pattern.

---

# 2.2 Core Question

Whenever you see a problem asking for some kind of **maximum, minimum, best, worst, largest, smallest, highest, lowest, etc.**, ask:

> **What is the best answer I've seen so far?**

Then ask:

> **Can I update that answer using only the current element and my existing state?**

If yes, you may have a **Best Answer Tracking** problem.

---

# 2.3 The Fundamental Pattern

The generic structure is:

```text
initialize best

for each element:
    compare current element with best
    update best if necessary

return best
```

For maximum:

```text
best = arr[0]

for i = 1 to n-1:
    best = max(best, arr[i])
```

For minimum:

```text
best = arr[0]

for i = 1 to n-1:
    best = min(best, arr[i])
```

The algorithm is extremely simple.

The important part is understanding **why it works**.

---

# 2.4 The Invariant

Our core invariant is:

> **After processing index `i`, `best` represents the optimal answer among elements from index `0` through `i`.**

For maximum:

```text
best = maximum(arr[0...i])
```

For minimum:

```text
best = minimum(arr[0...i])
```

This is much more important than memorizing the code.

---

# 2.5 Deriving the Maximum Algorithm

Suppose:

```text
arr = [5, 2, 8, 1, 7]
```

We want:

```text
max(arr)
```

After processing `5`:

```text
best = 5
```

Now we see `2`.

Only two possibilities exist:

```text
2 > 5
2 <= 5
```

If `2 > 5`, update.

Otherwise, keep `5`.

So:

```text
best = max(best, current)
```

Then `8` arrives:

```text
best = max(5, 8)
     = 8
```

Then:

```text
best = max(8, 1)
     = 8
```

Then:

```text
best = max(8, 7)
     = 8
```

Final:

```text
best = 8
```

---

# 2.6 Why Don't We Need the Entire Past?

This is the deeper idea.

Suppose we have processed:

```text
[5, 2, 8, 1]
```

and we know:

```text
best = 8
```

Do we need to remember:

```text
5
2
8
1
```

to process the next element?

No.

For finding the maximum, everything except `8` is irrelevant.

If the next element is `6`:

```text
max(8, 6) = 8
```

If the next element is `100`:

```text
max(8, 100) = 100
```

So we have compressed the entire processed history into:

```text
best = 8
```

This is a very important DSA concept:

> **State compression:** retain only the information from the past that can affect future decisions.

---

# 2.7 State

For a simple maximum problem:

```text
int best
```

is enough.

Its meaning is:

> Maximum value among all elements processed so far.

For minimum:

```text
int best
```

means:

> Minimum value among all elements processed so far.

Notice that the variable name isn't important.

Its **semantic meaning** is.

---

# 2.8 State Transition

Suppose:

```text
best = maximum(arr[0...i-1])
```

Now we encounter:

```text
arr[i]
```

There are only two possibilities.

### Case 1

```text
arr[i] > best
```

The new element is better.

Therefore:

```text
best = arr[i]
```

### Case 2

```text
arr[i] <= best
```

The existing answer is still better.

Therefore:

```text
best remains unchanged
```

So:

```text
best = max(best, arr[i])
```

This is the **state transition**.

---

# 2.9 Correct Initialization

A common mistake is:

```java
int best = 0;
```

This is not always correct.

Consider:

```text
arr = [-8, -3, -10]
```

If:

```java
int best = 0;
```

you would incorrectly return:

```text
0
```

But `0` isn't even in the array.

The correct initialization is usually:

```java
int best = arr[0];
```

because `arr[0]` is a legitimate candidate.

Then process:

```text
arr[1] ... arr[n-1]
```

This is a general principle:

> **Initialize the answer using a valid candidate whenever possible.**

---

# 2.10 Maximum vs Minimum

The pattern is identical.

| Problem       | State                | Transition                        |
| ------------- | -------------------- | --------------------------------- |
| Maximum       | largest so far       | `best = max(best, x)`             |
| Minimum       | smallest so far      | `best = min(best, x)`             |
| Longest       | longest so far       | update if current is longer       |
| Shortest      | shortest so far      | update if current is shorter      |
| Highest score | highest score so far | update if current score is better |
| Lowest cost   | lowest cost so far   | update if current cost is smaller |

So don't memorize separate algorithms.

Recognize the common pattern:

> **Track the optimal candidate seen so far.**

---

# 2.11 Running Maximum

There is an important variation.

Suppose:

```text
arr = [3, 1, 5, 2, 8]
```

Instead of asking for only the final maximum, suppose we want:

> Maximum value seen at every position.

Then:

```text
3 → 3
1 → 3
5 → 5
2 → 5
8 → 8
```

Result:

```text
[3, 3, 5, 5, 8]
```

This is called a **running maximum**.

We are still using exactly the same state:

```text
maxSoFar
```

but instead of returning it only at the end, we record it after every step.

---

## Running Maximum Example

```text
arr = [4, 2, 7, 1, 5]
```

|  i | arr[i] | maxSoFar |
| -: | -----: | -------: |
|  0 |      4 |        4 |
|  1 |      2 |        4 |
|  2 |      7 |        7 |
|  3 |      1 |        7 |
|  4 |      5 |        7 |

Therefore:

```text
runningMax = [4, 4, 7, 7, 7]
```

This pattern becomes extremely useful later for:

* Prefix maximum
* Trapping Rain Water
* Stock problems
* Array preprocessing
* Range-based optimization

---

# 2.12 Prefix Maximum

A running maximum is essentially a **prefix maximum**.

For:

```text
arr = [4, 2, 7, 1, 5]
```

we calculate:

```text
prefixMax[i] = max(arr[0...i])
```

Therefore:

```text
prefixMax = [4, 4, 7, 7, 7]
```

Likewise:

```text
prefixMin[i] = min(arr[0...i])
```

This gives:

```text
[4, 2, 2, 1, 1]
```

Keep this connection in mind.

Later, when we study **Prefix/Suffix Techniques**, this idea will become much more powerful.

---

# 2.13 Second Maximum

Now things become more interesting.

Problem:

```text
arr = [5, 2, 8, 1, 7]
```

Find the second largest element.

Answer:

```text
7
```

At first glance, you might think:

1. Find maximum.
2. Remove maximum.
3. Find maximum again.

That works.

But it requires two passes.

More importantly, we can solve it in **one pass**.

We need to track:

```text
largest
secondLargest
```

---

# 2.14 Why One Variable Isn't Enough

Suppose:

```text
arr = [5, 8, 7]
```

After processing:

```text
5
```

we know:

```text
largest = 5
```

After seeing `8`:

```text
largest = 8
```

But what happened to `5`?

It became a candidate for second largest.

Therefore when a new largest appears, the old largest must move down:

```text
secondLargest = largest
largest = current
```

This gives us the state:

```text
largest
secondLargest
```

---

# 2.15 Second Maximum State Transition

For every element `x`:

### Case 1 — New largest

```text
x > largest
```

Then:

```text
secondLargest = largest
largest = x
```

### Case 2 — Not largest, but better than second

```text
x > secondLargest
```

Then:

```text
secondLargest = x
```

Otherwise:

```text
do nothing
```

So the conceptual algorithm is:

```text
if x > largest:
    secondLargest = largest
    largest = x

else if x > secondLargest:
    secondLargest = x
```

---

# 2.16 Dry Run — Second Largest

Consider:

```text
arr = [5, 8, 2, 7, 10]
```

Initialize:

```text
largest = 5
secondLargest = -∞
```

### Process 8

```text
8 > 5
```

Therefore:

```text
secondLargest = 5
largest = 8
```

### Process 2

```text
2 < 8
2 < 5
```

Nothing changes.

```text
largest = 8
secondLargest = 5
```

### Process 7

```text
7 < 8
7 > 5
```

Therefore:

```text
secondLargest = 7
```

### Process 10

```text
10 > 8
```

Move the old largest down:

```text
secondLargest = 8
largest = 10
```

Final:

```text
largest = 10
secondLargest = 8
```

---

# 2.17 The Important Invariant for Two Best Values

For second maximum:

> **After processing index `i`, `largest` is the largest value seen so far and `secondLargest` is the second-largest valid candidate among the processed values.**

This is an example of **multiple-state tracking**.

The principle is the same:

```text
Best answer so far
```

but now we need to remember **two levels of quality**.

---

# 2.18 A Critical Question: What Does "Second Largest" Mean?

This is an interview trap.

Consider:

```text
[5, 8, 8, 3]
```

There are two interpretations.

### Distinct second largest

Distinct values:

```text
8, 5, 3
```

Therefore:

```text
second largest = 5
```

### Second element in sorted order

Sorted:

```text
3, 5, 8, 8
```

Then:

```text
second largest = 8
```

These are different problems.

Therefore always clarify:

> **Are duplicate values allowed to count as the second largest?**

This is exactly why **problem understanding** comes before coding.

---

# 2.19 Handling Duplicates

If the problem asks for the **second distinct largest**, we need:

```text
if x > largest:
    secondLargest = largest
    largest = x

else if x < largest && x > secondLargest:
    secondLargest = x
```

The important condition is:

```text
x < largest
```

This prevents a duplicate maximum from becoming the second distinct maximum.

For:

```text
[5, 8, 8, 3]
```

the result becomes:

```text
largest = 8
secondLargest = 5
```

---

# 2.20 What If There Is No Second Largest?

Consider:

```text
[8]
```

or:

```text
[8, 8, 8]
```

There is no second **distinct** largest value.

Your algorithm needs a way to represent that.

In Java, one approach is:

```java
Integer secondLargest = null;
```

This is often safer than choosing a magic value such as:

```text
-1
```

because the array could contain:

```text
[-10, -20, -30]
```

or:

```text
Integer.MIN_VALUE
```

The general lesson:

> **Sentinel values are safe only when the constraints guarantee that they cannot be valid answers.**

---

# 2.21 Second Minimum

Exactly the same pattern works in the opposite direction.

Maintain:

```text
smallest
secondSmallest
```

For each `x`:

```text
if x < smallest:
    secondSmallest = smallest
    smallest = x

else if x < secondSmallest:
    secondSmallest = x
```

For distinct values, additionally ensure:

```text
x > smallest
```

So:

```text
else if x > smallest && x < secondSmallest:
```

The structure is symmetric:

```text
Maximum:
largest
secondLargest

Minimum:
smallest
secondSmallest
```

---

# 2.22 Best Candidate

Now let's generalize beyond numbers.

Suppose each array element represents a candidate:

```text
Candidate {
    name
    score
}
```

Problem:

> Find the candidate with the highest score.

We don't necessarily care about the maximum **number**.

We care about the best **object**.

We can maintain:

```text
bestCandidate
```

For every candidate:

```text
if candidate.score > bestCandidate.score:
    bestCandidate = candidate
```

The pattern is therefore broader than:

```text
max(array)
```

It is:

> **Maintain the best candidate seen so far according to some comparison rule.**

---

# 2.23 Best Candidate as a General Pattern

Suppose:

```text
arr = [10, 25, 17, 31, 22]
```

and the problem says:

> Find the element with the highest value.

Comparison:

```text
x > best
```

Suppose instead:

> Find the index of the highest value.

Now the state is:

```text
bestIndex
```

and comparison becomes:

```text
arr[i] > arr[bestIndex]
```

Suppose:

> Find the person with the highest salary.

State:

```text
bestPerson
```

Comparison:

```text
person.salary > bestPerson.salary
```

Same pattern.

Only the **comparison rule** changes.

---

# 2.24 Best Pair

Now we reach a more interesting version.

Suppose:

```text
arr = [3, 8, 2, 10, 5]
```

Problem:

> Find the maximum difference between two elements where the larger element comes after the smaller element.

This is the classic stock-style pattern.

We want:

```text
arr[j] - arr[i]
```

where:

```text
i < j
```

and we want the maximum possible difference.

---

# 2.25 Brute Force

Try every pair:

```text
for i = 0 to n-1
    for j = i+1 to n-1
        calculate arr[j] - arr[i]
```

Time:

```text
O(n²)
```

For:

```text
n = 100,000
```

that's roughly:

```text
10^10
```

comparisons.

Too expensive.

---

# 2.26 Pattern Recognition

What does the formula say?

```text
arr[j] - arr[i]
```

For a fixed `j`, what value of `arr[i]` gives the largest answer?

The **smallest value before j**.

So instead of comparing `arr[j]` with every previous element, we only need:

```text
minimum value seen so far
```

This is the key transformation.

We convert:

> “Try every previous element”

into:

> “Remember the best previous candidate.”

That is **Best Answer Tracking**.

---

# 2.27 Maximum Difference

Suppose:

```text
arr = [7, 1, 5, 3, 6, 4]
```

We want maximum:

```text
arr[j] - arr[i]
```

with:

```text
i < j
```

Maintain:

```text
minSoFar
bestDifference
```

At each element:

```text
difference = current - minSoFar
```

Then:

```text
bestDifference = max(bestDifference, difference)
```

Finally:

```text
minSoFar = min(minSoFar, current)
```

---

# 2.28 Why This Order Matters

Suppose:

```text
current = arr[j]
```

We need a minimum from an **earlier** position.

Therefore:

```text
minSoFar
```

must represent elements before the current element.

So we conceptually do:

```text
calculate answer using previous state
then update state with current element
```

This distinction is extremely important.

Correct:

```text
difference = current - minSoFar
bestDifference = max(bestDifference, difference)
minSoFar = min(minSoFar, current)
```

If you update `minSoFar` first, you could accidentally use the current element as both:

```text
arr[i]
```

and:

```text
arr[j]
```

which violates:

```text
i < j
```

This is a very common invariant/order bug.

---

# 2.29 Dry Run — Maximum Difference

Input:

```text
[7, 1, 5, 3, 6, 4]
```

Initialize:

```text
minSoFar = 7
bestDifference = 0
```

| Current | minSoFar before | Difference | bestDifference | minSoFar after |
| ------: | --------------: | ---------: | -------------: | -------------: |
|       7 |               7 |          0 |              0 |              7 |
|       1 |               7 |         -6 |              0 |              1 |
|       5 |               1 |          4 |              4 |              1 |
|       3 |               1 |          2 |              4 |              1 |
|       6 |               1 |          5 |              5 |              1 |
|       4 |               1 |          3 |              5 |              1 |

Answer:

```text
5
```

The best transaction is:

```text
buy = 1
sell = 6
profit = 5
```

---

# 2.30 The Deeper Pattern

This problem looks like a **pair problem**.

A beginner might think:

> “Pair → nested loops.”

But the formula reveals:

```text
current - previous
```

For every current element, we don't need every previous element.

We only need the **best previous candidate**.

For maximum difference:

```text
best previous candidate = minimum previous value
```

This is a major interview skill:

> **When a pair problem contains a formula, ask whether one side of the pair can be summarized by a running best value.**

---

# 2.31 Maximum Difference Without Ordering Constraint

Now change the problem:

> Find the maximum absolute difference between any two elements.

Example:

```text
[3, 10, 2, 7]
```

The answer is:

```text
10 - 2 = 8
```

Do we need all pairs?

No.

The maximum absolute difference must occur between:

```text
global maximum
```

and:

```text
global minimum
```

Therefore:

```text
answer = maxElement - minElement
```

This requires only one traversal.

Maintain:

```text
maxSoFar
minSoFar
```

Then:

```text
answer = maxSoFar - minSoFar
```

This demonstrates an important principle:

> Sometimes a seemingly complex pair problem collapses into tracking a few extremal values.

---

# 2.32 Best Pair — General Recognition

Suppose you see:

> Find two elements that maximize/minimize some relationship.

Don't automatically jump to:

```text
O(n²)
```

Ask:

### Question 1

Can one element be summarized?

For example:

```text
current - minimumPrevious
```

### Question 2

Does only the best previous candidate matter?

If yes:

```text
maintain best previous candidate
```

### Question 3

Can the pair relationship be expressed using a running state?

If yes, a one-pass solution may exist.

---

# 2.33 Best Time to Buy and Sell Stock

This is one of the most important applications.

Given:

```text
prices = [7, 1, 5, 3, 6, 4]
```

You may buy once and sell once.

Goal:

> Maximize profit.

Profit:

```text
sellPrice - buyPrice
```

Constraint:

```text
buy before sell
```

This is exactly the maximum-difference problem.

---

# 2.34 Brute Force

Try every buy day and every later sell day:

```text
for i:
    for j > i:
        profit = prices[j] - prices[i]
```

Complexity:

```text
O(n²)
```

---

# 2.35 Pattern Recognition

For today's selling price:

```text
prices[j]
```

what buying price gives the maximum profit?

The smallest price seen before today.

Therefore maintain:

```text
minPrice
```

and calculate:

```text
profit = currentPrice - minPrice
```

Then maintain:

```text
bestProfit
```

So our state becomes:

```text
minPrice
bestProfit
```

---

# 2.36 The State Meaning

This is worth memorizing conceptually—not the code.

```text
minPrice
```

means:

> Cheapest buying opportunity seen before or at the relevant point.

```text
bestProfit
```

means:

> Maximum valid profit found so far.

The invariant is:

> **After processing index `i`, `minPrice` is the minimum price seen so far, and `bestProfit` is the maximum valid profit using days processed up to `i`.**

---

# 2.37 Why This Is Still Best Answer Tracking

At first glance, it looks like a different pattern.

But underneath:

```text
Best previous candidate
+
Best answer so far
```

We maintain two pieces of state.

The first state helps us generate a candidate answer.

The second state tracks the best candidate answer.

This is a very common structure in harder DSA problems.

---

# 2.38 A General Two-State Pattern

Many problems can be expressed as:

```text
bestPrevious
bestAnswer
```

For example:

### Maximum stock profit

```text
bestPrevious = minimum price
bestAnswer = maximum profit
```

### Maximum difference

```text
bestPrevious = minimum previous element
bestAnswer = maximum difference
```

### Some minimum-cost problems

```text
bestPrevious = cheapest previous option
bestAnswer = minimum total cost
```

The general reasoning is:

> **Maintain the best information from the past that allows the current element to produce the best possible candidate answer.**

---

# 2.39 Maximum vs Best Pair

Compare these two problems.

### Problem A

> Find maximum element.

State:

```text
best
```

Transition:

```text
best = max(best, current)
```

### Problem B

> Find maximum difference `arr[j] - arr[i]`, `i < j`.

State:

```text
minSoFar
bestDifference
```

Transition:

```text
bestDifference = max(bestDifference, current - minSoFar)
minSoFar = min(minSoFar, current)
```

Problem B is essentially:

```text
Best Answer Tracking
+
Best Previous Candidate Tracking
```

This is the direction in which your pattern recognition should develop.

---

# 2.40 A Useful Mental Transformation

When you see:

```text
maximize:
arr[j] - arr[i]
```

don't immediately see:

```text
two variables i and j
```

Instead ask:

> For the current `j`, what is the best possible `i`?

For maximum:

```text
arr[j] - minimumPrevious
```

For minimum difference:

```text
arr[j] - maximumPrevious
```

This transforms a pair search into a running-state problem.

---

# 2.41 Maximum Difference — Different Variations

Consider the following variants.

### Variant 1

> Maximum `arr[j] - arr[i]`, `i < j`

Track:

```text
minimum so far
best difference
```

### Variant 2

> Minimum `arr[j] - arr[i]`, `i < j`

Track:

```text
maximum so far
minimum difference
```

### Variant 3

> Maximum absolute difference between any two elements

Track:

```text
global minimum
global maximum
```

Answer:

```text
max - min
```

### Variant 4

> Maximum difference where indices don't matter

Again:

```text
global max - global min
```

### Variant 5

> Return the actual pair

Now track indices too:

```text
minIndex
bestBuyIndex
bestSellIndex
```

The underlying pattern doesn't change.

Only the **state** becomes richer.

---

# 2.42 State Is Determined by What the Future Needs

This is an extremely important lesson from Chapter 2.

Don't ask:

> “What variables do I normally use for this problem?”

Ask:

> **“What information from the past can the future need?”**

For maximum element:

```text
future only needs maximum
```

Therefore:

```text
best
```

For maximum difference:

```text
future needs smallest previous value
future also needs best difference
```

Therefore:

```text
minSoFar
bestDifference
```

For second maximum:

```text
future needs two best candidates
```

Therefore:

```text
largest
secondLargest
```

This is how you should derive state rather than memorize it.

---

# 2.43 Generic Best Answer Template

For a simple optimization:

```text
best = valid initial candidate

for each element x:
    if x is better than best:
        best = x

return best
```

For two-state optimization:

```text
bestPrevious = valid initial candidate
bestAnswer = worst valid answer

for each current element:
    candidate = combine(bestPrevious, current)

    if candidate improves bestAnswer:
        bestAnswer = candidate

    update bestPrevious using current

return bestAnswer
```

The second template is extremely valuable.

---

# 2.44 Generic Java Templates

### Maximum

```java
int max = arr[0];

for (int i = 1; i < arr.length; i++) {
    max = Math.max(max, arr[i]);
}
```

### Minimum

```java
int min = arr[0];

for (int i = 1; i < arr.length; i++) {
    min = Math.min(min, arr[i]);
}
```

### Running Maximum

```java
int maxSoFar = arr[0];

for (int i = 0; i < arr.length; i++) {
    maxSoFar = Math.max(maxSoFar, arr[i]);
    // use/store maxSoFar
}
```

### Maximum Difference

```java
int minSoFar = arr[0];
int bestDifference = Integer.MIN_VALUE;

for (int i = 1; i < arr.length; i++) {
    int currentDifference = arr[i] - minSoFar;

    bestDifference = Math.max(
        bestDifference,
        currentDifference
    );

    minSoFar = Math.min(minSoFar, arr[i]);
}
```

For a stock problem where the answer is allowed to be `0` when no profit is possible:

```java
int minPrice = prices[0];
int bestProfit = 0;

for (int i = 1; i < prices.length; i++) {
    bestProfit = Math.max(bestProfit, prices[i] - minPrice);
    minPrice = Math.min(minPrice, prices[i]);
}
```

---

# 2.45 Complexity Derivation

For simple maximum:

```text
n elements
×
O(1) work per element
=
O(n)
```

Space:

```text
Only one variable
=
O(1)
```

Therefore:

```text
Time  = O(n)
Space = O(1)
```

For maximum difference:

```text
n elements
×
O(1) work per element
=
O(n)
```

State:

```text
minSoFar
bestDifference
```

constant number of variables:

```text
O(1)
```

Therefore:

```text
Time  = O(n)
Space = O(1)
```

---

# 2.46 Can We Do Better Than O(n)?

For finding the maximum element, no asymptotically faster algorithm exists in the general unsorted case.

Why?

Because any element could potentially be the maximum.

For example:

```text
[2, 7, 4, 9, 1]
```

If you don't inspect `9`, you cannot know whether it is the maximum.

Therefore:

```text
Ω(n)
```

comparisons are necessary in the general case.

Our algorithm:

```text
O(n)
```

matches the lower bound.

Therefore:

> **O(n) is asymptotically optimal.**

This is an important habit:

> Don't stop at “my solution is O(n).” Ask whether O(n) is actually necessary.

---

# 2.47 Common Mistakes

## Mistake 1 — Initializing maximum to zero

```java
int max = 0;
```

Fails for all-negative arrays.

Prefer:

```java
int max = arr[0];
```

when the array is guaranteed non-empty.

---

## Mistake 2 — Incorrect second-largest logic

Incorrect:

```java
if (x > largest) {
    largest = x;
}
else if (x > secondLargest) {
    secondLargest = x;
}
```

What's missing?

When `largest` changes, the old `largest` must become `secondLargest`.

Correct:

```java
if (x > largest) {
    secondLargest = largest;
    largest = x;
}
```

---

## Mistake 3 — Ignoring duplicates

You must determine whether:

```text
[8, 8, 5]
```

has second largest:

```text
8
```

or:

```text
5
```

depending on the definition.

---

## Mistake 4 — Updating state in the wrong order

For maximum difference:

```java
minSoFar = Math.min(minSoFar, arr[i]);
best = Math.max(best, arr[i] - minSoFar);
```

can accidentally allow the current element to serve as its own previous element.

Think carefully about:

```text
What must my state represent BEFORE processing current?
```

---

## Mistake 5 — Tracking too much information

For maximum:

```text
all previous elements
```

are unnecessary.

You only need:

```text
best
```

A strong algorithm often comes from discovering that the past can be compressed.

---

# 2.48 Recognition Signals

When reading an unfamiliar problem, watch for words like:

### Direct signals

* largest
* smallest
* maximum
* minimum
* highest
* lowest
* best
* worst
* greatest
* least

### Relationship signals

* maximum difference
* minimum difference
* maximum profit
* best pair
* best previous value
* maximum gain
* minimum cost

### Structural signals

* “as you scan”
* “among elements seen so far”
* “before this element”
* “previous”
* “earlier”
* “best possible”

These should trigger:

> **Can I maintain an optimal candidate while scanning?**

---

# 2.49 Recognition Decision Tree

When you see an optimization problem over an array:

```text
             Optimization?
                  |
          +-------+-------+
          |               |
       Single            Pair/
       element          relationship
          |               |
     Track best      Can one side be
     candidate       summarized?
                          |
                    +-----+-----+
                    |           |
                   Yes          No
                    |           |
              Running best   Consider other
              candidate      patterns
```

For example:

```text
Find maximum element
        ↓
Single element
        ↓
Track best
        ↓
O(n)
```

But:

```text
Maximum arr[j] - arr[i]
        ↓
Pair relationship
        ↓
For each j, need best i
        ↓
Minimum previous arr[i]
        ↓
Track min + answer
        ↓
O(n)
```

---

# 2.50 Brute Force → Optimization Derivation

This is one of the most important exercises.

Suppose:

> Find maximum `arr[j] - arr[i]`, `i < j`.

### Brute force

```text
Try every pair
```

Complexity:

```text
O(n²)
```

### Ask:

> For a fixed `j`, do I really need every previous `i`?

No.

We only need the smallest previous `arr[i]`.

Therefore:

```text
minSoFar
```

summarizes all previous candidates.

Then:

```text
candidate = arr[j] - minSoFar
```

Then track:

```text
bestDifference
```

This transforms:

```text
O(n²)
```

into:

```text
O(n)
```

The optimization didn't come from a clever coding trick.

It came from **identifying which information from the past actually matters**.

---

# 2.51 Chapter 1 vs Chapter 2

This distinction is important.

### Chapter 1 — Linear Traversal

Core question:

> **What do I need to compute while scanning?**

Example:

```text
Count even numbers.
```

State:

```text
count
```

Transition:

```text
if even:
    count++
```

---

### Chapter 2 — Best Answer Tracking

Core question:

> **What is the best answer I've seen so far?**

Example:

```text
Find maximum.
```

State:

```text
best
```

Transition:

```text
best = max(best, current)
```

---

### More advanced Chapter 2

Core question:

> **What is the best previous candidate that helps the current element produce the best answer?**

Example:

```text
Maximum difference
```

State:

```text
minSoFar
bestDifference
```

This is the bridge from simple traversal to more sophisticated patterns.

---

# 2.52 Chapter 2's Three Levels

You should mentally organize this chapter into three levels.

## Level 1 — Direct Best Tracking

```text
maximum
minimum
largest
smallest
```

Pattern:

```text
best = better(best, current)
```

---

## Level 2 — Multiple Best Candidates

```text
second largest
second smallest
top two
best two candidates
```

Pattern:

```text
best
secondBest
```

---

## Level 3 — Best Previous Candidate + Best Answer

```text
maximum difference
best stock profit
best pair under ordering constraint
```

Pattern:

```text
bestPrevious
bestAnswer
```

This third level is particularly important for interviews.

---

# 2.53 The Most Important Concept of This Chapter

Don't memorize:

```java
Math.max(...)
```

Instead internalize:

> **I am scanning the array. I don't need the entire history. I need only the best piece of information from the history that can influence the future.**

For maximum:

```text
history → maximum
```

For minimum:

```text
history → minimum
```

For second maximum:

```text
history → top two
```

For stock profit:

```text
history → minimum buying price
```

For maximum difference:

```text
history → minimum previous value
```

This is **state compression through an invariant**.

---

# 2.54 Chapter 2 Problem Progression

I recommend solving the chapter in this order rather than jumping directly to famous problems.

### Level 1 — Pure Best Tracking

1. Find largest element
2. Find smallest element
3. Find maximum positive value
4. Find minimum negative value
5. Find maximum index
6. Find minimum index
7. Find largest even number
8. Find smallest odd number

### Level 2 — Running Best

9. Running maximum
10. Running minimum
11. Prefix maximum
12. Prefix minimum
13. Count how many times a new maximum appears
14. Count how many times a new minimum appears

### Level 3 — Multiple Best Values

15. Second largest
16. Second smallest
17. Second largest distinct
18. Second smallest distinct
19. Largest and second largest together
20. Smallest and second smallest together

### Level 4 — Best Candidate

21. Index of maximum
22. Element with maximum frequency/value according to a criterion
23. Best student/candidate based on score
24. Best candidate satisfying a condition
25. Best element according to a custom comparison

### Level 5 — Best Previous Candidate

26. Maximum difference
27. Minimum difference with ordering
28. Best time to buy and sell stock
29. Maximum profit with one transaction
30. Maximum `arr[j] - arr[i]` where `i < j`

### Level 6 — Variations

31. Return indices instead of value
32. Return the actual pair
33. Handle duplicates
34. Handle all-negative values
35. Handle no valid second maximum
36. Maximum difference with constraints
37. Maximum difference between elements at least K apart

### Level 7 — Recognition Problems

Then remove the chapter label and mix problems from:

* Linear Traversal
* Best Answer Tracking
* Hashing
* Two Pointers

The goal is to determine:

> **Is this merely a traversal, or is there a best-state I can maintain?**

---

# 2.55 Chapter 2 Mastery Checklist

Before leaving this chapter, you should be able to answer these without hesitation:

### Concept

* What does best answer tracking mean?
* Why can maximum be solved in one pass?
* Why can minimum be solved in one pass?
* What does "running maximum" mean?
* What is a prefix maximum?

### State

* What is the state for maximum?
* What is the state for second maximum?
* What is the state for maximum difference?
* Why does maximum difference need two state variables?

### Invariant

Can you complete:

> “After processing index `i`, `best` represents ______.”

And:

> “Before processing `arr[i]`, `minSoFar` represents ______.”

### Optimization

Can you explain:

> Why does maximum difference not require `O(n²)`?

without mentioning code?

### Edge Cases

Can you handle:

```text
all negative
all positive
duplicates
single element
all equal
no valid second distinct maximum
```

### Recognition

Given an unfamiliar problem, can you identify:

```text
What is the answer?
What is the candidate?
What information from the past matters?
Can that information be summarized?
What is my state?
What is my invariant?
```

---

# 2.56 The Chapter 2 Mental Model

I want you to leave this chapter with this hierarchy in your head:

```text
ARRAY
  ↓
SCAN
  ↓
What information from the past matters?
  ↓
Can I compress that information?
  ↓
YES
  ↓
Maintain BEST STATE
  ↓
Current element arrives
  ↓
Generate candidate answer
  ↓
Compare with BEST ANSWER
  ↓
Update state
  ↓
Continue
```

And the most important progression is:

```text
Maximum
   ↓
Running Maximum
   ↓
Second Maximum
   ↓
Best Candidate
   ↓
Best Previous Candidate
   ↓
Best Pair / Maximum Difference
   ↓
More advanced optimization patterns
```

### The one sentence to remember

> **Best Answer Tracking = scan the array while maintaining the smallest amount of state necessary to represent the best solution among everything seen so far.**

And the central invariant:

> **After processing index `i`, my state represents the optimal candidate/answer obtainable from the processed portion of the array.**

That idea will reappear later in **Greedy, Sliding Window, Monotonic Structures, Binary Search on Answer, and Dynamic Programming**—so Chapter 2 is much more fundamental than its simple-looking problems suggest.
