# Zombie Invasion

###### Made by [Kshitij](https://github.com/kshitijkota)

## Problem Statement

You are given a $ M \times N $ grid where:
- Each cell is either a zombie (denoted by $ 1 $) or a human (denoted by $ 0 $).
- Zombies can infect **only one** adjacent humans in **one step**. Adjacent cells are the ones that share a side (top, bottom, left, right).

Your task is to determine the **minimum time** required for all humans to be infected.

---

## Input Format

1. The first line contains two integers, $ M $ and $ N $ ($ 1 \leq M, N \leq 1000 $): the number of rows and columns in the grid.
2. The next $ M $ lines contain $ N $ integers each (either $ 0 $ or $ 1 $) representing the grid.

---

## Constraints

1. $1 \leq M, N \leq 1000$
2. At least one zombie ($ 1 $) exists in the grid.
3. Grid input is always valid.

---

## Output Format

A single integer representing the minimum time required to infect all humans.

---

## Test Cases

### Test Case 1 (3x3)

**Input:**
```
3 3
0 1 0
0 0 0
0 0 0
```

**Output:**
```
4
```

**Explanation:**

- Zombies infect humans in the following order:
    1. $(1, 2) \rightarrow (1, 1)$
    2. $(1, 1) \rightarrow (2, 1)$
    3. $(2, 1) \rightarrow (3, 1)$
    4. $(3, 1) \rightarrow (3, 2)$

---

### Test Case 2 (3x3)

**Input:**

```
3 3
1 1 1
0 0 0
0 0 0
```

**Output:**
```
2
```

---

### Test Case 3 (3x3)

**Input:**

```
3 3
1 1 1
1 1 1
1 1 1
```

**Output:**
```
0
```


---

###  Test Case 4 (4x4)

**Input:**

```
4 4
1 0 0 0
0 0 0 0
0 0 0 0
0 0 0 1
```

**Output:**

```
4
```

---

### Test Case 5 (5x3)

**Input:**

```
5 3
1 0 0
0 0 0
0 1 0
0 0 0
0 0 1
```

**Output:**
```
3
```

---

### Test Case 6 (7x9)

**Input:**

```
7 9
0 0 0 1 0 0 0 0 0
0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 1 0 0
0 0 1 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0
0 0 0 0 1 0 0 0 0
0 0 0 0 0 0 0 0 0
```

**Output:**
```
6
```

---

### Test Case 7 (1x7)

**Input:**

```
1 7
1 0 0 0 0 0 1
```

**Output:**
```
3
```

---
### Implementation using python

```python
from collections import deque
import copy
import sys

def get_neighbors(x, y, M, N):
    """Returns list of valid neighboring positions"""
    directions = [(-1, 0), (0, 1), (1, 0), (0, -1)]  # up, right, down, left
    neighbors = []
    for dx, dy in directions:
        new_x, new_y = x + dx, y + dy
        if 0 <= new_x < M and 0 <= new_y < N:
            neighbors.append((new_x, new_y))
    return neighbors

def count_humans(grid):
    """Count remaining humans in grid"""
    return sum(row.count(0) for row in grid)

def simulate_one_cycle(grid, M, N):
    """Simulate one clock cycle where each zombie can infect one human"""
    # Create a copy of current grid to track changes
    new_grid = copy.deepcopy(grid)
    # Track which zombies have infected in this cycle
    used_zombies = set()
    # Track which humans have been infected in this cycle
    infected_humans = set()

    # Check each cell
    for i in range(M):
        for j in range(N):
            # If this is a zombie that hasn't infected anyone yet
            if grid[i][j] == 1 and (i, j) not in used_zombies:
                # Get valid neighbors
                neighbors = get_neighbors(i, j, M, N)
                # Look for uninfected humans that haven't been infected this cycle
                for nx, ny in neighbors:
                    if grid[nx][ny] == 0 and (nx, ny) not in infected_humans:
                        # Infect this human
                        new_grid[nx][ny] = 1
                        used_zombies.add((i, j))
                        infected_humans.add((nx, ny))
                        break  # This zombie is done for this cycle

    return new_grid, len(infected_humans) > 0

def solve_zombie_infection(M, N, initial_grid):
    grid = copy.deepcopy(initial_grid)
    time = 0
    initial_humans = count_humans(grid)

    if initial_humans == 0:  # Already all zombies
        return 0

    while True:
        # Simulate one cycle
        new_grid, made_changes = simulate_one_cycle(grid, M, N)

        time += 1
        grid = new_grid

        # Check if all humans are infected
        if count_humans(grid) == 0:
            break

    return time

input = sys.stdin.read
data = input().split()

M = int(data[0])
N = int(data[1])
grid = []
index = 2
for i in range(M):
    row = []
    for j in range(N):
        row.append(int(data[index]))
        index += 1
    grid.append(row)

result = solve_zombie_infection(M, N, grid)
print(result)
```