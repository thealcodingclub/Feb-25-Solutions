# Sample: Goat Latin

###### Made by [Ritvik Matta](https://github.com/rtk5)

## Problem Statement
You are given a string sentence that consist of words separated by spaces. Each word consists of lowercase and uppercase letters only.

We would like to convert the sentence to "Goat Latin" (a made-up language similar to Pig Latin.) The rules of Goat Latin are as follows:

If a word begins with a vowel ('a', 'e', 'i', 'o', or 'u'), append "ma" to the end of the word.
For example, the word "apple" becomes "applema".
If a word begins with a consonant (i.e., not a vowel), remove the first letter and append it to the end, then add "ma".
For example, the word "goat" becomes "oatgma".
Add one letter 'a' to the end of each word per its word index in the sentence, starting with 1.
For example, the first word gets "a" added to the end, the second word gets "aa" added to the end, and so on.
Return the final sentence representing the conversion from sentence to Goat Latin.


---

## Input Format
- A sentence consists of English letters and spaces.

---

## Constraints
- 1 <= sentence.length <= 150
- sentence consists of English letters and spaces.
- sentence has no leading or trailing spaces.
- All the words in the sentence are separated by a single space.


---

## Output Format
- A sentence in Pig Latin.

---

## Test Cases

1. **Input:**
```
"I speak Goat Latin"
```

1.   **Output:**  
```
"Imaa peaksmaaa oatGmaaaa atinLmaaaaa"
```

1. **Explanation:**
    - The word "I" becomes "Imaa".
    - The word "speak" becomes "peaksmaaa".
    - The word "Goat" becomes "oatGmaaaa".
    - The word "Latin" becomes "atinLmaaaaa".

---

2. **Input:**
```
"The quick brown fox jumped over the lazy dog"
```

2.   **Output:**  
```
"heTmaa uickqmaaa rownbmaaaa oxfmaaaaa umpedjmaaaaaa overmaaaaaaa hetmaaaaaaaa azylmaaaaaaaaa ogdmaaaaaaaaaa"

```

---

3. **Input:**
```
"Hello world"
```

3.   **Output:**  
```
"elloHmaa orldwmaaa"
```
---

4. **Input:**
```
"Goat Latin is amazing"
```

4.   **Output:**  
```
"oatGmaa atinLmaaa ismaaaa amazingmaaaaa"
```
---

5. **Input:**
```
"Umbrella protects you from rain"
```

5.   **Output:**  
```
"Umbrellamaa rotectspmaaa ouymaaaa romfmaaaaa ainrmaaaaaa"
```
---

6. **Input:**
```
"apple orange banana grape"
```

6.   **Output:**  
```
"applemaa orangemaa aananabmaaa rapegmaaaa"
```
---

7. **Input:**
```
"I am enjoying this problem"
```

7.   **Output:**  
```
"Imaa amaa enjoyingmaaa histmaaaa roblempmaaaaa"
```
---

8. **Input:**
```
""
```

8.   **Output:**  
```
""
```
---


## Solution

### Pseudocode
1. Split the input sentence into a list of words using spaces as the delimiter.
2. Initialize an empty string `result` to store the final Goat Latin sentence.
3. Initialize `wordIndex` to 1 (to track the position of each word).
4. For each `word` in the list of words:
    4.1. If the first character of `word` is a vowel ('a', 'e', 'i', 'o', 'u', case-insensitive):
        - Append "ma" to the end of the word.
    4.2. Else (if the word starts with a consonant):
        - Remove the first character and append it to the end of the word.
        - Append "ma" to the end of the modified word.
    4.3. Append `'a'` repeated `wordIndex` times to the word.
    4.4. If `result` is not empty:
        - Append a space to `result`.
    4.5. Append the modified word to `result`.
    4.6. Increment `wordIndex` by 1.
5. Return `result` as the final Goat Latin sentence.

---

## Implementation

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <ctype.h>

int isVowel(char ch) {
    ch = tolower(ch);
    return ch == 'a' || ch == 'e' || ch == 'i' || ch == 'o' || ch == 'u';
}

int main() {
    char sentence[200];
    fgets(sentence, sizeof(sentence), stdin);
    
    char *result = malloc(2000); 
    result[0] = '\0'; 
    int wordIndex = 1;
    char *word = strtok(sentence, " \n");
    
    while (word != NULL) {
        char goatWord[200]; 
        if (isVowel(word[0])) {
            sprintf(goatWord, "%sma", word);
        } else {
            sprintf(goatWord, "%s%cma", word + 1, word[0]);
        }
        
        for (int i = 0; i < wordIndex; i++) {
            strcat(goatWord, "a");
        }
        
        if (result[0] != '\0') {
            strcat(result, " ");
        }
        strcat(result, goatWord);
        
        word = strtok(NULL, " \n");
        wordIndex++;
    }
    
    printf("%s\n", result);
    free(result);
    return 0;
}
```
