## Prequisites
Ask:
> Am I looking for one thing that proves TRUE, or one thing that proves FALSE?

# Algorithm Recipe — Chapter 3

---

## The Framework

For every problem, force yourself through this:

```
                 PROBLEM
                    ↓
        What exactly must be true?
                    ↓
           REQUIRED CONDITION
                    ↓
        What would make it false?
                    ↓
            VIOLATION CONDITION
                    ↓
       What information detects it?
                    ↓
                  STATE
                    ↓
       Choose simplest traversal
                    ↓
            Scan / pointers / set
                    ↓
          Violation found?
             ↙          ↘
           YES           NO
            ↓             ↓
       return false     continue
                           ↓
                       finished?
                           ↓
                      return true
```

---

## The One Question To Develop

Whenever you see a new validation problem, don't ask *"What algorithm is this?"* first.

**Ask:**

> "What is the **smallest piece of evidence** that can prove this is invalid?"

Then ask:

> "What is the **minimum state** I need to find that evidence?"

That will naturally lead you to:

| Pattern | State Needed |
|---------|--------------|
| Basic condition | Current element |
| Adjacent condition | Previous + current |
| Symmetric condition | Left + right |
| Uniqueness | HashSet |
| Multiple constraints | Combine violations |

---

## The Worksheet Template

For every problem, use this exact worksheet:

```
Problem #:
Name:

Question:
________________________________

What must be true?
________________________________

What makes it invalid?
Violation:
________________________________

Minimum state:
________________________________

Traversal:
________________________________

Early-exit condition:
________________________________

Java code:
________________________________

Time:
________________________________

Space:
________________________________

Why is this correct?
________________________________
```

> **Don't skip the "Violation" and "Minimum state" lines.** Those two are the actual learning; the Java code should become almost mechanical afterward.

---

## Example Walkthrough: Valid Parentheses (LeetCode 20)

### Problem #: 1
### Name: Valid Parentheses

**Question:**
Given a string containing `(`, `)`, `{`, `}`, `[`, `]`, determine if the input string is valid.

---

**What must be true?**
Every opening bracket must have a matching closing bracket in the correct order (LIFO).

**What makes it invalid?**
1. A closing bracket appears when no matching opening bracket is present
2. A closing bracket doesn't match the most recent unmatched opening bracket
3. There are unmatched opening brackets at the end

**Violation:**
```
closing bracket encountered AND 
(stack is empty OR top of stack != matching opening bracket)
```
OR
```
after scanning all characters, stack is not empty
```

**Minimum state:**
- A stack of opening brackets seen so far
- The current character being processed

**Traversal:**
Scan the string left to right, character by character.

**Early-exit condition:**
Return `false` immediately when a violation is detected.

**Java code:**
```java
public boolean isValid(String s) {
    Deque<Character> stack = new ArrayDeque<>();
    
    for (char c : s.toCharArray()) {
        if (c == '(' || c == '[' || c == '{') {
            stack.push(c);
        } else {
            if (stack.isEmpty()) return false;
            char top = stack.pop();
            if (!isMatching(top, c)) return false;
        }
    }
    return stack.isEmpty();
}

private boolean isMatching(char open, char close) {
    return (open == '(' && close == ')') ||
           (open == '[' && close == ']') ||
           (open == '{' && close == '}');
}
```

**Time:** O(n)
**Space:** O(n)

**Why is this correct?**
- Every closing bracket is matched against the most recent unmatched opening bracket (LIFO)
- If the stack is empty when a closing bracket appears, there's no opening bracket to match
- The `isMatching()` check ensures the correct pair
- The final `stack.isEmpty()` check ensures no unmatched openings remain

---

## The "What Is The Violation?" Pattern

For most validation problems, violations fall into these categories:

### 1. Boundary Violations
```
Question: "Is this value within range?"
Violation: value < min OR value > max
State: current value
```

### 2. Adjacent Violations
```
Question: "Are adjacent elements ordered?"
Violation: current <= previous (for strictly increasing)
State: previous + current
```

### 3. Symmetry Violations
```
Question: "Is this a palindrome?"
Violation: left character != right character
State: left index + right index
```

### 4. Uniqueness Violations
```
Question: "Are all elements unique?"
Violation: current value already seen
State: HashSet of seen values
```

### 5. Dependency Violations
```
Question: "Are dependencies satisfied?"
Violation: child appears before parent
State: Set of satisfied dependencies + current requirement
```

### 6. Structural Violations
```
Question: "Is the tree balanced?"
Violation: height difference > 1
State: current node height + left/right heights
```

---

