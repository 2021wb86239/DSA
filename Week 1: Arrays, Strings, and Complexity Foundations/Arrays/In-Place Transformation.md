# Chapter 4 — In-Place Transformation

This chapter is about **changing the array itself without creating another array**.

The core question is:

> **How can I rearrange the existing elements while maintaining a clear boundary between what is already fixed and what is still being processed?**

---

# 4.1 What Does In-Place Mean?

An algorithm is generally considered **in-place** when it uses only a constant amount of extra space.

Example:

```text
[1, 2, 3, 4, 5]
```

Reverse it directly:

```text
[5, 4, 3, 2, 1]
```

Instead of:

```text
create new array
→ copy elements in reverse order
→ return new array
```

we modify the original array.

Usually:

```text
Extra Space = O(1)
```

> The input array itself can be modified. The important part is that we don't use another data structure proportional to `n`.

---

# 4.2 The Core Model — Processed vs Unprocessed

Most in-place problems can be understood as:

```text
[ processed | unprocessed ]
```

For example:

```text
[2, 0, 4, 0, 7, 1]
```

While processing, you may maintain:

```text
[ correctly arranged | still needs work ]
```

The boundary moves as the algorithm progresses.

For example:

```text
[2, 4 | 0, 0, 7, 1]
```

Then:

```text
[2, 4, 7 | 0, 0, 1]
```

The left side satisfies some invariant.

This is the central idea:

> **At every step, clearly define what part of the array is already correct.**

---

# 4.3 Swap

A swap exchanges two elements.

```text
arr[i] ↔ arr[j]
```

Example:

```text
[1, 2, 3, 4]
```

Swap indices `0` and `3`:

```text
[4, 2, 3, 1]
```

Java:

```java
int temp = arr[i];
arr[i] = arr[j];
arr[j] = temp;
```

Swap is the basic operation behind:

* Reverse
* Partition
* Sort Colors
* Many Two Pointer problems
* QuickSort partitioning

---

# 4.4 Shift

Sometimes elements need to be moved to create space or close a gap.

Example:

```text
[2, 5, 7, 9]
```

Logically remove `5`:

```text
[2, 7, 9, _]
```

The elements after it shift left.

Similarly, insertion may require:

```text
[2, 5, _, 7, 9]
```

Insert `6`:

```text
[2, 5, 6, 7, 9]
```

But physical shifting can be expensive.

For one insertion/deletion:

```text
O(n)
```

This leads to an important DSA idea:

> Sometimes we don't physically delete or insert. We maintain a logical boundary instead.

---

# 4.5 Overwrite

Overwrite means:

> Put the correct value into the next correct position.

Example:

```text
[1, 2, 2, 3, 3, 4]
```

Suppose we want unique elements at the front.

We maintain:

```text
[unique values | unprocessed]
```

Process the array:

```text
[1 | 2, 2, 3, 3, 4]
```

Next unique value `2`:

```text
[1, 2 | 2, 3, 3, 4]
```

Skip duplicate `2`.

Next unique value `3`:

```text
[1, 2, 3 | 3, 3, 4]
```

Eventually:

```text
[1, 2, 3, 4 | ...]
```

We don't care what remains after the valid portion.

This is extremely important.

---

# 4.6 Logical Deletion

Arrays have fixed size.

You cannot truly shrink a normal Java array in place.

Suppose:

```text
[3, 2, 2, 3]
```

Remove all `3`s.

After transformation:

```text
[2, 2, _, _]
```

The important result is:

```text
newLength = 2
```

So logically:

```text
Valid array = arr[0...newLength - 1]
```

The rest:

```text
arr[newLength...n-1]
```

doesn't matter.

This is called **logical deletion**.

---

# 4.7 Read Pointer and Write Pointer

This is one of the most important patterns in this chapter.

```text
read  → scans every element
write → points to next valid position
```

Generic structure:

```text
write = 0

for read = 0 to n-1:

    if arr[read] should be kept:
        arr[write] = arr[read]
        write++
```

At the end:

```text
[ valid elements | irrelevant elements ]
          ↑
        write
```

`write` represents:

> The number of valid elements.

---

# 4.8 Example — Remove Element

Array:

```text
[3, 2, 2, 3]
```

Remove:

```text
3
```

Start:

```text
write = 0
```

### `read = 0`

```text
arr[0] = 3
```

Don't keep.

```text
write = 0
```

Array unchanged:

