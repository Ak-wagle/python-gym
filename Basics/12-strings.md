# Module 5.1: Strings

A **string** is an **immutable sequence of characters**. "Immutable" means once created, you cannot change individual characters - you must create a new string. Strings support indexing (accessing characters by position) and slicing (extracting substrings), similar to how you'd work with lists (you'll learn lists in Module 5.2).

**Key Technical Properties:**
- **Ordered**: Characters have positions (index 0, 1, 2, etc.)
- **Immutable**: Can't change characters in place (`string[0] = 'X'` causes error)
- **Indexable**: Access characters with position: `string[0]` = first character
- **Sliceable**: Extract portions: `string[0:5]` = first 5 characters
- **Iterable**: Can loop through characters

**Why This Matters**: Understanding strings as sequences is crucial for text processing, especially in robotics (parsing sensor output, log files, commands).

---

## String Indexing and Negative Indexing

### Positive Indexing (Left to Right)

```python
text = "Python"

# Accessing by position
print(text[0])  # P (first character)
print(text[1])  # y
print(text[5])  # n (last character)

# Common positions
# Index:  0 1 2 3 4 5
# Char:   P y t h o n
```

### Negative Indexing (Right to Left)

```python
text = "Python"

print(text[-1])  # n (last character)
print(text[-2])  # o (second to last)
print(text[-6])  # P (first character)

# Negative positions
# Index:  -6 -5 -4 -3 -2 -1
# Char:    P  y  t  h  o  n
```

**When to Use**: Negative indexing is great when you want characters from the end without knowing string length.

---

## String Slicing

### Slicing Syntax: `string[start:stop:step]`

```python
text = "Hello World"

# Basic slicing [start:stop]
print(text[0:5])    # "Hello" (start at 0, stop before 5)
print(text[6:11])   # "World"

# Omitting start or stop
print(text[:5])     # "Hello" (start is default 0)
print(text[6:])     # "World" (stop is default end)
print(text[:])      # "Hello World" (entire string)

# Step parameter
print(text[::2])    # "HloWrd" (every 2nd character)
print(text[1::2])   # "el ol" (start at 1, every 2nd)

# Reverse string
print(text[::-1])   # "dlroW olleH" (reverse!)
print(text[-1::-1]) # "dlroW olleH" (also reverse)
```

**Key Rule**: Slicing goes from index `start` UP TO (but not including) index `stop`.

---

## String Methods for Processing

### Case Methods

```python
text = "Hello World"

print(text.upper())           # "HELLO WORLD"
print(text.lower())           # "hello world"
print(text.capitalize())      # "Hello world" (first letter capital)
print(text.title())           # "Hello World" (each word capitalized)
print(text.swapcase())        # "hELLO wORLD" (flip case)
```

### Finding/Searching Methods

```python
text = "Hello World"

# Find position of substring
print(text.find("World"))     # 6 (position where "World" starts)
print(text.find("xyz"))       # -1 (not found)
print(text.index("World"))    # 6 (same as find, but errors if not found)

# Count occurrences
print(text.count("l"))        # 3 (three 'l' characters)
print(text.count("o"))        # 2

# Check if starts/ends with
print(text.startswith("Hell")) # True
print(text.startswith("World")) # False
print(text.endswith("ld"))     # True
print(text.endswith("Hello"))  # False
```

### Cleaning/Replacing Methods

```python
text = "  Hello World  "

# Remove whitespace
print(text.strip())           # "Hello World" (remove from both ends)
print(text.lstrip())          # "Hello World  " (left side only)
print(text.rstrip())          # "  Hello World" (right side only)

# Replace characters
print(text.replace("World", "Python"))  # "  Hello Python  "
print(text.replace("l", "L"))  # "  HeLLo WorLd  "

# Useful for cleaning user input
user_input = "  Alice  "
name = user_input.strip()     # "Alice" - clean for processing
```

### Checking Methods

```python
text = "Hello123"

print(text.isalpha())         # False (contains numbers)
print(text.isdigit())         # False (contains letters)
print(text.isalnum())         # True (all alphanumeric)
print(text.isupper())         # False (not all uppercase)
print(text.islower())         # False (not all lowercase)
print(text.isspace())         # False (not just spaces)

# Practical example
password = "Pass123!"
if len(password) >= 8 and password.isalnum():
    print("Valid password")
```

**Note about `len()`**: This function works with any sequence. You'll see it again with lists and other collections.

