# SRE Training (Day 16) - Python Programming
**Author: bhoomikaushik**

## 1. Remove Parentheses Program

### Code Logic
1. Convert the string into a list for easy modification.
2. Traverse left to right and remove unmatched `)`.
3. Traverse right to left and remove unmatched `(`.
4. Join the modified list back into a string.
5. Return the balanced parentheses string.

### Code Implementation
```python
def remove_invalid_parentheses(s):
    # Convert string to list for easy modification
    chars = list(s)
    
    # First pass: remove unmatched closing parentheses
    open_count = 0
    i = 0
    while i < len(chars):
        if chars[i] == '(':
            open_count += 1
        elif chars[i] == ')':
            if open_count == 0:
                # Remove unmatched closing parenthesis
                chars.pop(i)
                i -= 1  # Adjust index after removal
            else:
                open_count -= 1
        i += 1
    
    # Second pass: remove unmatched opening parentheses (right to left)
    close_count = 0
    i = len(chars) - 1
    while i >= 0:
        if chars[i] == ')':
            close_count += 1
        elif chars[i] == '(':
            if close_count == 0:
                # Remove unmatched opening parenthesis
                chars.pop(i)
            else:
                close_count -= 1
        i -= 1
    
    # Join the modified list back into a string
    return ''.join(chars)

# Example usage
print(remove_invalid_parentheses("()())()"))  # Output: "()()()"
print(remove_invalid_parentheses("(()"))      # Output: "()"
```

## 2. Reverse Words Program

### Code Logic
- Split the sentence into words using `split()`.
- Reverse the order of words using slicing `[::-1]`.
- Join the reversed words back into a sentence using `' '.join()`.
- Return the final reversed sentence without altering individual words.

### Code Implementation
```python
def reverse_words(sentence):
    # Split the sentence into words
    words = sentence.split()
    
    # Reverse the order of words
    reversed_words = words[::-1]
    
    # Join the reversed words back into a sentence
    reversed_sentence = ' '.join(reversed_words)
    
    return reversed_sentence

# Example usage
print(reverse_words("Hello World"))               # Output: "World Hello"
print(reverse_words("Python is awesome"))         # Output: "awesome is Python"
print(reverse_words("SRE training day sixteen"))  # Output: "sixteen day training SRE"
```

## 3. Anagram Program

### Code Logic
- `sorted(s1)` and `sorted(s2)` convert the strings into sorted lists of characters.
- If the sorted versions match, the strings are anagrams.

### Code Implementation
```python
def is_anagram(s1, s2):
    # Remove spaces and convert to lowercase for case-insensitive comparison
    s1 = s1.replace(" ", "").lower()
    s2 = s2.replace(" ", "").lower()
    
    # If lengths are different, they can't be anagrams
    if len(s1) != len(s2):
        return False
    
    # Sort both strings and compare
    return sorted(s1) == sorted(s2)

# Example usage
print(is_anagram("listen", "silent"))       # Output: True
print(is_anagram("heart", "earth"))         # Output: True
print(is_anagram("python", "typhon"))       # Output: True
print(is_anagram("hello", "world"))         # Output: False
print(is_anagram("race a car", "car race")) # Output: True
```