```text
[3, 2, 2, 3]
```

### `read = 1`

```text
arr[1] = 2
```

Keep.

```text
arr[write] = arr[read]
arr[0] = 2
write++
```

Now:

```text
[2, 2, 2, 3]
 ↑
valid
```

### `read = 2`

Keep `2`:

```text
[2, 2, 2, 3]
```

Now:

```text
write = 2
```

Finished.

Valid region:

```text
[2, 2]
```

Return:

```text
2
```

---

# 4.9 The Invariant for Read/Write

This is the key:

> **Before processing `read`, all elements in `arr[0...write-1]` are exactly the elements we decided to keep from the already processed region.**

In simpler form:

```text
[ correct result | processed but rejected/unimportant | unprocessed ]
```

As `read` moves:

```text
[ valid | irrelevant | unprocessed ]
```

The `write` pointer expands the valid region.

---

# 4.10 Move Zeroes

Problem:

```text
[0, 1, 0, 3, 12]
```

Move all zeroes to the end while preserving the relative order of non-zero elements.

Expected:

```text
[1, 3, 12, 0, 0]
```

Think:

```text
Keep non-zero elements
```

So use read/write.

### Phase 1 — Compact non-zero elements

```text
write = 0

for read = 0 to n-1:
    if arr[read] != 0:
        arr[write] = arr[read]
        write++
```

After this:

```text
[1, 3, 12 | ?, ?]
```

### Phase 2 — Fill remaining positions

```text
while write < n:
    arr[write] = 0
    write++
```

Result:

```text
[1, 3, 12, 0, 0]
```

This is a beautiful example of:

> **Logical deletion + overwrite + reconstruction.**

---

# 4.11 Why Not Swap for Move Zeroes?

Suppose:

```text
[0, 1, 0, 3, 12]
```

If we blindly swap a zero with every non-zero:

```text
swap 0 and 1
→ [1, 0, 0, 3, 12]

swap first zero and 3
→ [1, 3, 0, 0, 12]
```

This can work with a carefully designed two-pointer approach, but the deeper requirement is:

> **Preserve the order of non-zero elements.**

So you must always ask:

> Does the transformation require stability?

**Stable** means relative order is preserved.

Example:

```text
[a, 0, b, 0, c]
```

Should become:

```text
[a, b, c, 0, 0]
```

not:

```text
[c, b, a, 0, 0]
```

---

# 4.12 Remove Duplicates from Sorted Array

Example:

```text
[1, 1, 2, 2, 3]
```

Expected valid region:

```text
[1, 2, 3]
```

Because the array is sorted, duplicates are adjacent.

Use two pointers.

```text
read  → scans
write → last unique position
```

Initialize:

```text
write = 1
```

The first element is automatically unique.

For every `read` from `1`:

```text
if arr[read] != arr[read - 1]:
    arr[write] = arr[read]
    write++
```

Result:

```text
[1, 2, 3, ...]
```

Return:

```text
write
```

Important invariant:

> **`arr[0...write-1]` contains all unique elements from the processed part.**

---

# 4.13 Reverse Array

This is a pure swapping transformation.

Example:

```text
[1, 2, 3, 4, 5]
```

Use:

```text
left = 0
right = n - 1
```

Swap:

```text
1 ↔ 5
```

```text
[5, 2, 3, 4, 1]
```

Then:

```text
2 ↔ 4
```

```text
[5, 4, 3, 2, 1]
```

Move:

```text
left++
right--
```

Stop when:

```text
left >= right
```

Java:

```java
void reverse(int[] arr) {
    int left = 0;
    int right = arr.length - 1;

    while (left < right) {
        int temp = arr[left];
        arr[left] = arr[right];
        arr[right] = temp;

        left++;
        right--;
    }
}
```

Invariant:

> **Everything outside `[left, right]` is already reversed correctly.**

---

# 4.14 Rotate Array

Example:

```text
[1, 2, 3, 4, 5, 6, 7]
```

Rotate right by `3`:

```text
[5, 6, 7, 1, 2, 3, 4]
```

A powerful in-place technique is:

### Step 1

Reverse entire array:

```text
[7, 6, 5, 4, 3, 2, 1]
```

### Step 2

Reverse first `k`:

```text
[5, 6, 7, 4, 3, 2, 1]
```

### Step 3

Reverse remaining:

```text
[5, 6, 7, 1, 2, 3, 4]
```

