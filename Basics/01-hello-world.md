# Module 1.1: Hello World - The First Program

Welcome to Python! 

This is where every programmer's journey begins - the legendary "Hello, World!" program.

## What is Hello World?

"Hello, World!" is a simple program that prints text to the screen. It's tradition - like a secret handshake for programmers. When you run your first Hello World program, you've officially entered the world of coding!

## Your First Program

### Step 1: Create a File

Open VS Code and create a new file called `hello.py`

### Step 2: Write the Code

Type this exactly:

```python
print("Hello, World!")
```

That's it! That's your first Python program. 

### Step 3: Run the Program

In VS Code terminal, type:

```bash
python hello.py
```

You should see:

```
Hello, World!
```

## Understanding the Code

Let's break down what just happened:

```python
print("Hello, World!")
```

| Part | What it means |
|------|--------------|
| `print` | A built-in Python function that displays text |
| `(` `)` | Parentheses - tells Python this is a function call |
| `"Hello, World!"` | The text you want to print (the string) |

## Variations (Have Fun!)

Try modifying your program:

```python
# Print your name
print("My name is Newton!")

# Print multiple times
print("Hello!")
print("World!")
print("!")

# Print numbers
print(99)
print(3.14)

# Print a formula result
print(10 + 5)

# Empty line
print()

# Fancy text
print("🐍 Python is goated! 🐍")
```

## Common Mistakes

### ❌ Mistake 1: Missing Quotes

```python
print(Hello, World!)  # ERROR!
```

**Why it fails**: Python doesn't know "Hello" is text without quotes

**Fix**: 
```python
print("Hello, World!")
```

### ❌ Mistake 2: Wrong Quotes

```python
print('Hello, World!"')  # Mixed quotes!
```

**Why it fails**: Quotes must match (both single or both double)

**Fix**: 
```python
print("Hello, World!")
# or
print('Hello, World!')
```

### ❌ Mistake 3: Misspelled Function

```python
prnt("Hello, World!")  # Typo!
```

**Why it fails**: Python doesn't know what `prnt` means

**Fix**: It's `print`, not `prnt`

### ❌ Mistake 4: Missing Parentheses

```python
print "Hello, World!"  # Old Python 2 style (doesn't work in Python 3)
```

**Why it fails**: Python 3 requires parentheses

**Fix**:
```python
print("Hello, World!")
```

## How Print Works

The `print()` function:
1. Takes text (or numbers) as input
2. Displays it on your screen
3. Automatically moves to the next line

```python
print("Line 1")
print("Line 2")
print("Line 3")
```

Output:
```
Line 1
Line 2
Line 3
```

## Printing Different Things

### Strings (Text)

```python
print("This is a string")
print('Single or double quotes work')
```

### Numbers

```python
print(99)
print(3.14)
print(1000000)
```

### Mathematical Expressions

```python
print(10 + 5)      # Output: 15
print(10 - 3)      # Output: 7
print(10 * 2)      # Output: 20
print(10 / 2)      # Output: 5.0
```

### Multiple Things (Separated by Commas)

```python
print("I am", 21, "years old")
# Output: I am 21 years old

print("Apple", "Banana", "Cherry")
# Output: Apple Banana Cherry
```

##  Milestone Task: Profile Printer

Create a program that prints your profile information in a cool way!

### Requirements:
- Print your name
- Print your age
- Print your favorite programming language
- Print a fun fact about yourself
- Make it look interesting with extra lines and symbols

### Example Output:

```
╔════════════════════════╗
║   MY AWESOME PROFILE   ║
╚════════════════════════╝

Name: Guido van Rossum
Age: 69
Favorite Language: Python
Fun Fact: I can solve Rubik's cubes!

🐍 Ready to code! 🐍
```

## What's Next?

In the next module, you'll learn about **variables** - containers that store information your program can use and modify. This unlocks real programming power!

---

## References

- Python print() function: https://docs.python.org/3/library/functions.html#print
- VS Code Python setup: https://code.visualstudio.com/docs/python/python-tutorial

