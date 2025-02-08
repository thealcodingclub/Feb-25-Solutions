# Palindrome Permutation

###### Made by [Nishant](https://github.com/nishantHolla)

## Problem Statement
Given a string, write a function to check if any valid permutation of the string results in a
palindrome. A permutation is a rearrangement of letters in the string. A palindrome is a word or
phrase that is the same as forwards and backward. The palindrome does not need to be in a dictionary.

---

## Input Format
- A string `S` of length `N`;

---

## Constraints
- 1 < `N` < 1000
- `S[i]` is an English letter (both upper case and lower case) or space

---

## Output Format
- Print `1` if any permutation of string `S` is a palindrome else print `0`.

---

## Test case

1. **Input:**
```
TaCT Coao
```

1. **Output:**
```
1
```

1. **Explanation:**
```plaintext
The string "TaCT Coao" can be rearranged to form a palindrome "Taco cat".
```

2. **Input:**
```
X
```

2. **Output:**
```
1
```

3. **Input:**
```
The quick brown fox JuMped oVer The Lazy dog
```

3. **Output:**
```
0
```

3. **Explanation:**
```plaintext
The string "The quick brown fox JuMped oVer The Lazy dog" cannot be rearranged to form a palindrome.
```


4. **Input:**
```
A man a Plan A canal Panama
```

4. **Output:**
```
1
```

5. **Input:**
```
Was it A Car or A Cat i saW
```

5. **Output:**
```
1
```

6. **Input:**
```
pneumonoultramicroscopicsilicovolcanoconiosis
```

6. **Output:**
```
0
```

7. **Input:**
```
hcadmbefgglflhbhalihhjjadfgiebkijhacblibkfdgigbkjeleffcgidcljkkdcebeamdeimchchjddmalefmbmkmagflgjkjkica hcadmbefgglflhbhalihhjjadfgiebkijhacblibkfdgigbkjeleffcgidcljkkdcebeamdeimchchjddmalefmbmkmagflgjkjkica hcadmbefgglflhbhalihhjjadfgiebkijhacblibkfdgigbkjeleffcgidcljkkdcebeamdeimchchjddmalefmbmkmagflgjkjkica hcadmbefgglflhbhalihhjjadfgiebkijhacblibkfdgigbkjeleffcgidcljkkdcebeamdeimchchjddmalefmbmkmagflgjkjkica hcadmbefgglflhbhalihhjjadfgiebkijhacblibkfdgigbkjeleffcgidcljkkdcebeamdeimchchjddmalefmbmkmagflgjkjkica hcadmbefgglflhbhalihhjjadfgiebkijhacblibkfdgigbkjeleffcgidcljkkdcebeamdeimchchjddmalefmbmkmagflgjkjkica hcadmbefgglflhbhalihhjjadfgiebkijhacblibkfdgigbkjeleffcgidcljkkdcebeamdeimchchjddmalefmbmkmagflgjkjkica hcadmbefgglflhbhalihhjjadfgiebkijhacblibkfdgigbkjeleffcgidcljkkdcebeamdeimchchjddmalefmbmkmagflgjkjkica hcadmbefgglflhbhalihhjjadfgiebkijhacblibkfdgigbkjeleffcgidcljkkdcebeamdeimchchjddmalefmbmkmagflgjkjkica hcadmbefgglflhbhalihhjjadfgiebkijhacblibkfdgigbkjeleffcgidcljkkdcebeamdeimchchjddmalefmbmkmagflgjkjkica hcadmbefgglflhbhalihhjjadfgiebkijhacblibkfdgigbkjeleffcgidcljkkdcebeamdeimchchjddmalefmbmkmagflgjkjkica
```

7. **Output:**
```
1
```

8. **Input:**
```
hello
```

8. **Output:**
```
0
```

## Solution

### Pseudocode
1. Read input string `S`
2. Create Hash Map `h` with default value of 0.
3. Iterate through the string and increment the value of the character in the hash map `h`.
4. If more than one value in the hash map has odd value then print `0` else print `1`.

```plaintext
function is_permutaiton_palindrome(S):
    HashMap h
    for c in S:
        if c in h:
            increment h[c]
        else:
            set h[c] to 1

    odd_count = 0
    for c in h:
        if h[c] is odd:
            increment odd_count

    if odd_count > 1:
        print 0
    else
        print 1
```

### Implementation

```python
def is_permutaiton_palindrome(S):
	h = dict()
	for c in S:
		if c in h:
			h[c] += 1
		else:
			h[c] = 1

	odd_count = 0
	for key in h:
		if h[key] % 2 != 0:
			odd_count += 1
	if odd_count > 1:
		print('0')
	else:
		print('1')
is_permutaiton_palindrome(input())
```
