# Kth Longest Subarrays with Sum Less Than or Equal to M

###### Made by [Angad](https://github.com/Anga205)

# Description

Given an array of integers and two integers k & m, return the k-th longest subarrays where sum of subarray <= m

## Problem Statement

Given an array `arr[]` of integers and two integers $k$ and $m$, return the $k$-th longest subarrays such that the sum of the elements of the subarray is less than or equal to $m$. If there are fewer than $k$ valid subarrays, return an empty list. If there are multiple subarrays that are the $k$-th longest, then return them in order of their occurance in the array

## Input Format

- A single integer $n$ representing the length of the array
- A space separated integer array of length $n$, which can contain both positive and negative numbers.
- An integer $k$ representing the position of the longest subarray (1-based index).
- An integer $m$ which represents the maximum allowed sum for the subarray.

## Constraints

- $1 \leq k \leq$ number of valid subarrays.
- $1 \leq n \leq 10^5$
- $-10^9 \leq$ elements of array $\leq 10^9$
- $-10^9 \leq m \leq 10^9$

## Output Format
A space-separated list of numbers representing the k-th longest contiguous subarray where the sum of the subarray’s elements is less than or equal to m. If there are fewer than k valid subarrays, return NULL.

if there are multiple k-th longest subarrays, print them in different lines in order of their occurance in the given array

## Sample Test Cases

### Test Case 1

#### Input

```
7
1 2 -1 2 3 -2 4
1
4
```

#### Output

```
2 -1 2 3 -2
```

#### Explanation

Value of n is `7`, so array has a length of `7`

Value of K is 1 and value of M is 4, so we need to find the 1st longest subarray with sum less than or equal to 4.

the longest subarray with sum ≤ 4 is `2 -1 2 3 -2`

---

### Test Case 2

#### Input

```
8
1 2 3 4 5 6 7 8
2
10
```

#### Output

```
1 2 3
2 3 4
```

#### Explanation
The value of `N` is 8, so the length of the array must be 8 numbers
the value of `K` is 2 and value of `M` is 10, so we must find the 2nd longest subarrays with a sum less than or equal to 10

the first longest valid subarray is 1,2,3,4 which has a length of 4

there are 2 valid subarrays with a length of 3 that are also less or equal to 4 (1,2,3 and 2,3,4)
since 2 subarrays are tied for the `K`-th place, we print them in different lines in order of their occurance in the array

---

### Test Case 4

#### Input

```
54
-1 96 69 -8 -97 31 40 -49 -8 -32 24 77 -75 13 74 -35 -40 -86 29 86 38 46 -62 17 36 34 -51 73 -91 19 -65 -30 -63 -81 47 31 64 8 38 44 77 65 -58 -33 38 -99 75 44 60 -100 9 80 78 -67
7
82
```

#### Output

```
-8 -97 31 40 -49 -8 -32 24 77 -75 13 74 -35 -40 -86 29 86 38 46 -62 17 36 34 -51 73 -91 19 -65 -30 -63 -81 47 31 64 8 38 44 77 65 -58 -33
```

---

### Test Case 5

#### Input

```
52
87 59 82 -72 -56 8 -96 75 -12 46 69 -55 35 -93 17 45 65 70 58 -20 -73 -36 34 -81 -54 -13 -3 33 -18 56 27 -95 29 -83 -34 71 54 82 -63 -1 -5 25 91 68 -64 -79 -84 21 57 -74 -74 -54
6
66
```

#### Output

```
59 82 -72 -56 8 -96 75 -12 46 69 -55 35 -93 17 45 65 70 58 -20 -73 -36 34 -81 -54 -13 -3 33 -18 56 27 -95 29 -83 -34 71 54 82 -63 -1 -5 25 91 68 -64 -79 -84 21
82 -72 -56 8 -96 75 -12 46 69 -55 35 -93 17 45 65 70 58 -20 -73 -36 34 -81 -54 -13 -3 33 -18 56 27 -95 29 -83 -34 71 54 82 -63 -1 -5 25 91 68 -64 -79 -84 21 57
-72 -56 8 -96 75 -12 46 69 -55 35 -93 17 45 65 70 58 -20 -73 -36 34 -81 -54 -13 -3 33 -18 56 27 -95 29 -83 -34 71 54 82 -63 -1 -5 25 91 68 -64 -79 -84 21 57 -74
-56 8 -96 75 -12 46 69 -55 35 -93 17 45 65 70 58 -20 -73 -36 34 -81 -54 -13 -3 33 -18 56 27 -95 29 -83 -34 71 54 82 -63 -1 -5 25 91 68 -64 -79 -84 21 57 -74 -74
8 -96 75 -12 46 69 -55 35 -93 17 45 65 70 58 -20 -73 -36 34 -81 -54 -13 -3 33 -18 56 27 -95 29 -83 -34 71 54 82 -63 -1 -5 25 91 68 -64 -79 -84 21 57 -74 -74 -54
```
---
---

Solution in C++

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <set>
#include <functional>
using namespace std;

struct Subarray {
    int start;
    int end;
    int length;
};

bool compareLength(const Subarray &a, const Subarray &b) {
    if (a.length == b.length) return a.start < b.start;
    return a.length > b.length;
}

int main() {
    int n, m;
    cin >> n;
    vector<int> arr(n);
    
    for (int i = 0; i < n; ++i)
        cin >> arr[i];
        
    int k;
    cin >> k;
    cin >> m;
    
    set<int> lens;
    vector<Subarray> validSubarrays;
    
    for (int start = 0; start < n; start++) {
        int sum = 0;
        for (int end = start; end < n; end++) {
            sum += arr[end];
            if (sum <= m) {
                Subarray sub;
                sub.start = start;
                sub.end = end;
                sub.length = end - start + 1;
                validSubarrays.push_back(sub);
                lens.insert(sub.length);
            }
        }
    }

    if (validSubarrays.empty()) {
        cout << "NULL" << endl;
        return 0;
    }

    vector<int> sortedLengths(lens.begin(), lens.end());
    sort(sortedLengths.begin(), sortedLengths.end(), greater<int>());
    
    int targetLength = sortedLengths[k - 1];

    for (const auto &sub : validSubarrays) {
        if (sub.length == targetLength) {
            for (int i = sub.start; i <= sub.end; ++i) {
                cout << arr[i] << " ";
            }
            cout << endl;
        }
    }

    return 0;
}
```