### Splitting and Joining Methods

```python
text = "apple,banana,cherry"

# Split into list (you'll learn lists in Module 5.2)
fruits = text.split(",")      # ["apple", "banana", "cherry"]

# Join list back into string
words = ["Hello", "World", "Python"]
result = " ".join(words)      # "Hello World Python"

# Practical: Split sentences into words
sentence = "The quick brown fox"
words = sentence.split()      # ["The", "quick", "brown", "fox"]
```

**Note about lists**: When you call `.split()`, it returns a list. Don't worry about how lists work yet - you'll learn in Module 5.2. For now, just know you get multiple values back.

---

## String Formatting (Deep Dive)

### F-Strings (Recommended - Python 3.6+)

```python
name = "Patrick"
age = 42
score = 95.5

# Simple insertion
print(f"Name: {name}, Age: {age}")  # "Name: Patrick, Age: 42"

# Expressions inside {}
print(f"Next year: {age + 1}")      # "Next year: 43"
print(f"Score: {score:.1f}%")       # "Score: 95.5%" (1 decimal)

# Method calls
print(f"Uppercase: {name.upper()}")  # "Uppercase: PATRICK"

# Alignment and padding
print(f"{name:10}")                 # "Patrick     " (10 chars wide)
print(f"{age:>5}")                  # "   42" (right aligned)
print(f"{score:.2f}")               # "95.50" (2 decimals)
```

### Old-School String Formatting (Still Works)

```python
# % formatting
print("Name: %s, Age: %d" % ("Patrick", 42))

# .format() method
print("Name: {}, Age: {}".format("Patrick", 42))

# Just concatenation
print("Name: " + name + ", Age: " + str(age))
```

**Recommendation**: Use f-strings - they're cleaner and faster!

---

## Practical Examples

### Example 1: URL Parser

```python
url = "https://www.example.com/path/to/page"

# Extract components
protocol = url.split("://")[0]      # "https"
domain = url.split("://")[1].split("/")[0]  # "www.example.com"
path = "/" + url.split("/", 3)[3]   # "/path/to/page"

print(f"Protocol: {protocol}")
print(f"Domain: {domain}")
print(f"Path: {path}")
```

### Example 3: Password Validator

```python
def validate_password(password):
    """Check if password meets requirements"""
    
    if len(password) < 8:
        return False, "Too short (min 8 chars)"
    
    if not any(c.isupper() for c in password):
        return False, "Missing uppercase letter"
    
    if not any(c.isdigit() for c in password):
        return False, "Missing digit"
    
    return True, "Valid password!"

# Test
pwd = "Pass123"
is_valid, message = validate_password(pwd)
print(f"Password '{pwd}': {message}")
```

**Note about `any()`**: This function checks if any item in a list is True. You'll learn more about this in Module 10.2.

---

## Common Mistakes

### ❌ Mistake 1: Trying to Change String (Immutable)

```python
# ERROR - strings are immutable
text = "Hello"
text[0] = "J"  # TypeError!

# Create new string instead
text = "J" + text[1:]  # "Jello"
```

### ❌ Mistake 2: Forgetting Methods Return New String

```python
text = "hello"

# Wrong - doesn't modify text
text.upper()  # Returns "HELLO" but doesn't save it
print(text)   # Still "hello"!

# Save the result
text = text.upper()
print(text)   # "HELLO"
```

---

## Milestone Task: Text Processor

Create a program that processes and analyzes text!

### Requirements:
- Take user input (sentence/paragraph)
- Perform multiple string operations
- Calculate statistics
- Display formatted results
- Use at least 5 different string methods

### Example Output:

```
==================================================
TEXT PROCESSOR
==================================================

Enter some text: Hello World! 123

==================================================
ANALYSIS
==================================================
Length: 13 characters
Letters: 10
Digits: 3
Spaces: 2
Uppercase: 2
Lowercase: 8

==================================================
TRANSFORMATIONS
==================================================
UPPERCASE: HELLO WORLD! 123
lowercase: hello world! 123
Reversed: 321 !dlroW olleH
Title Case: Hello World! 123

Words: 3
Words: ['Hello', 'World!', '123']

Most common letter: 'l' (3x)
```

---

## What's Next?

Next module: **Lists** - Mutable sequences that can hold multiple items!

---

## References

- Strings: https://docs.python.org/3/tutorial/introduction.html#strings
- String Methods: https://docs.python.org/3/library/stdtypes.html#string-methods

