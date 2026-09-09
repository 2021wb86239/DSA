# Chapter 3 — Validation & Constraint Checking

Chapter 3 is another **simple but extremely important traversal pattern**.

The core idea is:

> **Assume the array is valid → scan for a violation → immediately return false when a violation is found.**

If the entire scan finishes without finding a violation:

> **Return true.**

---

# 3.1 The Core Pattern

```text
Assume valid
      ↓
Scan
      ↓
Check constraint
      ↓
Violation?
   ↙       ↘
 Yes        No
  ↓          ↓
false      continue
             ↓
          finished?
             ↓
            true
```

Generic form:

```text
valid = true

for each element:
    if constraint is violated:
        return false

return true
```

In practice, we often don't even need `valid`:

```text
for each element:
    if violation:
        return false

return true
```

This is the main pattern of the chapter.

---

# 3.2 Why Validation Is Different From Best Tracking

Compare Chapter 2:

> **What is the best answer I've seen so far?**

Chapter 3:

> **Have I seen anything that makes the answer invalid?**

So the state is often extremely small:

```text
valid / invalid
```

or sometimes we don't need explicit state at all.

We simply search for a **counterexample**.

---

# 3.3 The Important Mental Model

For a validation problem:

> **You don't need to prove that everything is valid. You only need to find one violation.**

For example:

> Is the array sorted?

Instead of checking:

> “Is every element correctly sorted?”

look for:

> “Can I find one adjacent pair that is out of order?”

If yes → invalid.

If no violation exists → valid.

This is a very powerful way of thinking.

---

# 3.4 Check if Array Is Sorted

Consider:

```text
[1, 2, 3, 5, 8]
```

Question:

> Is the array sorted in non-decreasing order?

Meaning:

```text
arr[i] <= arr[i + 1]
```

must hold for every adjacent pair.

So we scan:

```text
1 <= 2 ✓
2 <= 3 ✓
3 <= 5 ✓
5 <= 8 ✓
```

No violation.

Therefore:

```text
true
```

---

# 3.5 Finding the Violation

Consider:

```text
[1, 2, 7, 4, 8]
```

Check:

```text
1 <= 2 ✓
2 <= 7 ✓
7 <= 4 ✗
```

We found a violation.

Therefore immediately:

```text
false
```

We don't need to inspect `8`.

This is **early exit**.

---

# 3.6 Sorted — Generic Algorithm

For non-decreasing order:

```text
for i = 1 to n-1:
    if arr[i] < arr[i-1]:
        return false

return true
```

Notice the condition.

We reject when:

```text
current < previous
```

because that means the current value decreased.

---

# 3.7 Strictly Increasing

Now change the requirement.

> Every next element must be strictly greater than the previous element.

For:

```text
[1, 3, 5, 8]
```

valid.

For:

```text
[1, 3, 3, 8]
```

invalid.

Why?

Strictly increasing means:

```text
arr[i] > arr[i-1]
```

Therefore violation occurs when:

```text
arr[i] <= arr[i-1]
```

Algorithm:

```text
for i = 1 to n-1:
    if arr[i] <= arr[i-1]:
        return false

return true
```

---

# 3.8 Non-Decreasing vs Strictly Increasing

This distinction is essential.

| Requirement         | Valid relationship    | Violation             |
| ------------------- | --------------------- | --------------------- |
| Non-decreasing      | `current >= previous` | `current < previous`  |
| Strictly increasing | `current > previous`  | `current <= previous` |
| Non-increasing      | `current <= previous` | `current > previous`  |
| Strictly decreasing | `current < previous`  | `current >= previous` |

Examples:

```text
[1, 2, 2, 5]
```

Non-decreasing:

```text
true
```

Strictly increasing:

```text
false
```

because:

```text
2 == 2
```

---

# 3.9 The Invariant

For sortedness, the invariant is:

> **Before processing index `i`, all adjacent relationships before `i` satisfy the required ordering constraint.**

Or more simply:

> **After processing index `i`, the prefix `arr[0...i]` satisfies the required ordering property.**

When we find:

```text
arr[i] < arr[i-1]
```

the invariant is broken.

Therefore we immediately return:

```text
false
```

---

# 3.10 Why Do We Only Check Adjacent Elements?

This is an important reasoning question.

Suppose:

```text
[1, 3, 5, 8]
```

If every adjacent relationship satisfies:

```text
arr[i-1] <= arr[i]
```

