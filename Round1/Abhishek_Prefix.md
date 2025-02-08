# Office Performance Analysis

###### Made by [Abhishek](https://github.com/itsabhianant)

## Description

Calculate the total productivity of an employee over a specific range of days.

## Problem Statement

In a corporate office, the management tracks the daily performance scores of employees over a period of `n` days. Each performance score is recorded in an array, where each number represents the productivity score for a specific day.

The HR department frequently needs to calculate the total productivity of an employee over a specific range of days to assess performance during certain periods. Your task is to help HR efficiently process these queries and provide the requested information.

---

## Input Format

1. The first line contains two integers, `n` and `q`:
   - `n`: The number of days for which performance data is recorded (`1 ≤ n ≤ 2 × 10^5`).
   - `q`: The number of queries HR wants to process (`1 ≤ q ≤ 2 × 10^5`).

2. The second line contains `n` integers, `x_1, x_2, ..., x_n`, representing the performance scores for each day (`1 ≤ x_i ≤ 10^9`).

3. Each of the next `q` lines contains two integers `a` and `b` (`1 ≤ a ≤ b ≤ n`), representing a query. For each query, HR needs to calculate the total productivity from day `a` to day `b` (inclusive).

---

## Constraints

- `1 ≤ n, q ≤ 2 × 10^5`
- `1 ≤ x_i ≤ 10^9`
- `1 ≤ a ≤ b ≤ n`

---

## Output Format

For each query, output a single integer, the total productivity score over the specified range of days.

---

## Test Cases

1. Input:
   
```
8 4
3 2 4 5 1 1 5 3
2 4
5 6
1 8
3 3
```

1. Output:

```
11
2
24
4
```

1. Explanation

First Line: `8 4`

- `8` is the number of elements in the array.
- `4` is the number of queries.

Second Line: `3 2 4 5 1 1 5 3`

- This is the array of 8 elements.

Subsequent Lines: Each pair represents a query in the form `(a, b)`, where `a` is the starting index and `b` is the ending index (1-based index).

### Queries and Outputs

For each query `(a, b)`, you need to find the sum of the elements from index `a` to `b` (inclusive).

Let's go through a few queries to understand the output:

1. **Query (2, 4)**:
  - Sum of elements from index 2 to 4: `2 + 4 + 5 = 11`
  - Output: `11`

2. **Query (5, 6)**:
  - Sum of elements from index 5 to 6: `1 + 1 = 2`
  - Output: `2`

3. **Query (1, 8)**:
  - Sum of elements from index 1 to 8: `3 + 2 + 4 + 5 + 1 + 1 + 5 + 3 = 24`
  - Output: `24`

4. **Query (3, 3)**:
  - Sum of elements from index 3 to 3: `4`
  - Output: `4`

---

2. Input:
```
8 36
7 6 4 6 2 9 4 8
1 1
1 2
1 3
1 4
1 5
1 6
1 7
1 8
2 2
2 3
2 4
2 5
2 6
2 7
2 8
3 3
3 4
3 5
3 6
3 7
3 8
4 4
4 5
4 6
4 7
4 8
5 5
5 6
5 7
5 8
6 6
6 7
6 8
7 7
7 8
8 8
```

2. Output
```
7
13
17
23
25
34
38
46
6
10
16
18
27
31
39
4
10
12
21
25
33
6
8
17
21
29
2
11
15
23
9
13
21
4
12
8
```

2. Explanation

First Line: `8 36`

- `8` is the number of elements in the array.
- `36` is the number of queries.

Second Line: `7 6 4 6 2 9 4 8`

- This is the array of 8 elements.

Subsequent Lines: Each pair represents a query in the form `(l, r)`, where `l` is the starting index and `r` is the ending index (1-based index).

### Queries and Outputs

For each query `(l, r)`, you need to find the sum of the elements from index `l` to `r` (inclusive).

Let's go through a few queries to understand the output:

1. **Query (1, 1)**:
  - Sum of elements from index 1 to 1: `7`
  - Output: `7`

2. **Query (1, 2)**:
  - Sum of elements from index 1 to 2: `7 + 6 = 13`
  - Output: `13`

3. **Query (1, 3)**:
  - Sum of elements from index 1 to 3: `7 + 6 + 4 = 17`
  - Output: `17`

4. **Query (1, 4)**:
  - Sum of elements from index 1 to 4: `7 + 6 + 4 + 6 = 23`
  - Output: `23`

5. **Query (1, 5)**:
  - Sum of elements from index 1 to 5: `7 + 6 + 4 + 6 + 2 = 25`
  - Output: `25`

6. **Query (1, 6)**:
  - Sum of elements from index 1 to 6: `7 + 6 + 4 + 6 + 2 + 9 = 34`
  - Output: `34`

7. **Query (1, 7)**:
  - Sum of elements from index 1 to 7: `7 + 6 + 4 + 6 + 2 + 9 + 4 = 38`
  - Output: `38`

8. **Query (1, 8)**:
  - Sum of elements from index 1 to 8: `7 + 6 + 4 + 6 + 2 + 9 + 4 + 8 = 46`
  - Output: `46`

---

3. Input
```
5 3
15 20 25 30 35
1 3
2 5
3 4
```

3. Output
```
60
110
55
```
---

4. Input
```
10 2
1000000000 1000000000 1000000000 1000000000 1000000000 1000000000 1000000000 1000000000 1000000000 1000000000
1 10
5 10
```
4. Output
```
10000000000
6000000000
```
---
5. Input
```
1 1
1
1 1
```

5. Ouput
```
1
```
---
## Solution

### Pseudocode

1. **Input Reading**:
   - Read integers `n` (number of elements) and `q` (number of queries).
   - Read the array `arr` of size `n`.

2. **Prefix Sum Calculation**:
   - Create an array `prefix_sum` of size `n+1` (1-based indexing).
   - Initialize `prefix_sum[0] = 0`.
   - For `i = 1` to `n`:
     - `prefix_sum[i] = prefix_sum[i-1] + arr[i-1]`.

3. **Query Processing**:
   - For each query `(a, b)`:
     - Compute the range sum as:
       ```
       result = prefix_sum[b] - prefix_sum[a-1]
       ```
     - Output the `result`.

### Time Complexity
- Prefix sum computation: \( O(n) \)
- Query processing: \( O(1) \) per query, \( O(q) \) for all queries.
- Total: \( O(n + q) \)

### Space Complexity
- \( O(n) \) for the prefix sum array.
---

### Implementation

#### C++ Implementation

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    // Input reading
    int n, q;
    cin >> n >> q; // Number of elements and queries

    vector<int> arr(n); // Array to store the elements
    for (int i = 0; i < n; i++) {
        cin >> arr[i];
    }

    // Prefix sum calculation
    vector<long long> prefix_sum(n + 1, 0); // Prefix sum array
    for (int i = 1; i <= n; i++) {
        prefix_sum[i] = prefix_sum[i - 1] + arr[i - 1];
    }

    // Query processing
    while (q--) {
        int a, b;
        cin >> a >> b; // Read query range [a, b]
        cout << prefix_sum[b] - prefix_sum[a - 1] << endl; // Compute and print result
    }

    return 0;
}
```