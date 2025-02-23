# K-th Smallest Subarray Product

###### Made by [Angad](https://github.com/Anga205)

## Problem Statement

Given an array `A` of `N` positive integers, find the `K`-th smallest product formed by any contiguous palindromic subarray of length greater than or equal to `M`.

A subarray is a contiguous sequence of elements from the array. The product of a subarray is the product of all its elements.

A palindromic subarray is a subarray that reads the same forward and backward. For example, in the array `[1, 2, 3, 2, 1]`, the subarray `[2, 3, 2]` is palindromic because it reads the same in both directions.

## Input Format

- The first line an integer `N`
- The first line an integer `K`
- The first line an integer `M`
- The fourth line contains N space-separated positive integers (array `A`)

## Constraints

- All array elements are positive integers.
- Consider all contiguous subarrays of length at least M.
- (1 ≤ `A[i]` ≤ 10<sup>4</sup>)
- (1 ≤ `M` ≤ `N` ≤ 10<sup>5</sup>)
- (1 ≤ `K` ≤ `N` * (`N` + 1) / 2)

## Output Format

- A single integer representing the K-th smallest product among all palandromic subarrays.


## Sample Test Cases

### Test Case 1

#### Input

```
100
3
5
9 9 0 8 1 5 8 4 6 4 7 7 4 3 0 5 9 6 4 4 8 3 2 6 8 3 3 8 7 7 5 3 8 8 5 6 3 6 4 1 7 7 9 6 6 1 1 1 7 4 2 4 2 3 5 8 8 4 4 8 8 6 3 6 1 9 8 3 0 1 4 9 8 2 8 9 5 3 5 0 2 8 0 1 6 5 5 8 6 5 7 7 7 5 7 1 3 6 9 3
```

#### Output

```
65536
```

#### Explanation

1. The value of `N` is 100, so the length of array `A` is 100.
2. The value of `K` is 3, meaning we need to find the 3rd smallest product.
3. The value of `M` is 5, so we consider all palindromic subarrays of length at least 5.
4. The array `A` is given as:
    ```
    [9, 9, 0, 8, 1, 5, 8, 4, 6, 4, 7, 7, 4, 3, 0, 5, 9, 6, 4, 4, 8, 3, 2, 6, 8, 3, 3, 8, 7, 7, 5, 3, 8, 8, 5, 6, 3, 6, 4, 1, 7, 7, 9, 6, 6, 1, 1, 1, 7, 4, 2, 4, 2, 3, 5, 8, 8, 4, 4, 8, 8, 6, 3, 6, 1, 9, 8, 3, 0, 1, 4, 9, 8, 2, 8, 9, 5, 3, 5, 0, 2, 8, 0, 1, 6, 5, 5, 8, 6, 5, 7, 7, 7, 5, 7, 1, 3, 6, 9, 3]
    ```
5. On parsing this array, we find that these are the valid palindromic subarrays with length greater than or equal to 5:
```
3 6 9 3
8 8 4 4 8 8 
9 8 2 8 9 
5 7 7 7 5
```
their products are:
```
489
65536
10368
8575
```
Clearly, the 3rd smallest product here is `65536`, so we print it.

### Test Case 2

#### Input

```
100
5
3
1 1 8 6 5 0 9 0 4 0 6 2 1 6 5 4 0 9 8 3 1 5 4 4 9 8 5 0 5 5 7 7 9 3 4 2 1 6 4 5 2 4 7 0 4 2 5 3 8 9 3 3 2 5 5 7 9 0 3 4 9 4 4 5 3 1 4 6 3 8 3 3 7 3 9 9 9 6 1 1 9 3 2 6 6 8 9 2 9 2 5 6 9 7 5 7 6 7 0 4
```

#### Output

```
144
```

### Test Case 3

#### Input

```
150
2
4
1 8 3 6 7 3 6 9 4 9 6 9 5 8 2 9 5 4 4 6 8 0 6 7 0 9 5 6 4 3 9 6 9 7 3 8 9 0 9 9 6 1 6 3 2 1 4 1 9 6 6 4 9 8 7 0 9 1 7 0 4 0 4 4 2 8 5 5 3 8 0 7 8 8 9 3 7 2 3 4 3 3 3 4 6 1 6 7 0 1 1 1 7 3 1 6 6 6 1 6 9 5 0 3 7 8 3 2 2 1 7 6 3 8 8 3 4 5 7 3 9 2 9 4 2 4 1 6 9 8 4 6 2 1 4 7 1 0 6 2 0 1 8 7 6 0 7 9 4 1
```

#### Output

```
432
```

### Test Case 4

#### Input

