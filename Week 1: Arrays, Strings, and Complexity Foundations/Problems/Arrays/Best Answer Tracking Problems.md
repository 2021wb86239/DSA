# Chapter 2 — Best Answer Tracking Cheat Sheet
    1. First ask these 5 questions
    Whenever you get an array optimization problem, ask:
    ```text
    1. What exactly am I trying to find?
        The largest element in the array.
    2. What is the "best" candidate so far?
        The largest element I have seen so far.
    3. What information from the past do I actually need?
        Only the largest value seen so far.
        I don't need all previous elements.
    4. Can I store that information in 1–3 variables?
        Yes. One variable is enough."best"
    5. After processing arr[i], what should my state mean?
        best = maximum value among arr[0...i].
    ```

## Level 1 — Pure Best Tracking
### Find largest element
    ```
    1. finding largest element in the array
    2. best refers the largest among processed elements
    3. bestSoFar
    4. yes
    5. it should be the largest element from arr[0..i]
    ```
    Pattern: Best Answer Tracking, since we are maintaing best so far from the processed elements.
    State: bestSoFar
    State Transition: bestSoFar = Math.max(bestSoFar, CurrentElement)
    Algorithm:
    ```text
    bestsoFar = arr[0];
    for each element i:
        bestSoFar = Math.max(bestSoFar, arr[i])
    return bestSoFar
    ```
    Time: O(n)
    Space: O(1)
#### Find smallest element
    State: bestSoFar
    State Transition: bestSoFar = Math.min(bestSoFar, currentElement)
    Algorithm:
    ```text
    bestSofar = arr[0]
    for each element i:
        bestSoFar = Math.min(bestSoFar, currentElement)
    return bestSoFar
    ```
#### Find maximum positive value
    State: bestSoFar
    State Transition: check if arr[i]>0, then Math.max(bestSofar, currentelement)
    Algorithm:
    ```text
    bestSoFar = arr[0]
    for each element i:
        if(arr[i] > 0)
            bestSoFar = Math.max(bestSoFar, arr[i])
    return bestSoFar
    ```
#### Find minimum negative value
    State: bestSoFar
    State Transition: check if arr[i]<0, then Math.min(bestSofar, currentelement)
    Algorithm:
    ```text
    bestSoFar = arr[0]
    for each element i:
        if(arr[i] < 0)
            bestSoFar = Math.min(bestSoFar, arr[i])
    return bestSoFar
    ```
#### Find maximum index
    State: bestSoFar
    State Transition: if arr[i]> bestsofar, then bestsofar = i
    Algorithm:
    ```text
    bestSoFar = arr[0]
    for each element i:
        if(arr[i] > bestsofar)
            bestSoFar = i
    return bestSoFar
    ```
#### Find minimum index
    State: bestSoFar
    State Transition: if arr[i]< bestsofar, then bestsofar = i
    Algorithm:
    ```text
    bestSoFar = arr[0]
    for each element i:
        if(arr[i] < bestsofar)
            bestSoFar = i
    return bestSoFar
    ```
#### Find largest even number
    State: bestSoFar
    State Transition: check if arr[i]%2 ==0, then bestsofar = Math.max(bestSofar, currentelement)
    Algorithm:
    ```text
    bestSoFar = arr[0]
    for each element i:
        if(arr[i]%2 == 0)
            bestSoFar = Math.max(bestSoFar, arr[i])
    return bestSoFar
    ```
#### Find smallest odd number
    State: bestSoFar
    State Transition: check if arr[i]%2 !=0, then bestsofar = Math.max(bestSofar, currentelement)
    Algorithm:
    ```text
    bestSoFar = arr[0]
    for each element i:
        if(arr[i]%2 != 0)
            bestSoFar = Math.min(bestSoFar, arr[i])
    return bestSoFar
    ```
