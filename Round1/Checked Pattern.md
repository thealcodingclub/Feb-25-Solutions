# Checked Matrix Pattern

###### Made by [Sampriti](https://github.com/Sampriti2803)

## Problem Statement
Create a matrix pattern based on a given integer N. The pattern is filled in two triangles:
1. *First Triangle:* Top to bottom, left to right.
2. *Second Triangle:* Bottom to top, right to left.

The characters alternate between uppercase and lowercase alphabets, wrapping back to 'A' or 'a' when 'Z' or 'z' is reached.

---

## Input Format
- An integer (N), where (1 ≤ N ≤ 100).

---

## Constraints
- (1 ≤ N ≤ 100)
- Input is always an integer.

---

## Output Format
- A symmetrical N x N matrix pattern where each row is printed on a new line with characters separated by a single space.

---

## Test Cases

### Test Case 1

*Input:*
```
1
```


*Output:*
```
A
```

---

### Test Case 2

*Input:*

```
3
```


*Output:*

```
A i H
b C g
D e F
```


---

### Test Case 3 (3x3)

*Input:*
```5```

*Output:*
```
A y X w V
b C u T s
D e F r Q
g H i J p
K l M n O
```

---

###  Test Case 4 (4x4)

*Input:*

```
10
```

*Output:*

```
A v U t S r Q p O n
b C m L k J i H g F
D e F e D c B a Z y
g H i J x W v U t S
K l M n O r Q p O n
p Q r S t U m L k J
V w X y Z a B i H g
c D e F g H i J f E
K l M n O p Q r S d
t U v W x Y z A b C
```

---


---

## Solution

### Pseudocode
1. Define a function checked_matrix that takes the input N and a 2D matrix of size N x N.
2. Initialize a variable current to 'A'.
3. Fill the first triangle (top to bottom, left to right) by iterating over the rows and columns where j <= i. Alternate the case of characters based on (i + j) % 2.
4. Fill the second triangle (bottom to top, right to left) by iterating where j > i.
5. Print the matrix row by row.

---

### Implementation

```c
#include <stdio.h>
#include <stdlib.h>
#include <ctype.h>

#define MAX_SIZE 100

void checked_matrix(int n, char matrix[MAX_SIZE][MAX_SIZE]) {
    char current = 'A';

    // Fill first triangle (top to bottom, left to right)
    for (int i = 0; i < n; i++) {
        for (int j = 0; j <= i; j++) {
            matrix[i][j] = (i + j) % 2 == 0 ? toupper(current) : tolower(current);
            current = (current == 'Z' || current == 'z') ? 'A' : current + 1;
        }
    }

    // Fill second triangle (bottom to top, right to left)
    for (int i = n - 1; i >= 0; i--) {
        for (int j = n - 1; j > i; j--) {
            matrix[i][j] = (i + j) % 2 == 0 ? toupper(current) : tolower(current);
            current = (current == 'Z' || current == 'z') ? 'A' : current + 1;
        }
    }
}

void print_matrix(int n, char matrix[MAX_SIZE][MAX_SIZE]) {
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            if (matrix[i][j] != '\0') {
                printf("%c ", matrix[i][j]);
            }
        }
        printf("\n");
    }
}

int main() {
    int n;
    char matrix[MAX_SIZE][MAX_SIZE] = {0};

    printf("Enter the size of the matrix (N): ");
    scanf("%d", &n);

    if (n < 1 || n > MAX_SIZE) {
        printf("Invalid input. N must be between 1 and 100.\n");
        return 1;
    }

    checked_matrix(n, matrix);
    print_matrix(n, matrix);

    return 0;
}
```
