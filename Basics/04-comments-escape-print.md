# Module 1.4: Comments, Escape Sequences & Print Customization

Good code isn't just about working - it's about being **readable**. This module teaches you three things that make code cleaner: comments, escape sequences, and print formatting.

## Comments: Notes in Your Code

A **comment** is text that Python ignores. Use it to explain what your code does.

### Single-Line Comments

Use `#` for comments on one line:

```python
# This is a comment
name = "Shakespeare"  # This is also a comment

# Calculate area of circle
PI = 3.14159
radius = 5
area = PI * radius ** 2
```

### Multi-Line Comments

Use triple quotes for longer explanations:

```python
"""
This is a multi-line comment.
You can write multiple lines here.
This explains what the function/program does.
"""

'''
You can also use single quotes
instead of double quotes.
Both work!
'''
```

### When to Comment

**Good comments explain WHY, not WHAT:**

```python
#  Bad comment (obvious what it does)
x = 5  # Set x to 5

#  Good comment (explains why)
DISCOUNT_PERCENTAGE = 0.15  # 15% discount for bulk orders
```

## Escape Sequences: Special Characters

An **escape sequence** is a combination of characters that Python interprets as a special instruction.

### Common Escape Sequences

| Sequence | What it does | Example |
|----------|------------|---------|
| `\n` | New line | `"Hello\nWorld"` → Hello (newline) World |
| `\t` | Tab (indent) | `"Name\tAge"` → Name    Age |
| `\\` | Backslash | `"C:\\Users\\Bob"` → C:\Users\Bob |
| `\"` | Double quote | `"He said \"Hi\""` → He said "Hi" |
| `\'` | Single quote | `'It\'s cool'` → It's cool |
| `\r` | Return to line start | Rarely used |
| `\b` | Backspace | Rarely used |

### Examples

```python
# New lines
print("Line 1\nLine 2\nLine 3")
# Output:
# Line 1
# Line 2
# Line 3
```
```python
# Tabs for indentation
print("Name\tAge\tCity")
print("Alexander\t25\tNYC")
print("Ashoka\t30\tLA")
# Output:
# Name    Age    City
# Alexander   25     NYC
# Ashoka     30     LA
```
```python
# Backslashes (file paths)
print("My files are in C:\\Users\\MyName\\Documents")
```
```python
# Quotes
print("He said \"Hello!\"")
print("It's a beautiful day")
```
```python
# Combined
print("Dear Ronaldo,\n\tWelcome to Python!\n\t  - Python Team")
# Output:
# Dear Ronaldo,
#    Welcome to Python!
#      - Python Team
```

## Print Customization: sep and end

The `print()` function has hidden powers!

### The sep Parameter (Separator)

By default, `print()` separates items with a space. Change it with `sep`:

```python
# Default separator (space)
print("A", "B", "C")
# Output: A B C

# Custom separator
print("A", "B", "C", sep="-")
# Output: A-B-C

print("Apple", "Banana", "Cherry", sep=" | ")
# Output: Apple | Banana | Cherry

print("Item1", "Item2", "Item3", sep="")
# Output: Item1Item2Item3

# Useful for CSV format
print("Name", "Age", "City", sep=",")
print("Messi", 30, "Argentina", sep=",")
```

### The end Parameter (Ending)

By default, `print()` ends with a newline. Change it with `end`:

```python
# Default (prints newline at end)
print("Loading")
print("Loading")  # Prints on new line

# Custom ending
print("Loading", end=" ")
print("Loading", end=" ")
print("Done!")
# Output: Loading Loading Done!
```

## String Repetition & Formatting

### Repeating Strings

```python
print("*" * 10)
# Output: **********

print("=" * 20)
# Output: ====================

print("Ha" * 3)
# Output: HaHaHa
```

### F-Strings (Best for Formatting)

F-strings let you put variables directly in text:

```python
name = "Donald"
age = 50

# Old way (concatenation)
print("My name is " + name + " and I'm " + str(age))

# Better way (f-string)
print(f"My name is {name} and I'm {age}")

# With expressions inside {}
price = 19.99
quantity = 3
print(f"Total: ${price * quantity}")

# With formatting
pi = 3.14159
print(f"Pi ≈ {pi:.2f}")  # .2f = 2 decimal places
# Output: Pi ≈ 3.14
```

## Common Mistakes

### ❌ Mistake 1: Forgetting Backslash in Escape Sequences

```python
print("C:\Users\Bob")  #  Doesn't work right
print("C:\\Users\\Bob")  #  Correct
```

### ❌ Mistake 2: Using Wrong Quotes Inside String

```python
print("He said "Hello"")  # ERROR! Confuses Python
print("He said \"Hello\"")  # Escape the inner quotes
print('He said "Hello"')  # Use different quote type
```

### ❌ Mistake 3: Mixing sep and end Wrong

```python
print(1, 2, 3 sep="-")  #  Missing comma before sep
print(1, 2, 3, sep="-")  #  Correct

print("Loading"end="...")  # Missing comma before end
print("Loading", end="...")  # Correct
```

### ❌ Mistake 4: Forgetting Closing Quote

```python
name = "John  #  Missing closing quote
print(f"Hello {name}")
```

## Milestone Task: ASCII Art Creator

Create a program that uses escape sequences and string repetition to generate cool ASCII art!

### Requirements:
- Use `\n` for new lines
- Use `\t` for indentation
- Use string repetition (`*` * n)
- Create at least 3 different ASCII designs
- Print them with clear separation
- Add comments explaining each section

### Example Output:

```
╔════════════════════════════════════════╗
║          ASCII ART GALLERY              ║
╚════════════════════════════════════════╝

Design 1: Simple Tree
    *
   ***
  *****
 *******
    |

Design 2: Box Border
╔════════════════════════╗
║   Welcome to Python!   ║
╚════════════════════════╝

Design 3: Diamond
    *
   * *
  *   *
 *     *
  *   *
   * *
    *
```

### Starter Code:

### Challenge: Print Your Name in ASCII

```
# Example: A-S-C-I-I (using letters made from symbols)

# A
print("  *  ")
print(" * * ")
print("*****")
print("*   *")
print("*   *")

```

## What's Next?

Next module: **Input Statement** - How to get information from the user, not just print to them!

---

## References

- Escape Sequences: https://docs.python.org/3/reference/lexical_analysis.html#string-and-bytes-literals
- Python Print Function: https://docs.python.org/3/library/functions.html#print
- F-Strings: https://peps.python.org/pep-0498/

