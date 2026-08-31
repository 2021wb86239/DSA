#### Input:
#### Ouput:
#### Pattern:
#### Recognition Siganl:
#### State:
#### State Transition:
#### Invariant:
#### Algorithm:
#### Complexity:
#### - Time:
#### - Space:
## Level 1 — Pure Traversal
### Print all elements
#### Input:
    An array of size n
#### Ouput:
    print all elements to the console.
#### Pattern:
    Linear Traversal
#### Recognition Siganl:
    All, Since the problem mentioned `all` that mean we have to process all elements. So linear traversal makes sense.
#### State:
    No State to be maintained.
#### State Transition:
    No State Transition
#### Invariant:
    after processing an index i, the console has elements printed from [0..i]printed.
#### Algorithm:
    ```text
    for each element i:
        print arr[i]
    ```

#### Complexity:
#### - Time:
    Since we are accessing each element it's O(n)
#### - Space:
    We are not storing any value other than accessing an element so it's O(1)
### Print elements in reverse
#### Input:
    An array of size n
#### Ouput:
    print all elements to the console in reverse direction.
#### Pattern:
    Linear Traversal
#### Recognition Siganl:
    All, Since the problem mentioned `all` that mean we have to process all elements. So linear traversal makes sense.
#### State:
    No State to be maintained.
#### State Transition:
    No State Transition
#### Invariant:
    after processing an index i, the console has elements printed from [length-1..i] printed.
#### Algorithm:
    ```text
    for each element i in range(length-1, 0):
        print arr[i]
    ```

#### Complexity:
#### - Time:
    Since we are accessing each element it's O(n)
#### - Space:
    We are not storing any value other than accessing an element so it's O(1)
### Sum of array
#### Input:
    An array of size n
#### Ouput:
    return sum of all elements in the input array
#### Pattern:
    Linear Traversal
#### Recognition Siganl:
    Sum, Since the problem mentioned `sum of array` that mean we have to process all elements to do the sum. So linear traversal makes sense.
#### State:
    Sum
#### State Transition:
    after accessing each element, we update the sum by the accessed element.
#### Invariant:
    after processing an index i, sum stores sum of all elements from [0..i]
#### Algorithm:
    ```text
    sum =0;
    for each element i:
        do sum += arr[i];
    return sum;
    ```

#### Complexity:
#### - Time:
    Since we are accessing each element it's O(n)
#### - Space:
    Except the state variable We are not storing any value other than accessing an element so it's O(1)
### Count elements
#### Input:
    An array of size n
#### Ouput:
    return count of all elements in the input array.
#### Pattern:
    Linear Traversal
#### Recognition Siganl:
    Count, Since the problem mentioned `count elements` that mean we have to process all elements to count. So linear traversal makes sense.
#### State:
    Count State to be maintained.
#### State Transition:
    After Each element Access, increase count state by 1.
#### Invariant:
    after processing an index i, count stores no of element from 0..i
#### Algorithm:
    ```text
    count = 0;
    for each element i:
        count +=1;
    return count;
    ```

#### Complexity:
#### - Time:
    Since we are accessing each element it's O(n)
#### - Space:
    Expect the count variable, We are not storing any value other than accessing an element so it's O(1)
### Count even numbers
#### Input:
    An array of size n
#### Ouput:
    return count of all even numbers in the input array.
#### Pattern:
    Linear Traversal
#### Recognition Siganl:
    Count, Since the problem mentioned `count even` that mean we have to process all elements to determine the even numbers in the input array. So linear traversal makes sense.
#### State:
    Count
#### State Transition:
    After Accessing each element arr[i], check if arr[i]%2 ==0 if yes increase count by 1.
#### Invariant:
    after processing an index i, count stores number of even numbers from [0..i]
#### Algorithm:
    ```text
    count = 0;
    for each element i:
        if arr[i]%2 == 0;
            count +=1;
    return count
    ```

#### Complexity:
#### - Time:
    Since we are accessing each element it's O(n)
#### - Space:
    Except Count varaible, We are not storing any value other than accessing an element so it's O(1)
### Count odd numbers
#### Input:
    An array of size n
#### Ouput:
    return count of all odd numbers in the input array.
#### Pattern:
    Linear Traversal
#### Recognition Siganl:
    Count, Since the problem mentioned `count odd` that mean we have to process all elements to determine the odd numbers in the input array. So linear traversal makes sense.
#### State:
    Count
#### State Transition:
    After Accessing each element arr[i], check if arr[i]%2 !=0 if yes increase count by 1.
#### Invariant:
    after processing an index i, count stores number of odd numbers from [0..i]
#### Algorithm:
    ```text
    count = 0;
    for each element i:
        if arr[i]%2 != 0;
            count +=1;
    return count
    ```

#### Complexity:
#### - Time:
    Since we are accessing each element it's O(n)
#### - Space:
    Except Count varaible, We are not storing any value other than accessing an element so it's O(1)
### Count positive numbers
#### Input:
    An array of size n
#### Ouput:
    return count of all positive numbers in the input array.
#### Pattern:
    Linear Traversal