then the entire sequence is non-decreasing.

We don't need to compare:

```text
1 with 5
1 with 8
3 with 8
```

because the transitive ordering is already established through adjacent elements:

```text
1 <= 3 <= 5 <= 8
```

Therefore:

> **For sortedness, adjacent comparisons are sufficient.**

This reduces the problem to a single linear scan.

---

# 3.11 Palindrome

Now the validation condition is different.

Problem:

> Determine whether an array reads the same forward and backward.

Example:

```text
[1, 2, 3, 2, 1]
```

Valid palindrome.

We need:

```text
arr[0] == arr[4]
arr[1] == arr[3]
arr[2] == arr[2]
```

The natural pattern is **two pointers**.

```text
left = 0
right = n - 1
```

Then:

```text
while left < right:
    if arr[left] != arr[right]:
        return false

    left++
    right--

return true
```

---

# 3.12 Why Early Exit Works for Palindrome

Consider:

```text
[1, 2, 7, 4, 1]
```

Compare:

```text
1 == 1 ✓
2 == 4 ✗
```

We already know the array cannot be a palindrome.

No reason to continue.

Therefore:

```text
return false
```

Again:

> **One counterexample is enough to invalidate the entire structure.**

---

# 3.13 Palindrome Invariant

At every iteration:

> **All pairs outside the `[left, right]` range have already been verified to match.**

So:

```text
[left ... right]
```

is the only unverified portion.

If:

```text
arr[left] != arr[right]
```

we have a violation.

If `left >= right`, every required pair has been checked.

Therefore:

```text
true
```

---

# 3.14 Why This Is Connected to Validation

Palindrome isn't just a two-pointer problem.

Its deeper structure is:

```text
Check constraint
      ↓
Violation?
      ↓
Yes → false
No  → continue
```

Two pointers simply give us an efficient way to perform the validation.

This is an important distinction:

> **A problem can involve multiple patterns.**

For palindrome:

```text
Primary purpose → validation
Technique       → two pointers
```

---

# 3.15 Duplicate Validation

Problem:

> Check whether an array contains duplicates.

Example:

```text
[2, 5, 7, 2]
```

There is a duplicate:

```text
2
```

Therefore:

```text
false
```

if the question is:

> “Are all elements unique?”

---

# 3.16 Brute Force

Compare every pair:

```text
for i:
    for j > i:
        if arr[i] == arr[j]:
            return false

return true
```

Time:

```text
O(n²)
```

This works but becomes expensive for large arrays.

---

# 3.17 Optimized Duplicate Validation

Use a `HashSet`.

As we scan:

```text
if current already exists:
    return false

add current
```

Example:

```text
[4, 7, 2, 7]
```

Process:

```text
4 → add
7 → add
2 → add
7 → already exists → false
```

This is another validation pattern:

> **Maintain the information needed to detect a future violation.**

---

# 3.18 Duplicate Validation State

Unlike sortedness, where we only need the previous element, duplicate checking requires remembering potentially many previous values.

State:

```text
seen
```

where:

```text
seen = all values encountered so far
```

Invariant:

> **After processing index `i`, `seen` contains exactly the distinct values encountered in `arr[0...i]`.**

When current value already exists:

```text
current ∈ seen
```

we found a violation.

---

# 3.19 Constraint Checking

Validation doesn't always mean sortedness or duplicates.

Imagine:

> Every array element must be between `1` and `100`.

Then:

```text
for each x:
    if x < 1 || x > 100:
        return false

return true
```

Or:

> Every element must be even.

```text
for each x:
    if x % 2 != 0:
        return false

return true
```

Or:

> No two adjacent elements may differ by more than 10.

```text
for i = 1 to n-1:
    if abs(arr[i] - arr[i-1]) > 10:
        return false

return true
```

The pattern remains unchanged.

---

# 3.20 Constraint Violation Thinking

Instead of asking:

> “How do I prove this array is valid?”

ask:

> **“What would make this array invalid?”**

Then identify the smallest condition representing that violation.

Examples:

### Sorted

Invalid when:

```text
current < previous
```

### Strictly increasing

Invalid when:

```text
current <= previous
```

### Unique

Invalid when:

```text
current already seen
```

### Range constraint

Invalid when:

```text
current < min || current > max
```

### Palindrome

Invalid when:

```text
left != right
```

This is the core of the chapter.

---

# 3.21 Early Exit