## The "Minimum State" Question

Ask yourself:

> "If I were walking through the data once, what is the absolute minimum I need to remember?"

| Problem Type | Minimum State | Why |
|--------------|---------------|-----|
| **Current element condition** | Current value | Check it, move on |
| **Adjacent condition** | Previous value + current | Need both to compare |
| **Sliding window** | Window state + left/right pointers | Need to track window bounds |
| **Uniqueness check** | Set of seen values | Need to detect duplicates |
| **Parentheses** | Stack | Need LIFO matching |
| **Two-pointer** | Left pointer + right pointer | Need both ends |

---

## The "Traversal" Question

Ask yourself:

> "Which direction and order gives me the information I need?"

| Traversal | When to Use |
|-----------|-------------|
| **Left to right** | Checking current with past state |
| **Right to left** | Checking current with future state |
| **Two pointers from ends** | Symmetric conditions (palindrome) |
| **Two pointers from start** | Sliding window, two-sum |
| **BFS** | Level-order, shortest path |
| **DFS** | Path existence, depth-first properties |
| **Post-order** | Child before parent (tree balancing) |
| **In-order** | BST properties |

---

## The "Early-Exit" Question

Ask yourself:

> "Can I stop early, or do I need to see everything?"

| Condition | Early Exit? |
|-----------|-------------|
| **Validation** | ✅ Yes — return false on first violation |
| **Search** | ✅ Yes — return on first match |
| **Counting all violations** | ❌ No — need to count everything |
| **Processing all elements** | ❌ No — need to complete traversal |
| **Finding maximum** | ✅ Sometimes — can prune if impossible to beat |

---

## Practice: Fill in Your Own

### Problem #: ___
### Name: ________

**Question:**
________________________________

**What must be true?**
________________________________

**What makes it invalid?**
Violation:
________________________________

**Minimum state:**
________________________________

**Traversal:**
________________________________

**Early-exit condition:**
________________________________

**Java code:**
________________________________

**Time:** ___
**Space:** ___

**Why is this correct?**
________________________________

---

## The Mental Model

```
PROBLEM
   ↓
"What makes it invalid?" → VIOLATION
   ↓
"To detect that, what's the minimum state?" → STATE
   ↓
"How do I walk through to detect violations?" → TRAVERSAL
   ↓
"Can I stop early?" → EARLY-EXIT
   ↓
CODE
```

> **Remember**: The code is the easiest part. The thinking is:
> 1. **Violation** — what breaks the rule?
> 2. **State** — what do I need to remember?
> 3. **Traversal** — how do I step through?

Once you have those three, the code writes itself.

# Problems
## Level 1 — Basic Validation
### Check all elements are positive
Problem:
The problem is asking us to check if all the elements in the array are positive.
What must be true?
each element must be positive
What makes it invalid?
if any element is negative, this makes array invalid.
Violation: arr[i]<0

Minimum state: current element

Traversal: left to right

Early-exit condition:
if arr[i]< 0

Java code:
```java
for(int i = 0;i`<`n; i++){
    if(arr[i]<0)
        return false;
}
return true;
```

Time: O(n)

Space: O(1)

Why is this correct?

#### Check all elements are even
Problem: The problem is asking us to check if all elements in the array are even
What must be true?
each element must be even
What makes it invalid?
Violation: arr[i]%2 !=0

Minimum state: current element

Traversal: left to right

Early-exit condition: arr[i]%2 !=0

Java code:
```java
for(int i = 0;i`<`n; i++){
    if(arr[i]%2 !=0)
        return false;
}
return true;
```
Time: O(n)

Space: O(1)

Why is this correct?
#### Check array contains a target
Problem: The problem is asking about whether an array contains a target
What must be true?
the target must be there in the array

What makes it invalid?
Violation: if array doesn't contain the target

Minimum state: current element

Traversal: left to right

Early-exit condition: arr[i] == target

Java code:
```java
for(int i = 0;i`<`n; i++){
    if(arr[i] == target)
        return true;
}
return false;
```
Time: O(n)

Space: O(1)

Why is this correct?
#### Check array contains no negative
This is similar to <check all elements are positive.>
#### Check every element is within [L, R]
Problem: The problem is asking us to check if all elements in the array are within [L, R]
What must be true? 
each element in the array must be within [L,R]
What makes it invalid?
Violation: arr[i] < L || arr[i]>R

Minimum state: current element

Traversal: left to right

Early-exit condition: arr[i] < L || arr[i]>R

Java code:
```java
for(int i = 0;i`<`n; i++){
    if(arr[i] < L || arr[i]>R)
        return false;
}
return true;
```
Time: O(n)