```
300
6
3
8 2 9 0 7 7 3 6 4 5 9 7 4 8 6 4 1 3 1 0 0 8 9 6 5 0 2 7 7 5 3 0 8 3 7 1 9 9 7 9 1 9 7 0 1 7 9 9 8 0 9 2 5 5 1 5 1 2 4 3 2 1 4 8 8 2 3 3 5 6 7 5 9 7 0 2 8 9 2 6 7 0 1 6 2 8 7 4 8 5 4 7 9 8 3 1 7 7 7 4 2 5 7 0 8 7 7 6 0 6 1 4 3 2 3 2 1 6 7 2 5 1 8 5 8 1 7 6 5 4 4 3 5 5 3 8 9 4 5 6 0 9 5 2 9 8 1 0 8 9 0 8 6 0 2 6 4 1 7 8 1 6 7 2 9 4 2 0 3 5 2 5 8 8 1 6 7 8 2 9 7 5 6 2 1 5 3 9 4 3 2 4 6 5 0 1 2 8 9 8 9 1 7 3 6 5 4 5 4 4 1 9 6 4 2 3 5 0 4 4 5 5 6 8 8 5 9 3 0 1 4 8 5 8 6 1 6 2 5 5 8 6 0 7 7 7 1 4 9 2 3 9 1 4 9 7 9 5 2 9 3 1 6 6 7 2 9 4 3 6 0 9 0 1 6 8 8 1 3 6 8 2 7 5 9 8 1 1 1 3 1 0 4 9 3 9 1 3 1 3
```

#### Output

```
12
```

### Test Case 5

#### Input

```
500
5
5
0 9 9 8 2 2 4 2 9 3 8 6 1 7 8 3 7 1 9 9 9 8 2 7 4 9 7 7 2 8 0 6 5 6 3 5 3 1 5 9 6 6 4 7 3 2 6 7 2 1 5 7 5 6 4 2 0 9 6 3 2 6 9 2 3 2 1 4 7 9 9 7 7 1 3 7 1 7 4 0 6 8 7 8 2 7 3 7 2 8 9 3 2 5 9 1 5 5 2 8 4 2 6 1 7 0 5 0 4 6 0 6 6 3 3 8 1 7 5 1 2 0 6 4 2 5 7 7 0 4 7 1 1 3 1 0 0 0 1 0 0 4 7 0 8 5 5 9 8 7 5 3 8 0 4 0 0 1 7 2 9 3 6 4 8 7 6 3 6 5 9 3 2 9 8 9 2 6 1 9 1 1 0 3 1 7 5 3 5 6 3 3 9 3 3 1 8 6 5 3 6 7 8 8 9 0 0 9 5 3 7 2 2 6 8 0 0 7 9 1 8 5 1 6 1 1 1 2 5 4 3 2 5 6 6 2 4 2 7 0 8 6 6 8 3 0 3 5 5 9 3 6 2 7 4 6 6 7 4 1 0 3 0 9 1 0 2 3 0 9 5 1 3 2 7 8 5 1 7 7 6 4 5 9 5 2 0 5 9 5 3 3 6 1 1 5 8 5 5 7 2 7 2 9 7 6 7 2 9 0 2 7 2 4 7 2 4 3 6 5 6 3 6 3 2 1 7 9 9 0 3 3 2 9 3 1 8 8 1 7 4 7 7 2 3 8 7 2 1 7 4 8 7 6 4 0 5 2 1 8 4 3 6 7 5 1 5 9 8 9 0 6 5 4 8 3 2 4 7 3 9 9 0 6 2 2 6 0 0 7 6 2 0 5 3 4 6 0 5 6 0 8 4 5 4 4 3 6 6 6 1 4 3 4 9 6 7 5 9 8 8 9 5 0 8 6 5 2 7 9 6 0 2 4 5 3 3 3 4 7 3 9 3 4 9 3 0 3 7 2 1 9 6 7 6 9 0 2 6 4 1 9 3 1 1 4 7 7 5 5 0 8 2 8 1 2 4 6 1 4 2 0 7 2 4 6 6 7 1 7 1 3 3 1 5 3 0 2 2 5
```

#### Output

```
2592
```

### Test Case 6

#### Input