Early exit means:

> **Stop as soon as the final answer is already determined.**

For validation:

```text
violation found
      ↓
answer is definitely false
      ↓
STOP
```

Example:

```text
[1, 2, 3, 0, 1000000000, 500, ...]
```

If we're checking sortedness:

```text
3 > 0
```

already proves the array isn't sorted.

Everything after `0` is irrelevant.

---

# 3.22 Why Early Exit Is More Than an Optimization

Suppose:

```text
arr = [9, 1, 1000000, 5000000, ...]
```

We discover the violation immediately.

Early exit gives better **actual runtime**.

But more importantly, it reflects the logic of the problem:

> Once a counterexample exists, the proposition “the entire array is valid” is false.

So early exit is both:

* an optimization
* a consequence of the correctness logic

---

# 3.23 Validation Template

For simple validation:

```text
for each element:
    if violation:
        return false

return true
```

For adjacent validation:

```text
for i = 1 to n-1:
    if relation(previous, current) is invalid:
        return false

return true
```

For symmetric validation:

```text
left = 0
right = n - 1

while left < right:
    if relation(left, right) is invalid:
        return false

    left++
    right--

return true
```

For uniqueness validation:

```text
seen = empty set

for each x:
    if x is already in seen:
        return false

    add x to seen

return true
```

---

# 3.24 Java Templates

### Check sorted — non-decreasing

```java
boolean isSorted(int[] arr) {
    for (int i = 1; i < arr.length; i++) {
        if (arr[i] < arr[i - 1]) {
            return false;
        }
    }

    return true;
}
```

### Strictly increasing

```java
boolean isStrictlyIncreasing(int[] arr) {
    for (int i = 1; i < arr.length; i++) {
        if (arr[i] <= arr[i - 1]) {
            return false;
        }
    }

    return true;
}
```

### Palindrome

```java
boolean isPalindrome(int[] arr) {
    int left = 0;
    int right = arr.length - 1;

    while (left < right) {
        if (arr[left] != arr[right]) {
            return false;
        }

        left++;
        right--;
    }

    return true;
}
```

### No duplicates

```java
boolean containsNoDuplicates(int[] arr) {
    Set<Integer> seen = new HashSet<>();

    for (int x : arr) {
        if (!seen.add(x)) {
            return false;
        }
    }

    return true;
}
```

---

# 3.25 Complexity

### Sortedness

One scan:

```text
n elements × O(1)
= O(n)
```

Space:

```text
O(1)
```

So:

```text
Time  = O(n)
Space = O(1)
```

### Palindrome

We inspect at most half the array:

```text
n/2 × O(1)
= O(n)
```

Space:

```text
O(1)
```

So:

```text
Time  = O(n)
Space = O(1)
```

### Duplicate checking with HashSet

For `n` elements:

```text
n × average O(1)
= O(n)
```

Space:

```text
O(n)
```

So average:

```text
Time  = O(n)
Space = O(n)
```

---

# 3.26 Important Comparison

Notice the difference between these problems:

| Problem             | State                  |
| ------------------- | ---------------------- |
| Sorted              | Previous element       |
| Strictly increasing | Previous element       |
| Palindrome          | Left + right           |
| Range validation    | Current element        |
| No duplicates       | Set of previous values |

This teaches an important DSA principle:

> **The constraint determines the state.**

Don't start with:

> “I'll use two pointers.”

Start with:

> **“What information do I need to detect a violation?”**

Then choose the technique.

---

# 3.27 Validation vs Search

Another useful distinction:

### Search

> Find an element satisfying condition.

Example:

```text
Does 10 exist?
```

You can return:

```text
true
```

as soon as you find it.

### Validation

> Does the entire array satisfy a condition?

Example:

```text
Are all elements positive?
```

You return:

```text
false
```

as soon as you find one invalid element.

But you only return:

```text
true
```

after the entire relevant structure has been checked.

This asymmetry is important:

```text
Search:
found → true immediately

Validation:
violation → false immediately
valid → only after complete verification
```

---

# 3.28 Chapter 3 Recognition Signals

When a problem asks:

* Is the array valid?
* Is it sorted?
* Is it increasing?
* Is it a palindrome?
* Are all elements unique?
* Does every element satisfy...?
* Does the arrangement obey...?
* Check whether...
* Validate...
* Determine if...

Immediately think:

> **What is the violation condition?**

Then:

```text
Can I detect that violation in one pass?
```