## Level 2 — Running Best
### Running maximum
    ```
    1. finding largest element for current element i
    2. best refers the largest among processed elements
    3. bestSoFar
    4. yes
    5. it should be the largest element from arr[0..i]
    ```
    Pattern: Best Answer Tracking, since we are maintaing best so far from the processed elements.
    State: bestSoFar
    State Transition: bestSoFar = Math.max(bestSoFar, CurrentElement)
    Algorithm:
    ```text
    bestsoFar = arr[0];
    for each element i:
        bestSoFar = Math.max(bestSoFar, arr[i])
        arr[i] = bestSofar
    return arr;
    ```
    Time: O(n)
    Space: O(1)
#### Running minimum
    State: bestSoFar
    State Transition: bestsofar = Math.max(bestSofar, currentelement)
    Algorithm:
    ```text
    bestSoFar = arr[0]
    for each element i:
        bestSoFar = Math.min(bestSoFar, arr[i])
        arr[i] = bestSoFar
    return bestSoFar
    ```
#### Prefix maximum
    the distinction is prefix stores entire history for arr[i] = max(0..i) in case of running max the history is erased as soon as we find new max.
    Same logic as running max
    State: 
    State Transition:
    Algorithm:
#### Prefix minimum
    the distinction is prefix stores entire history for arr[i] = min(0..i) in case of running min the history is erased as soon as we find new min.
    State:
    State Transition:
    Algorithm:
#### Count how many times a new maximum appears
    State: bestsofar, count
    State Transition: if(arr[i] > bestsofar) the bestsofar = arr[i], count +=1
    Algorithm:
    ```text
    bestsofar = arr[0]
    count = 0
    for each element i:
        if(arr[i] > bestsofar)
            bestsofar = arr[i]
            count+=1
    return count;
    ```
#### Count how many times a new minimum appears
    State: bestsofar, count
    State Transition: if(arr[i] < bestsofar) the bestsofar = arr[i], count +=1
    Algorithm:
    ```text
    bestsofar = arr[0]
    count = 0
    for each element i:
        if(arr[i] < bestsofar)
            bestsofar = arr[i]
            count+=1
    return count;
    ```
## Level 3 — Multiple Best Values
### Second largest
    ```
    1. finding the second largest value
    2. the second largest element i have seen so far
    3. largest and second largest value i have seen so far
    4. yes, largest and secondLargest
    5. secondLargest = secondlargest value among arr[0..i]
    ```
    Pattern: Best Answer Tracking, since we are maintaing best so far from the processed elements.
    State: bestSoFar
    State Transition: when we find arr[i] > largest(new largest) then secondLargest = largest
    Algorithm:
    ```text
    largest = arr[0]
    secondLargest = Integer.MIN;
    for each element i:
        if arr[i] >= largest:
            secondLargest = largest;
            largest = arr[i]
        else if arr[i] >= secondLargest && arr[i] < largest
            secondLargest = arr[i]
    return secondLargest;
    ```
    Time: O(n)
    Space: O(1)
#### Second smallest
    State: smallest, secondSmallest
    State Transition: when we find arr[i]<smallest (new smallest) the secondSmallest = arr[i]
    Algorithm:
    ```text
    smallest = arr[0]
    secondSmallest = Integer.Max
    for each element i:
        if arr[i] < smallest:
            secondSmallest = smallest;
            smallest = arr[i];
        else if arr[i]<secondSmallest && arr[i] >smallest
            secondSmallest = smallest;
    ```
#### Second largest distinct
    the above code will handle the distinct.
    State: 
    State Transition:
    Algorithm:
#### Second smallest distinct
    the above code will handle the distinct
    State: 
    State Transition:
    Algorithm:
#### Largest and second largest together
    prviously return alorithm does that.
    State: 
    State Transition:
    Algorithm:
#### Smallest and second smallest together
    State: 
    State Transition:
    Algorithm:
