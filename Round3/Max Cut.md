# K-th Smallest Subarray Product

###### Made by [The Alcoding Club](https://github.com/thealcodingclub)

## Problem Statement

You are given an undirected connected weighted [graph](https://en.wikipedia.org/wiki/Graph_(discrete_mathematics)) of $n$ nodes and $m$ edges. The graph doesn't contain self loops or multiple edges.

You are required to select any integer $x$ and remove all edges from the graph that have weight **strictly lesser** than $x$. The graph should remain connected after this operation.

The integer $x$ that you select must be the maximum such value for which the graph remains connected.

A graph is said to be connected if every node in the graph can be reached from every other node in the graph by traversing some edges.

**Note:** If you are using _Python_ to solve the problem, use "Python 3" and not "Pypy 3" as the former has a TL of $15s$ whereas the latter can only be set to a maximum of $6s$. _C/C++_ TL is $3s$.

## Input Format

$1 \le n \le 3 \cdot 10^5$

$n - 1 \le m \le min(\frac{n \cdot (n - 1)}{2},\ 3 \cdot 10^5)$

$1 \le u_i, v_i \le n$

$1 \le w_i \le 10^9$

## Constraints

- All array elements are positive integers.
- Consider all contiguous subarrays of length at least M.
- (1 ≤ `A[i]` ≤ 10<sup>4</sup>)
- (1 ≤ `M` ≤ `N` ≤ 10<sup>5</sup>)
- (1 ≤ `K` ≤ `N` * (`N` + 1) / 2)

## Output Format

Output a single integer $x$ satisfying the conditions in the problem statement.


## Sample Test Cases

### Test Case 1

#### Input

```
5 5
2 1 7
5 3 8
4 2 3
3 1 5
3 4 6
```

#### Output

```
5
```

#### Explanation

The given graph looks something like:

![Graph-1](https://s3.amazonaws.com/hr-assets/0/1644716952-da69d919b1-graph-1.png)

After removing all edges with weight lower than $5$, we get the following graph:

![Graph-2](https://s3.amazonaws.com/hr-assets/0/1644716972-b08e491714-graph-2.png)

It can be shown that $5$ is the maximum value of $x$ such that the graph remains connected after removing all edges with weight lower it.

## Solution (Python)

```python
import sys

class UnionFind:
    def __init__(self, n):
        self.parent = list(range(n))
        self.rank = [0] * n

    def find(self, u):
        if self.parent[u] != u:
            self.parent[u] = self.find(self.parent[u])
        return self.parent[u]

    def union(self, u, v):
        root_u = self.find(u)
        root_v = self.find(v)
        if root_u != root_v:
            if self.rank[root_u] > self.rank[root_v]:
                self.parent[root_v] = root_u
            elif self.rank[root_u] < self.rank[root_v]:
                self.parent[root_u] = root_v
            else:
                self.parent[root_v] = root_u
                self.rank[root_u] += 1

def maximum_spanning_tree(n, edges):
    edges.sort(key=lambda x: -x[2])  # Sort edges by weight in descending order
    uf = UnionFind(n)
    max_x = float('inf')
    
    for u, v, w in edges:
        if uf.find(u) != uf.find(v):
            uf.union(u, v)
            max_x = w
    
    return max_x

if __name__ == "__main__":
    input = sys.stdin.read
    data = input().split()
    
    n = int(data[0])
    m = int(data[1])
    edges = []
    
    index = 2
    for _ in range(m):
        u = int(data[index]) - 1
        v = int(data[index + 1]) - 1
        w = int(data[index + 2])
        edges.append((u, v, w))
        index += 3
    
    result = maximum_spanning_tree(n, edges)
    print(result)
```