#### Recognition Siganl:
    Count, Since the problem mentioned `count positive` that mean we have to process all elements to determine the positive numbers in the input array. So linear traversal makes sense.
#### State:
    Count
#### State Transition:
    After Accessing each element arr[i], check if arr[i]>=0 if yes increase count by 1.
#### Invariant:
    after processing an index i, count stores number of posivite numbers from [0..i]
#### Algorithm:
    ```text
    count = 0;
    for each element i:
        if arr[i] >= 0;
            count +=1;
    return count
    ```

#### Complexity:
#### - Time:
    Since we are accessing each element it's O(n)
#### - Space:
    Except Count varaible, We are not storing any value other than accessing an element so it's O(1)
### Count negative numbers
#### Input:
    An array of size n
#### Ouput:
    return count of all negative numbers in the input array.
#### Pattern:
    Linear Traversal
#### Recognition Siganl:
    Count, Since the problem mentioned `count negative` that mean we have to process all elements to determine the negative numbers in the input array. So linear traversal makes sense.
#### State:
    Count
#### State Transition:
    After Accessing each element arr[i], check if arr[i]<0 if yes increase count by 1.
#### Invariant:
    after processing an index i, count store number of negative numbers count from [0..i]
#### Algorithm:
    ```text
    count = 0;
    for each element i:
        if arr[i]< 0;
            count +=1;
    return count
    ```

#### Complexity:
#### - Time:
    Since we are accessing each element it's O(n)
#### - Space:
    Except Count varaible, We are not storing any value other than accessing an element so it's O(1)

## Level 2 — Aggregation
### Find largest element
#### Input:
    An array of size n
#### Ouput:
    return the largest element from the input array.
#### Pattern:
    Linear Traversal
#### Recognition Siganl:
    Find, Since the problem mentioned `Find` that mean we have to process all elements to determine the largest number from the input array. So linear traversal makes sense.
#### State:
    maxSoFar
#### State Transition:
    After Accessing each element arr[i], check if arr[i]>maxSoFar if yes update maxSofar with arr[i].
#### Invariant:
    after processing an index i, maxSoFar stores largest number from [0..i]
#### Algorithm:
    ```text
    maxSoFar = 0;
    for each element i:
        if arr[i]>maxSoFar;
            maxSoFar = arr[i];
    return maxSoFar;
    ```

#### Complexity:
#### - Time:
    Since we are accessing each element it's O(n)
#### - Space:
    Except maxSoFar varaible, We are not storing any value other than accessing an element so it's O(1)
#### Variations
##### Find smallest element
    State is `minSoFar`, condition & state transistion is if update minSoFar if `arr[i]<minSoFar`, 
##### Find average
    State is `average`, state transitioin access each element and update average. end of the loop in the return statement do average/array length.
##### Find sum of positive elements
    State is `sum`, state transition is updating the sum if the current element is positive(arr[i]>0).
##### Find sum of negative elements
    State is `sum`, state transition is updating the sum if the current element is negative(arr[i]<0).
##### Find maximum positive number
    State is `maxPositive`, state transition is updating the maxPositive if the current element is positive(arr[i]>0 && arr[i] > maxPositive).
##### Find minimum negative number
    State is `minNegative`, state transition is updating the minNegative if the current element is negative and less than minNegative(arr[i]>0 && arr[i] > maxPositive).

## Level 3 — Validation
### Check if any element is negative
#### Input:
    An array of size n
#### Ouput:
    return true if array contains at least one negative element otherwise return false;
#### Pattern:
    Linear Traversal
#### Recognition Siganl:
    Early Termination, The word any signals that we can stop as soon as a violating element is found. We may need to inspect the entire array if no negative element exists, so this uses linear traversal with early termination.
#### State:
    No State is required.
#### State Transition:
    After Accessing each element arr[i], check for violation arr[i]<0 if yes  return true. else process rest of the elements.
#### Invariant:
    After processing indices [0..i] without returning, no negative element exists in [0..i].
#### Algorithm:
    ```text
    for each element i:
        if arr[i]<0;
            return true;
    return false;
    ```

#### Complexity:
#### - Time:
    Since we are accessing each element it's O(n)
#### - Space:
    Except loop varaible, We are not storing any value other than accessing an element so it's O(1)
### Variations
#### Check if all elements are positive
    State checkNegitive, 
    state transition: is at each index i check for condition violation. if it breaks, then return false. at the end of loop return true if no element breaks condition., 
    Pattern: Condition Violation
    Invariant: After processing [0..i] without returning, every element in [0..i] is strictly positive.
#### Check if array contains X
    State: found
    State Transition: at each index i check if arr[i] is X 
    Pattern: Early Termination, because if we find the x before the end of the array we terminate loop early.
    Algorithm: at each index i check if arr[i] is x, if yes return true, else continue processing, at the end of the return false;
    Invariant: After processing [0..i], the found stores whether it found the x from [0..i]
#### Find first occurrence of X
    State: No State
    State Transition: No State Transition is required.
    Pattern: Early Termination, once we found x, we return immediately without processing next elements.
    Algorithm: at each index i check if the current element is x if yes return index immediately else keep looking at remaining elements.
    Invariant: If the loop continues after processing [0..i], then X does not occur in [0..i].