```
1000
3
5
0 4 6 7 8 8 7 6 4 1 7 2 9 8 3 0 3 0 3 6 7 5 3 2 7 9 8 4 6 2 9 8 5 7 7 6 7 5 3 4 9 1 6 7 1 3 4 1 4 3 5 4 1 3 0 2 3 5 8 5 1 8 9 3 5 1 5 6 3 2 3 9 9 2 3 1 8 5 3 5 3 3 0 8 6 5 2 9 8 9 4 4 4 6 2 3 0 7 5 8 4 9 5 7 2 6 1 1 5 3 9 4 4 5 8 5 4 2 6 7 8 4 1 7 7 1 5 5 0 4 1 3 9 7 1 2 9 2 7 4 7 7 7 9 2 9 4 2 4 4 0 0 1 9 7 1 9 6 6 6 9 7 0 5 6 6 5 8 2 1 0 9 5 2 6 3 3 0 8 3 5 8 6 9 4 2 2 7 5 2 6 5 6 9 1 8 9 3 3 9 3 3 8 4 1 4 6 2 1 7 6 8 1 1 3 3 5 9 9 8 4 2 0 1 1 9 6 2 1 4 6 1 0 0 7 9 0 9 3 3 8 8 3 5 5 6 5 2 4 1 8 7 5 6 7 3 4 9 8 5 6 3 5 7 2 9 5 9 7 6 5 1 5 8 7 2 8 6 5 4 4 9 4 4 7 5 6 4 8 7 1 8 1 8 3 1 6 8 7 9 0 7 6 0 1 4 3 6 7 8 3 8 7 5 4 8 0 0 6 1 7 3 4 3 8 9 3 4 6 0 8 6 5 0 2 0 8 7 0 2 0 9 7 7 6 9 9 0 5 4 3 0 7 8 5 2 0 1 0 5 6 9 2 1 5 1 8 9 2 4 1 7 9 0 7 1 0 9 7 4 0 6 5 4 9 1 2 7 2 5 7 7 2 4 6 5 1 7 8 7 9 8 7 2 6 7 3 5 0 0 6 4 5 8 3 0 4 7 9 3 1 1 5 1 4 2 8 0 2 9 1 1 7 0 7 8 9 2 5 2 0 4 6 7 3 1 9 3 0 2 4 5 6 5 4 9 8 4 9 0 3 5 6 8 9 3 9 1 9 6 5 8 2 6 4 6 1 3 7 0 0 3 0 7 5 8 3 9 1 3 7 6 9 3 2 7 5 1 2 1 7 2 8 4 3 9 5 6 9 5 3 4 8 4 9 5 7 6 3 4 4 6 6 7 6 7 1 1 0 6 2 1 8 3 5 8 0 3 3 8 1 9 2 9 2 2 1 6 9 5 2 1 0 0 1 0 0 3 0 7 8 7 7 9 7 5 9 1 6 9 8 5 2 7 1 3 2 1 9 5 9 3 9 5 9 9 1 6 5 4 1 8 4 8 2 3 0 8 9 7 7 4 1 3 5 7 8 5 5 5 4 2 8 9 0 0 1 1 9 1 0 6 7 9 7 3 4 3 5 2 7 7 0 7 6 7 8 6 5 5 8 2 7 1 5 1 4 5 2 0 4 6 8 1 8 7 0 8 8 7 9 4 6 9 8 9 0 7 8 5 4 0 8 1 0 6 3 5 4 3 4 4 4 5 9 6 7 3 1 9 6 2 6 3 0 0 2 8 6 7 2 5 8 6 0 3 3 4 1 1 9 2 4 3 8 3 8 1 7 6 2 6 4 4 9 3 8 0 9 6 6 1 0 7 1 6 9 8 3 4 4 2 3 2 0 6 5 3 0 6 7 5 0 8 9 8 8 2 5 8 5 1 9 2 1 3 2 1 3 2 6 9 7 3 1 1 0 5 0 0 7 1 5 9 6 0 3 7 2 7 0 4 4 2 6 7 3 3 9 7 7 6 5 2 1 6 6 9 5 5 9 0 4 4 3 6 1 7 9 7 4 1 3 3 0 7 7 3 2 8 7 1 8 2 5 2 7 9 3 7 7 1 7 5 4 8 1 4 9 3 0 5 3 1 9 0 9 1 9 9 7 7 9 1 5 1 3 1 2 2 5 2 3 1 1 0 9 2 5 3 0 4 8 3 0 4 7 6 2 0 0 0 1 8 0 9 9 8 3 8 9 9 2 2 6 1 7 7 0 3 0 0 1 7 2 7 8 5 7 1 5 3 8 2 7 9 4 6 9 9 7 8 9 7 0 4 2 7 5 5 5 9 5 7 1 8 6 3 9 8 5 4 8 5 0 9 0 0 2 6 5 4 4 4 2 5 3 1 5 5 0 6 6 5 1 2 8 1 2 3 9 5 8 8 8 2 2 8 4 8 7 6 7 6 8 9 5 1 5 3
```

#### Output

```
729
```

## Solution (Python)

```python
import math

N = int(input())
K = int(input())
M = int(input())
A = list(map(int, input().split()))

def find_subarrays(A, M):
    subarrays = []
    n = len(A)
    for i in range(n):
        for j in range(i + M, n + 1):
            subarrays.append(A[i:j])
    return subarrays

subarrays = find_subarrays(A, M)

def is_palindrome(arr):
    return arr == arr[::-1]

palindromic_subarrays = [subarr for subarr in subarrays if is_palindrome(subarr)]
subarrays = palindromic_subarrays


product_of_subarrays = sorted({math.prod(subarr) for subarr in subarrays})

print(product_of_subarrays[K - 1])
```