---

# 3.29 Brute Force → Optimization

Take duplicate checking.

Brute force:

```text
Compare every pair
```

```text
O(n²)
```

Ask:

> Why am I repeatedly checking whether I've seen a value before?

Instead maintain:

```text
seen
```

Now:

```text
current already seen?
```

can be answered quickly.

So:

```text
O(n²)
      ↓
remember previous values
      ↓
HashSet
      ↓
O(n) average
```

This connects Chapter 3 directly to **Chapter 8 — Hashing + Arrays**.

---

# 3.30 Chapter 3 vs Chapter 1 vs Chapter 2

You now have three closely related patterns.

### Chapter 1 — Linear Traversal

Question:

> **What can I compute while scanning?**

Example:

```text
count even numbers
```

State:

```text
count
```

---

### Chapter 2 — Best Answer Tracking

Question:

> **What is the best answer I've seen so far?**

Example:

```text
maximum element
```

State:

```text
best
```

---

### Chapter 3 — Validation

Question:

> **What would make the answer invalid?**

Example:

```text
is array sorted?
```

State:

```text
previous
```

and violation:

```text
current < previous
```

---

# 3.31 The Universal Traversal Connection

Your Chapter 1 framework now expands nicely:

### Chapter 1

```text
What am I producing?
        ↓
What state do I need?
        ↓
How does state change?
        ↓
When can I stop?
```

### Chapter 2

```text
What is the best answer?
        ↓
What state represents the best so far?
        ↓
Can current improve it?
        ↓
Can I stop early?
```

### Chapter 3

```text
What makes the structure invalid?
        ↓
What state lets me detect that?
        ↓
Did current violate the constraint?
        ↓
YES → return false
NO  → continue
```

---

# 3.32 Chapter 3 Problem Progression

Follow this order.

### Level 1 — Basic Validation

1. Check all elements are positive
2. Check all elements are even
3. Check array contains a target
4. Check array contains no negative
5. Check every element is within `[L, R]`

### Level 2 — Ordering

6. Check sorted
7. Check non-decreasing
8. Check non-increasing
9. Check strictly increasing
10. Check strictly decreasing

### Level 3 — Structural Validation

11. Check palindrome
12. Check symmetric array
13. Check alternating arrangement
14. Validate adjacent difference constraint
15. Validate a specific arrangement

### Level 4 — Uniqueness

16. Check duplicates
17. Check all elements distinct
18. Find whether any value occurs more than once

Start with brute force, then optimize with hashing.

### Level 5 — Mixed Validation

19. Sorted + unique
20. Strictly increasing
21. All values within range + unique
22. Validate arrangement with multiple constraints
23. Validate before performing another operation

### Level 6 — Recognition

Mix Chapter 1–3 problems without labels.

Your job:

```text
Is this:
    Linear Traversal?
    Best Answer Tracking?
    Validation?
    Multiple patterns?
```

---

# 3.33 Chapter 3 Mastery Checklist

You should be able to immediately answer:

### Sortedness

What is the violation for:

```text
non-decreasing?
strictly increasing?
non-increasing?
strictly decreasing?
```

### Palindrome

Why are two pointers appropriate?

What does the invariant mean?

### Duplicates

Why is nested comparison `O(n²)`?

How does a `HashSet` reduce it to average `O(n)`?

### Early Exit

Why can validation return immediately when a violation is found?

### State

For each problem, identify the minimum required state:

```text
sorted          → ?
palindrome      → ?
duplicates      → ?
range validation→ ?
strict increase → ?
```

---

# 3.34 Final Mental Model

The three chapters now form a progression:

```text
Chapter 1
Linear Traversal
      ↓
Scan → Maintain State → Update State


Chapter 2
Best Answer Tracking
      ↓
Scan → Maintain Best State → Improve Answer


Chapter 3
Validation
      ↓
Scan → Check Constraint → Find Violation → Exit
```

The key question for Chapter 3 is:

> **“What is the smallest piece of evidence that can prove this structure is invalid?”**

Once you can answer that, the algorithm often becomes almost obvious.

**Chapter 3 core pattern:**

```text
Assume valid
      ↓
Identify violation condition
      ↓
Scan
      ↓
Violation?
  ↓       ↓
 YES      NO
  ↓        ↓
false    continue
           ↓
        finished
           ↓
          true
```

That is the entire foundation of **Validation & Constraint Checking**.