#### Find last occurrence of X
    State: No State
    State Transition: No State Transition is required.
    Pattern: Reverse linear traversal + Early Termination, once we found x, we return immediately without processing next elements.
    Algorithm: here we need to find the last occurence, so we start search from last index of the array. that is the key learning here.
    Invariant: after processing index i, we didn't find the occurence from [length-1..i]

## Level 4 — Transformation
### Multiply every element by 2
#### Input:
    An array of size n
#### Ouput:
    return an array of size n with each index value multiplied by 2.
#### Pattern:
    In-Place Transformation + Forward Traversal. 
#### Recognition Siganl:
    Linear Traversal, The words `every element` signals that we need to vist every element and multiply each suggest that In-Transformation.
#### State: 
    The same Input array we use for Transforming and returning the multiplied array.
#### State Transition:
    At each index we access the element and multiply the element by 2 and update the index value to updated value.
#### Invariant:
    After processing indices [0..i], each index i element is multiplied by 2.
#### Algorithm:
    Loop through the array, access each index element store it in temp variable and mulitply it by 2, then update the value at the same index.
#### Complexity:
#### - Time:
    We are visiting the every element in the array, it's O(n)
#### - Space:
    Since we are doing In-Place transformation we don't need extra memory, and few temp variables. so its O(1).
### Replace negative numbers with 0
    State: No state required
    State Transition: no state required
    Pattern: In-Place Tranformation + Forward Traversal
    Invariant: After processing indices [0..i], any index element negative is replaced with 0
### Increment every element
    Problem: 
    State: 
    State Transition:
    Pattern:
    Invariant:
### Square every element
    Problem: square every element in the array
    State: No State required
    State Transition: No State required
    Pattern: In-Place Tranformation + forward Traversal
    Invariant: After processing indices [0..i], the array contains the squares at each index i 
### Replace even numbers with 0
    Problem: Replace every even number with 0 in the array
    State: No state required
    State Transition: no state required
    Pattern: In-Place Tranformation + Forward Traversal
    Invariant: After processing indices [0..i], the array contains even numbers replace with 0

## Level 5 — Multiple State
### Find min and max together
    Problem: return the min and max of a array
    State: min and max
    State Transition: at each index i, check current element with min and max and update the state
    Pattern: Maintain Multi-State + Forward Traversal
    Invariant: After processing indices [0..i], the min and max stores value from [0..i]
### Find sum and count together
    Problem: return the sum all elements and count of a X or condition?
    State: sum and count
    State Transition: At each index i, update the sum and count state
    Pattern: Multi State + Forward Traversal.
    Invariant: After processing indices [0..i], the sum and count has a sum of elements from indices [0..i]
### Find min, max and sum
    Problem: return min, max and sum of an array of size n
    State: min, max, and sum
    State Transition: At each index i, update the min, max and sum state
    Pattern: Multi State + Forward Traversal
    Invariant: After processing indices [0..i], the min, max and sum state has values from indices [0..i]
### Count positive and negative numbers
    Problem: return number of positive and negative numbers from the given array
    State: count
    State Transition: At each index i, determine current element is +ve or -ve, update state accordingly
    Pattern: Multi State + Forward Traversal
    Invariant: After processing indices [0..i], the count contains no of positive and negative number count from indices [0..i]
### Find min, max, sum and average
    Problem: return min, max, sum and average of an array of size n
    State: min, max, sum and average
    State Transition: At each index i, determine current min, max, sum and average and update the state
    Pattern: Multi State + Forward Traversal
    Invariant: After processing indices [0..1], the min, max, sum and average of indices from [0..1]

## Level 6 — Early Termination
### Does any element satisfy condition X?
    Problem: return true if any element satisfies condition x
    State: No State required
    State Transition: No State Required
    Pattern: Early Termination  +  Forward Traversal.
    Invariant: After processing each indices [0..i], the indices from [0..i] did not satisfy the condition X.
### Do all elements satisfy condition X?
    Problem: return true if all elements in the array satisfy condition x
    State: No State
    State Transition: No State Required
    Algorithm: visit each element, check negate condition x and return false if it satisfies.
    Pattern: Early Termination + Forward Traversal.
    Invariant: After processing indices [0..1], the indices did not satisfy the condition x.
### Find first element satisfying condition X
    Problem: return first element satisfying condition x
    State: No State required
    State Transition: no state required
    Pattern: Early Termination + forward Traversal.
    Invariant: After processing indices [0..1], the indices did the satisfy the condition x.
### Check whether target exists
    Problem: return true if the target exists in the array, otherwise return false.
    State: No State Required
    State Transition: No State Required
    Pattern: Early Termination + Forward Traversal
    Invariant: After processing indices [0..1], the target did not exist in the indices [0..1]
### Check whether array contains duplicate using only nested traversal first -- then later revisit with Hashing.
    Problem: return true if the array contains duplicate
    State: No State
    State Transition: No State Required
    Pattern: Early Termination + Forward Traversal
    Invariant: After processing indices [0..i], the indices[0..1] didn't have duplicate.