## Level 4 — Best Candidate
### Index of maximum
    Pattern: Best Answer Tracking, since we are maintaing best so far from the processed elements.
    State: bestSoFar
    State Transition: when we find arr[i] > largest(new largest) then secondLargest = largest
    Algorithm:
    ```text
    largest = arr[0]
    secondLargest = Integer.MIN;
    for each element i:
        if arr[i] >= largest:
            secondLargest = largest;
            largest = arr[i]
        else if arr[i] >= secondLargest && arr[i] < largest
            secondLargest = arr[i]
    return secondLargest;
    ```
    Time: O(n)
    Space: O(1)
#### Element with maximum frequency/value according to a criterion
#### Best student/candidate based on score
    Similar to max algorithm here we tract the best student based on score.
#### Best candidate satisfying a condition
    similar to above, but based on a condition rather than score.
#### Best element according to a custom comparison
    similar to above, but based on custom comparison
## Level 5 — Best Previous Candidate
### Maximum difference
    ```
    1. the maximum difference between two numbers
    2. the max difference i have seen so far after between two elements
    3. i need the min and max, the max difference is between these elements.
    4. yes, min and max
    5. min = minimum value among arr[0..i] and max = maximum value among arr[0..i]
    ```
    Pattern: Best Answer Tracking, since we are maintaing min and max from the processed elements.
    State: bestSoFar
    State Transition: max = Math.max(max, CurrentElement), min = Math.min(min, current element)
    Algorithm: without ordering
    ```text
    minSoFar = arr[0]
    maxSoFar = arr[0]

    for each element i:
        minSoFar = min(minSoFar, arr[i])
        maxSoFar = max(maxSoFar, arr[i])

    return maxSoFar - minSoFar
    ```
    Time: O(n)
    Space: O(1)
#### Maximum difference with ordering
    Problem: find arr[j] - arr[i], where i<j that means i must appear before j. we need max diff in this case with diff = arr[i] - minSoFar
    State: bestDiff, minSoFar
    State Transition: for each element bestDiff = max(bestDiff, minSoFar), minsofar = min(minsofar, arr[i])
    Algorithm:
    ```
    minsofar = arr[0]
    bestdiff = 0

    for each element i:
        bestdiff = max(bestdiff, arr[i] - minsofar)
        minsofar = min(minsofar, arr[i])
    return bestdiff;
    ```
#### Minimum difference with ordering
    Similar to above but here we track maxsofar and best diff
#### Best time to buy and sell stock
    if you comparing it clearly this is nothing but maximum difference.
    you need buy before sell.
    profit = current price - cheapest previous buy price // calculate profit with available cheapest price
    bestprofit = max(profit, bestprofit) // choose best profix
    minbuyprice = min(price, minbuyprice) // update cheapest minimum buy price
#### Maximum profit with one transaction
#### Maximum arr[j] - arr[i] where i < j
    We solved it above.
## Level 6 — Variations
### Return indices instead of value
    Its same add one more state for index, when update other state update index state.
### Return the actual pair
    maintain 2 bestindexes state and update them when updating best values
### Handle duplicates
    Handled in previous algorithms
### Handle all-negative values
### Handle no valid second maximum
### Maximum difference with constraints
    This is also we handled.
### Maximum difference between elements at least K apart
    Problem: Given an array and integer K, find the maximum difference between two elements whose indices are at least K positions apart.
    |i - j| >= K
    arr[j] - arr[i]
    Input: arr = [1, 5, 3, 9], K = 2
    Output: 8
    State: bestDiff, bestdiffindex
    State Transition: if the current element is K position apart and its difference is greater than bestDiff, update the bestdiff.
    Algorithm:
    ```text
    minsofar = arr[0]
    bestdiffindex = 0
    bestdiff = ar[0]
    for each element i:
        if(Math.abs(bestdiffindex, i) >= k):
            bestdiffindex = i
            bestdiff = max(bestdiff, arr[i]-minsofar)
            minsofar = min(minsofar, arr[i])
    return bestdiff;

    ```