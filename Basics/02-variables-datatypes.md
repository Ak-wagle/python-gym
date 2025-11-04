# Module 1.2: Variables & Data Types

Variables are like **labeled boxes** where your program stores information. Think of them as containers that hold data your program can use, modify, and reference.

## What is a Variable?

A variable is a name you assign to a value. When you create a variable, you're telling Python: "Remember this value and call it by this name."

```python
name = "Newton"
age = 20
```

Now Python "remembers" that `name` contains `"Newton"` and `age` contains `25`. You can use these variables anywhere in your code!

## Why Variables?

Without variables, you'd have to write:

```python
print("Hello, Newton!")
print("Newton is 20 years old")
print("Newton studies Python")
```

With variables, it's way cleaner:

```python
name = "Newton"
age = 20
print(f"Hello, {name}!")
print(f"{name} is {age} years old")
print(f"{name} studies Python")
```

## Naming Variables

Good variable names make code readable:

### ✅ Good Names
```python
student_name = "Newton"
user_age = 20
total_price = 99.99
is_enrolled = True
```

### ❌ Bad Names
```python
n = "Newton"               # Too short, unclear
studentsname = "Newton"    # No underscore, hard to read
AGE = 25                   # ALL CAPS (reserved for constants)
x = 99.99                  # Meaningless
```
**Attention!** Python might let you use these bad names, but good variable names make your code easier to read and maintain. Whether it's for you or someone else, clear names prevent confusion and save time in the long run. Keep it simple and descriptive!

### Naming Rules

Python variable names must follow these rules:

1. **Start with letter or underscore** - `_name`, `name123` ✅ | `123name` ❌
2. **Only letters, numbers, underscores** - `user_name_123` ✅ | `user-name` ❌
3. **Case sensitive** - `name` and `Name` are different variables
4. **Can't be reserved words** - `for`, `if`, `while`, `class`, etc. are reserved
5. **Use snake_case** - `my_variable` (not `myVariable` or `MyVariable`)

## Five Basic Data Types

Python has different data types for different kinds of information:

### 1. Integer (int)

```python
age = 20
temperature = -10
population = 7800000000

print(age)          # 20
```

The type() function tells you the data type of the variable or value passed to it.

```python
print(type(age))    # <class 'int'>
```

### 2. Float (float) - Decimal Numbers

```python
height = 5.9
pi = 3.14159
price = 19.99

print(height)       # 5.9
print(type(price))  # <class 'float'>
```

### 3. String (str) - Text

```python
name = "Newton"
city = 'New York'
message = "Python is fun!"

print(name)         # Newton
print(type(name))   # <class 'str'>
```

### 4. Boolean (bool) - True or False

```python
is_student = True
is_working = False
has_license = True

print(is_student)        # True
print(type(is_student))  # <class 'bool'>
```

### 5. None (NoneType) - No Value

```python
result = None       # Means "no value yet"

print(result)       # None
print(type(result)) # <class 'NoneType'>
```

## Creating and Using Variables

### Single Assignment

```python
username = "Tommy"
print(username)     # Tommy
```

### Multiple Assignment

```python
x = 10
y = 20
z = 30
```

Or multiple assignments on one line:

```python
a, b, c = 1, 2, 3
print(a, b, c)      # 1 2 3
```

### Swapping Variables

```python
x = 5
y = 10
x, y = y, x  # Swap them!
print(x, y)  # 10 5
```

## Modifying Variables

Variables can be changed:

```python
score = 0
print(score)  # 0

score = 100
print(score)  # 100

score = score + 10
print(score)  # 110
```

## Checking Data Type

Use the `type()` function to see what type a variable is:

```python
print(type(42))           # <class 'int'>
print(type(3.14))         # <class 'float'>
print(type("hello"))      # <class 'str'>
print(type(True))         # <class 'bool'>
print(type(None))         # <class 'NoneType'>
```

## Common Mistakes

### ❌ Mistake 1: Using Variable Before Creating It

```python
print(age)  # NameError! age doesn't exist yet
age = 20
```

**Fix**: Create the variable first
```python
age = 20
print(age)  # 20
```

### ❌ Mistake 2: Confusing Assignment (=) with Comparison (==)

```python
name = "Newton"  # Assignment - sets value
name == "Newton" # Comparison - checks if equal (returns True/False)
```

### ❌ Mistake 3: Using Reserved Words

```python
class = "Python101"  # ERROR! 'class' is reserved
```

**Fix**: Use a different name
```python
course_name = "Python101"
```

### ❌ Mistake 4: Not Using Quotes for Strings

```python
name = Newton  # ERROR! Python thinks Newton is a variable name
print(name)
```

**Fix**: Add quotes
```python
name = "Newton"  # Now it's a string
print(name)
```

### ❌ Mistake 5: Inconsistent Variable Names

```python
student_name = "Newton"
print(studentname)  # ERROR! Typo - this variable doesn't exist
```

**Fix**: Use exact same name
```python
student_name = "Newton"
print(student_name)  # Correct!
```

## Variable Assignment Shortcuts

```python
# Normal
x = x + 5

# Shortcut (same result)
x += 5

# Other shortcuts
x -= 3    # x = x - 3
x *= 2    # x = x * 2
x /= 4    # x = x / 4
```

##  Milestone Task: Create Your Player Character

Create a program that defines a video game character's stats. Print them in a cool format!

### Requirements:
- Create variables for: character_name, level, health_points, mana_points, gold, is_alive
- Mix different data types (string, int, float, bool, etc.)
- Print a character status screen
- Show the type of each variable
- Make it look like a real game interface

### Example Output:

```
╔════════════════════════════════════════╗
║         CHARACTER STATUS SCREEN        ║
╚════════════════════════════════════════╝

Character Name: Goated_Warrior
Level: 42
Health Points: 150
Mana Points: 75.5
Gold: 5000
Alive: True

─────────────────────────────────────────
STATUS: Ready for Battle! ⚔️
─────────────────────────────────────────
```

## What's Next?

In the next module, you'll learn **type casting** - how to convert one data type to another. This is super useful when working with user input!

---

## References

- Python Data Types: https://docs.python.org/3/tutorial/introduction.html#numbers
- Variable Naming Conventions: https://pep8.org/#naming-conventions
