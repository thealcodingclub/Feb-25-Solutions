# Social Media Engagement Analysis

###### Made by [Diya J Marar](https://github.com/diya-jm)

## Problem Statement
Analyze the daily engagement rates (likes + comments) of social media posts over a period of days to identify trends and patterns.
You are given a list of daily engagement rates for a series of social media posts over a period of `n` days. Each engagement rate is recorded in an array, where each element represents the engagement rate on a specific day. Your task is to process multiple queries to extract useful insights based on the engagement rates. For each query, you need to determine the following:
1. The length of the longest continuous sequence of days with increasing or stable engagement rates.

2. The total number of distinct engagement levels within a specified range of days.

3. The day on which a target engagement rate first occurs within the specified range, or `-1` if it does not occur.

## Constraints

- 1 < n < 1000
- 0 < Engagement rate <= 10000 for each day

## Input Format
1. Integer n: number of days.
2. Array of length n: daily engagement rates.
3. Integer q: number of queries.
4. Next q lines: three integers L, R (range of days), and T (target engagement rate).

## Output Format
For each query, print three values separated by spaces:
- Length of the longest continuous sequence of increasing or stable engagement rates.
- Total number of distinct engagement levels within the specified range.
- Day on which the target engagement rate first occurs within the specified range, or -1 if it does not occur.
## Test Cases
1. Input:
   ```
   9
   10 20 30 20 10 30 40 20 10
   3
   1 9 30
   3 7 40
   4 8 20
   ```
    Output:
   ```
   3 4 3
   3 4 7
   3 4 4
   ```
2. Input:
   ```
   6
   150 200 120 180 170 210
   2
   1 6 180
   2 5 170
   ```
   Output:
   ```
   2 6 4
   2 4 5  
   ```
3. Input:
   ```
   5
   180 180 180 180 180
   2
   1 5 180
   2 4 190
   ```
   Ouput:
   ```
   5 1 1
   3 1 -1
   ```
4. Input:
   ```
   12
   500 400 400 300 300 400 500 400 300 300 200 100
   3
   1 12 300
   3 9 400
   5 12 200
   ```
   Output:
   ```
   4 5 4
   4 3 3
   3 5 11   
   ```
5. Input:
   ```
   3
   300 300 300
   1
   1 2 200
   ```
   Output:
   ```
   2 1 -1
    ```


## Pseudocode
```
function longest_seq(rates, start, end):
    initialize max_length = 1
    initialize curr_length = 1
    for i from start + 1 to end:
        if rates[i] >= rates[i - 1]:
            increment curr_length
        else:
            update max_length = max(max_length, curr_length)
            reset curr_length = 1
    update max_length = max(max_length, curr_length)
    return max_length

function distinct_levels(rates, start, end):
    create a set from rates[start to end]
    return size of the set

function first_occurrence(rates, start, end, target):
    for i from start to end:
        if rates[i] == target:
            return i + 1 (1-based index)
    return -1

# Main Program
read integer n
read list of integers rates of length n
read integer q

for each query in q:
    read integers l, r, t
    adjust l and r to be 0-based (l -= 1, r -= 1)

    longest_seq_len = longest_seq(rates, l, r)
    distinct_levels_count = distinct_levels(rates, l, r)
    target_day = first_occurrence(rates, l, r, t)

    print longest_seq_len, distinct_levels_count, target_day

```

## Implementation
```python
def longest_seq(rates, start, end):
    max_len = 1
    curr_len = 1
    for i in range(start + 1, end + 1):
        if rates[i] >= rates[i - 1]:
            curr_len += 1
        else:
            max_len = max(max_len, curr_len)
            curr_len = 1
    max_len = max(max_len, curr_len)
    return max_len

def distinct_levels(rates, start, end):
    return len(set(rates[start:end + 1]))

def first_occurrence(rates, start, end, target):
    for i in range(start, end + 1):
        if rates[i] == target:
            return i + 1
    return -1

# Main Program
n = int(input())
rates = list(map(int, input().split()))
q = int(input())

for _ in range(q):
    l, r, t = map(int, input().split())
    l -= 1
    r -= 1
    
    longest_seq_len = longest_seq(rates, l, r)
    distinct_levels_count = distinct_levels(rates, l, r)
    target_day = first_occurrence(rates, l, r, t)
    
    print(longest_seq_len, distinct_levels_count, target_day)

```