This is:

```text
Reverse All
      ↓
Reverse First Part
      ↓
Reverse Second Part
```

Time:

```text
O(n)
```

Extra space:

```text
O(1)
```

---

# 4.15 Why Rotation Works

Original:

```text
[A | B]
```

where:

```text
A = [1, 2, 3, 4]
B = [5, 6, 7]
```

Desired:

```text
[B | A]
```

Reverse all:

```text
reverse(A + B)
=
reverse(B) + reverse(A)
```

Then reverse each section:

```text
B + A
```

So the reverse trick converts:

```text
[A | B]
```

into:

```text
[B | A]
```

This is a reusable transformation idea.

---

# 4.16 Partition

Partition means:

> Divide elements into groups based on a condition.

Example:

```text
[2, 7, 4, 9, 6, 3]
```

Put evens first:

```text
[2, 6, 4 | 9, 7, 3]
```

The internal order may or may not matter.

This distinction is critical.

Ask:

> **Does the problem require stable order?**

If no:

```text
swap-based partition
```

is often possible.

If yes:

```text
overwrite / extra storage / careful movement
```

may be needed.

---

# 4.17 Two-Pointer Partition

Use:

```text
left = 0
right = n - 1
```

Goal:

```text
[left side = valid group | right side = other group]
```

Example: negatives on left, positives on right.

Move `left` until finding a misplaced positive.

Move `right` until finding a misplaced negative.

Then:

```text
swap
```

Repeat.

The important idea:

> **Pointers search for elements that are on the wrong side of the partition.**

---

# 4.18 Rearrange Positives and Negatives

This problem has multiple versions.

### Version 1

Only require:

```text
negatives first
positives after
```

Order doesn't matter.

Use partitioning.

### Version 2

Require alternating:

```text
positive, negative, positive, negative
```

This is much more difficult.

### Version 3

Require alternating **and preserve relative order**.

Now stability matters, and the solution may need additional constraints or extra space.

Lesson:

> **The exact transformation requirement determines the pattern.**

Don't memorize:

```text
positives/negatives → use two pointers
```

Instead ask:

```text
What final arrangement is required?
Is order important?
Can I overwrite?
Can I swap?
What invariant should the processed region satisfy?
```

---

# 4.19 Sort Colors

Classic example:

```text
[2, 0, 2, 1, 1, 0]
```

Sort values:

```text
0, 1, 2
```

Expected:

```text
[0, 0, 1, 1, 2, 2]
```

Use three pointers:

```text
low
mid
high
```

Maintain:

```text
[ 0s | 1s | unknown | 2s ]
       ↑
      mid
```

More precisely:

```text
[0 ... low-1]       = 0
[low ... mid-1]     = 1
[mid ... high]      = unknown
[high+1 ... n-1]    = 2
```

Now process `arr[mid]`.

### If `0`

Swap with `low`.

```text
low++
mid++
```

### If `1`

Already in correct middle region.

```text
mid++
```

### If `2`

Swap with `high`.

```text
high--
```

Do **not** immediately increment `mid`.

Why?

Because the value swapped from `high` is still unknown and must be processed.

This is a very important pointer rule.

---

# 4.20 Sort Colors Invariant

At all times:

```text
[ 0s | 1s | unknown | 2s ]
```

The algorithm ends when:

```text
mid > high
```

because:

```text
unknown region is empty
```

This is one of the clearest examples of the:

```text
[ processed | unprocessed ]
```

model.

---

# 4.21 The Different Types of In-Place Transformation

You should now distinguish these.

## Type 1 — Swap-Based

```text
swap(arr[i], arr[j])
```

Examples:

* Reverse
* Partition
* Sort Colors

---

## Type 2 — Read/Write Overwrite

```text
read → inspect
write → next correct position
```

Examples:

* Remove Element
* Remove Duplicates
* Move Zeroes

---

## Type 3 — Multi-Region Partition

```text
[ group A | group B | unknown | group C ]
```

Examples:

* Sort Colors
* Dutch National Flag
* Multi-category partitioning

---

## Type 4 — Segment Transformation

```text
[A | B]
```

Transform segments.

Examples:

* Rotate using reverse
* Reverse subarrays
* Rearrange blocks

---

# 4.22 Universal Questions for This Chapter

When you encounter an in-place array problem, ask:

### 1. What should the final array look like?

Not:

> What code should I write?

First define:

