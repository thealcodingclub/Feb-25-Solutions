# Longest Collatz Chain

###### Made by [Akshaj](https://github.com/unhexate)

## Problem Statement

$f(n)$ is defined as  $$f(n) = 
\begin{cases} 
0, & \text{if } n = 1 \\ 
\frac{n}{2}, & \text{if } n \text{ is even} \\ 
3n + 1, & \text{if } n \text{ is odd and } n \neq 1 
\end{cases}$$

A chain is a sequence of numbers such that $a_{n+1}=f(a_n)$. For example, `3,10,5`
is a chain because $f(3)=10$ and $f(10)=5$. 

Given an array of distinct positive numbers, return the length of the longest chain using only the given elements.

---

## Input Format
- the number of elements ( `n` )
- `n` space separated integers, where each integer `i` describes array element `a[i]` (where 0 ≤ `i` ≤ `n`)

---

## Constraints
- $1 ≤ n ≤ 10^5$
- $1 ≤ a[i] ≤ 10^9$
- Array elements are distinct (meaning no two elements are equal)

---

## Output Format
- A single integer representing the length of the longest chain.

--- 

## Test Cases

1. **Input:**
```
4
5 3 2 10
```

1. **Output:**  
```
3
```

1. **Explanation:**
```
The longest chain is [3,10,5].
``` 
---

2. **Input:**
```
4
1 4 2 8
```

2.   **Output:**  
```
4
```

2. **Explanation:**
```
The longest chain is [8,4,2,1].
``` 

---

3. **Input:**
```
4
16 5 32 2
```

3.   **Output:**  
```
2
```

3. **Explanation:**
```
The longest chain is [5,16] or [32,16]
```

---

4. **Input:**
```
4
7 2 5 12
```

4.   **Output:**  
```
1
```

4. **Explanation:**
```
The longest chain is [7], [2], [5], or [12].
```

---

5. **Input:**
```
52
1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 32 33 34 35 36 37 38 39 40 41 42 43 44 45 46 47 48 49 50 51 52
```

5.   **Output:**  
```
22
```

5. **Explanation:**
```
The longest chain is [36,18,9,28,14,7,22,11,34,17,52,26,13,40,20,10,5,16,8,4,2,1]
```

---

6. **Input:**
```
51
1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 32 33 34 35 36 37 38 39 40 41 42 43 44 45 46 47 48 49 50 51
```

6.   **Output:**  
```
12
```

6. **Explanation:**
```
The longest chain is [48,24,12,6,3,10,5,16,8,4,2,1]
```

## Solution

### Pseudocode
1. Read the number of elements `n`.
2. Read the elements `a[i]` and store them in a dictionary `chain_map` with the value 1.
3. Iterate through the dictionary.
4. For an element `x`, if `x`'s value is not 1, continue.
5. While `x`'s value in the dictionary is 1, push x onto a queue `visited` and set x to `f(x)`, ie, follow the chain of unvisitedited numbers.
6. If `x` is in the dictionary, then while `visited` is not empty, dequeue the front element and set its value in `chain_map` to `len(visited)+chain_map[x]`
7. Else, while `visited` is not empty, dequeue the front element and set its value in `chain_map` to `len(visited)`
8. After iterating through the entire dictionary `chain_map`, return the maximum value.

```plaintext
function maxChain(a):
    chain_map = empty dictionary
    for x in a:
        set chain_map[x] to 1 
    visited = empty queue
    for each x in chain_map.keys():
        if chain_map[x] is not equal to 1:
            continue
        while chain_map[x] equals 1:
            add x to visited
            x = f(x)
        if chain_map[x] exists:
            while visited is not empty:
                chain_map[visited[0]] = length of visited + chain_map[x]
                pop front element from visited
        else:
            while visited is not empty:
                chain_map[visited[0]] = length of visited
                pop front element from visited
    return max value from chain_map
```

---

## Implementation

```py
def f(x):
    return 0 if x==1 else 3*x+1 if x%2 else x//2
def maxChain(myarray):
    chain_map={x:1 for x in myarray}
    visited=[]
    for x in chain_map.keys():
        if(chain_map[x]!=1):
            continue
        while(chain_map.get(x)==1): #follow chain
            visited+=[x]
            x=f(x)
        if(chain_map.get(x)): #we end on number whose chain is made
            while len(visited):
                chain_map[visited[0]]=len(visited)+chain_map.get(x)
                visited=visited[1:]
        else: #we end on number not in input
            while len(visited):
                chain_map[visited[0]]=len(visited)
                visited=visited[1:]
    return max(chain_map.values())

n = int(input())
a = list(map(int, input().split()))[:n]
print(maxChain(a))
```