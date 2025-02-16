# Maximum Product Subarray

###### Made by [Rishi Sheth](https://github.com/RishiASheth)

## Problem Statement
Given an integer array nums, find the contiguous subarray within the array (containing at least one number) that has the largest product and return the product.

---

## Input Format
- The first line contains an integer N, the size of the array.
- The second line contains N space-separated integers, the elements of the array.

---

## Constraints
- 1 ≤ 𝑁 ≤ 10^5
- −10 ≤ nums[i] ≤ 10

---

## Output Format
- A single integer, the maximum product of a contiguous subarray.

---

## Test Cases

1. **Input:**
```
6
2 3 -2 4 -1 -3
```

1.   **Output:**  
```
48
```
---

2. **Input:**
```
5  
-2 0 -1 5 2  

```

2.   **Output:**  
```
10
```

---

3. **Input:**
```
1
-5
```

3.   **Output:**  
```
-5
```

4. **Input:**
```
4
0 -2 -3 0
```

4.   **Output:**  
```
6
```

## Solution

### Pseudocode
Define function maxProduct(nums):
    1. If nums is empty, return 0.
    2. Initialize `max_so_far = nums[0]`, `curr_max = nums[0]`, and `curr_min = nums[0]`.
    3. Iterate over nums from index 1 to len(nums) - 1:
        a. Store `curr` as nums[i].
        b. Calculate `temp_max = max(curr, curr_max * curr, curr_min * curr)`.
        c. Update `curr_min = min(curr, curr_max * curr, curr_min * curr)`.
        d. Update `curr_max = temp_max`.
        e. Update `max_so_far = max(max_so_far, curr_max)`.
    4. Return `max_so_far`.


---

## Implementation

```py
def maxProduct(nums):
    if not nums:
        return 0

    max_so_far = nums[0]
    curr_max = nums[0]
    curr_min = nums[0]

    for i in range(1, len(nums)):
        curr = nums[i]
        temp_max = max(curr, curr_max * curr, curr_min * curr)
        curr_min = min(curr, curr_max * curr, curr_min * curr)
        curr_max = temp_max

        max_so_far = max(max_so_far, curr_max)

    return max_so_far
input()
nums = list(map(int, input().split()))
print(maxProduct(nums))
```