Space: O(1)

Why is this correct?
## Level 2 — Ordering
### Check sorted
Problem: The problem is asking us to check if the array is in sorted order.

What must be true? each element should be greater equal to the previous element.

What makes it invalid?
Violation: current element is less than previous element

Minimum state: current element and previous element

Traversal: left to right

Early-exit condition: arr[i] <= arr[i-1]

Java code:

```java
for(int i = 1; i<n; i++){
    if(arr[i]<= arr[i-1])
        return false;
return true;
}
```

Time: O(n)

Space: O(1)

Why is this correct?
#### Check non-decreasing
Problem:
The problem is asking us to check if array is non-decreasing. meaning arr[i+1] must be greater than or equal to previous element arr[i]
What must be true?
arr[i+1] must be greater than or equal to previous element arr[i]
What makes it invalid?
if arr[i+1] is less than the arr[i]
Violation: arr[i] < arr[i-1]

Minimum state: previous and current element

Traversal: left to right

Early-exit condition: arr[i] < arr[i-1]

Java code:

```java
for(int i = 1; i<n; i++){
    if(arr[i] < arr[i-1]>)
        return false;
return true;
}
```

Time: O(n)

Space: O(1)

Why is this correct?
#### Check non-increasing
Problem: The problem is asking us to check if array elements are in non-increasing order. meaning the every next element must be less than or equal to previous one. current <= previous

What must be true?
current <= previous
What makes it invalid?
if current element is greater than previous element
Violation: arr[i] > arr[i-1]

Minimum state: current and previous element

Traversal: left to right

Early-exit condition: arr[i] > arr[i-1]

Java code:
```java
for(int i = 1; i<n; i++){
    if(arr[i]>arr[i-1])
        return false
return true
}
```

Time: O(n)

Space: O(1)

Why is this correct?
#### Check strictly increasing
Problem: The is asking us to check if all elements in the array are strictly increasing.

What must be true? current element must be greater than previous

What makes it invalid? current element <= previous element
Violation: arr[i]<= arr[i-1]

Minimum state: current and previous element

Traversal: left to right

Early-exit condition: arr[i] <= arr[i-1]

Why is this correct?
#### Check strictly decreasing
Problem: The problem is asking us to check if all elements in the array are strictly decreasing.

What must be true?
current element must be less than previous element

What makes it invalid? current element greater than equal to previous element

Violation: arr[i] >= arr[i-1]

Minimum state: current and previous element

Traversal: left to right

Early-exit condition: arr[i] >= arr[i-1]

Why is this correct?
## Level 3 — Structural Validation
### Check palindrome
Problem:

What must be true?

What makes it invalid?
Violation:

Minimum state:

Traversal:

Early-exit condition:

Java code:

Time:

Space:

Why is this correct?
#### Check symmetric array
#### Check alternating arrangement
#### Validate adjacent difference constraint
#### Validate a specific arrangement
## Level 4 — Uniqueness
### Check duplicates
Problem:
The problem is asking us to check if any element exists more 1 time.
What must be true? all elements in the array should be unique.

What makes it invalid? if any element exists more than once its invalid
Violation: element already exists

Minimum state: previous elements + current element

Traversal: left to right

Early-exit condition: element already exists

Java code:
```java
HashSet j = new Hashset
for(int i =0; i<n; i++){
    if(j.contains(arr[i]))
        return false;
    j.add(arr[i])
return true;
}
```

Time: O(n) + hasset contains(1) => O(n)

Space: O(1)

Why is this correct?
#### Check all elements distinct
Same as above.
#### Find whether any value occurs more than once
Similar to above.
f
Start with brute force, then optimize with hashing.
## Level 5 — Mixed Validation
### Sorted + unique
Problem:
The problem is asking us to check if all elements in the array are iin sorted order + unique elements. We don't need to check it in 2 pass. if we do for strictly increasning. The constraint works.
What must be true?
current element must be greater than previous element.
What makes it invalid?
current element <= previous element
Violation: arr[i] <= arr[i-1]

Minimum state: current element and previous element

Traversal: left to right

Early-exit condition: arr[i] <= arr[i-1]

Java code: similar to strictly increasing

Why is this correct?
#### Strictly increasing
we already solved this. in the above.

#### All values within range + unique
we have to store each seen element hashset for existence check.
for each element check if it satisfies range + hashset non existence then return true elase false.
check for violation
for each element check if any of the validation fails, either element is out of range or already exists
#### Validate arrangement with multiple constraints
#### Validate before performing another operation