```text
Input  → Desired Arrangement
```

---

### 2. What part is already correct?

Can you maintain:

```text
[ correct | unknown ]
```

or:

```text
[group A | unknown | group B]
```

---

### 3. How do elements move?

Choose one:

```text
Swap?
Overwrite?
Shift?
Reverse?
Partition?
```

---

### 4. Is order important?

This is one of the biggest decision points.

```text
Order preserved?
        ↓
       Yes
        ↓
Need stable transformation
```

or:

```text
Order irrelevant?
        ↓
       Yes
        ↓
Swap-based partition may work
```

---

### 5. What does each pointer mean?

Never write:

```java
int i = 0;
int j = ...
```

without knowing what they represent.

For example:

```text
read  = current element being inspected
write = next valid position
```

or:

```text
left  = next position needing a left-group element
right = next position needing a right-group element
```

Pointer meaning is more important than pointer names.

---

# 4.23 Complexity

Most core in-place transformations:

| Problem              | Time | Extra Space |
| -------------------- | ---: | ----------: |
| Reverse              | O(n) |        O(1) |
| Rotate using reverse | O(n) |        O(1) |
| Remove Element       | O(n) |        O(1) |
| Move Zeroes          | O(n) |        O(1) |
| Remove Duplicates    | O(n) |        O(1) |
| Partition            | O(n) |        O(1) |
| Sort Colors          | O(n) |        O(1) |

---

# 4.24 Chapter 4 Recognition Signals

Think **In-Place Transformation** when the problem says:

* Modify the array
* Do it in-place
* `O(1)` extra space
* Rearrange elements
* Move elements
* Remove elements
* Reverse
* Rotate
* Partition
* Put all X together
* Separate elements based on a condition
* Return the new length
* Ignore elements after index `k`

Then ask:

> **What does the processed region guarantee?**

---

# 4.25 Chapter 4 Problem Learning Order

### Level 1 — Basic Operations

1. Swap two elements
2. Reverse array
3. Reverse a subarray
4. Swap adjacent elements

### Level 2 — Read/Write Pattern

5. Remove Element
6. Move Zeroes
7. Remove Duplicates from Sorted Array
8. Keep only elements satisfying a condition

### Level 3 — Segment Transformation

9. Rotate Array by `k`
10. Rotate left
11. Rotate right
12. Reverse segments

### Level 4 — Partitioning

13. Move negatives to one side
14. Move even/odd elements
15. Partition around a value
16. Separate positives and negatives

### Level 5 — Multi-Region

17. Sort Colors
18. Dutch National Flag
19. Partition three categories

### Level 6 — Mixed Problems

20. Rearrange based on multiple constraints
21. Stable vs unstable rearrangement
22. In-place transformation with return length
23. Reverse + partition
24. Rotation + validation

---

# 4.26 Mastery Checklist

Before leaving this chapter, you should confidently understand:

### Core Operations

* What is swapping?
* What is shifting?
* What is overwriting?
* When is shifting expensive?

### Read/Write

* Why do we need two pointers?
* What does `read` represent?
* What does `write` represent?
* What invariant does the valid prefix satisfy?

### Logical Deletion

* Why can't we physically shrink a Java array?
* Why do we return a new length?
* Which part of the array should the caller consider valid?

### Stability

* What does preserving relative order mean?
* When is swap-based partition unsafe?

### Reverse/Rotate

* Why does reverse work in `O(n)`?
* Why does the three-reversal rotation trick work?

### Partitioning

* What group does each region represent?
* When is order irrelevant?
* How do we find misplaced elements?

### Sort Colors

Can you write and explain:

```text
[0s | 1s | unknown | 2s]
```

and explain exactly why `mid` doesn't move after handling `2`?

---

# Final Mental Model

Chapter 4 is not about memorizing:

```text
Reverse → two pointers
Move Zeroes → read/write
Sort Colors → three pointers
```

The deeper model is:

> **Modify the array while maintaining regions with clearly defined meanings.**

Every problem becomes:

```text
What should the final arrangement be?
          ↓
What region is already correct?
          ↓
What region is still unknown?
          ↓
How should the current element move?
          ↓
Swap / Overwrite / Shift / Partition
          ↓
Expand the correct region
```

The single most important invariant for this chapter is:

> **At every step, I know exactly what property the processed region satisfies.**

Once you can design and maintain that invariant, **in-place array transformation problems become much easier to recognize and solve**.
