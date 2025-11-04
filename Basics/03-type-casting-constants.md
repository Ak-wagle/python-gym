# Module 1.3: Type Casting & Constants

Type casting is converting data from one type to another. It's like translating between languages - you're telling Python "treat this as a different type."

## Why Type Casting?

When users give you input, it comes as **text (string)**. If you want to do math with it, you need to convert it to a **number**.

```python
# User enters: "20"
age_text = "20"          # This is a string

# But we want it as a number:
age_number = int(age_text)  # Convert to integer: 25

# Now we can do math
next_year = age_number + 1  # 26

# But
next_year = age_text + 1  # ERROR! Can't add string + int
```

## Four Main Type Conversion Functions

### 1. int() - Convert to Integer

```python
# From string
num = int("42")
print(num)          # 42
print(type(num))    # <class 'int'>

# From float (removes decimal)
num = int(3.99)
print(num)          # 3 (not rounded, just truncated)

# From boolean
num = int(True)
print(num)          # 1
num = int(False)
print(num)          # 0
```

### 2. float() - Convert to Float

```python
# From string
price = float("19.99")
print(price)        # 19.99
print(type(price))  # <class 'float'>

# From integer
temperature = float(25)
print(temperature)  # 35.0 (now it has decimal)

# From string with integer
value = float("100")
print(value)        # 100.0
```

### 3. str() - Convert to String

```python
# From integer
num = 42
text = str(num)
print(text)         # "42"
print(type(text))   # <class 'str'>

# From float
pi = str(3.14)
print(pi)           # "3.14"

# From boolean
result = str(True)
print(result)       # "True"
```

### 4. bool() - Convert to Boolean

Any value can be converted to True or False:

```python
# Non-zero numbers = True
print(bool(1))      # True
print(bool(-5))     # True
print(bool(0.001))  # True

# Zero = False
print(bool(0))      # False
print(bool(0.0))    # False

# Non-empty strings = True
print(bool("hello"))    # True
print(bool("0"))        # True (it's not zero, it's text)

# Empty string = False
print(bool(""))         # False

# None = False
print(bool(None))       # False
```

## Example: User Input

In real world this is where type casting shines:

```python
# Get user's age (which comes as text)
age_text = input("How old are you? ")  # User types: 20

# Convert to integer
age = int(age_text)

# Now we can do math
birth_year = 2025 - age
print(f"You were born in {birth_year}")
```

Or combined:

```python
age = int(input("How old are you? "))  # Convert while getting input
birth_year = 2025 - age
print(f"You were born in {birth_year}")
```

## Common Mistakes

### ❌ Mistake 1: Converting Invalid String to Number

```python
num = int("hello")  # ERROR! Can't convert text to number
```

**Fix**: Make sure the string contains a valid number
```python
num = int("123")  # Works
```

### ❌ Mistake 2: Forgetting Type Conversion with User Input

```python
num1 = input("Enter number 1: ")  # "5" (string)
num2 = input("Enter number 2: ")  # "3" (string)
result = num1 + num2
print(result)  # "53" (string concatenation, not math!)
```

**Fix**: Convert to numbers first
```python
num1 = int(input("Enter number 1: "))
num2 = int(input("Enter number 2: "))
result = num1 + num2
print(result)  # 8 (actual math)
```

### ❌ Mistake 3: Converting Float to Int Loses Precision

```python
price = int("19.99")  # ERROR! int() can't convert string with decimal
```

**Fix**: Use float first, then int if needed
```python
price = float("19.99")  # 19.99 
price_int = int(price)  # 19 
```

## Constants in Python

A **constant** is a variable that **shouldn't change** after being set. By convention, use UPPERCASE_NAMES:

```python
# Constants (don't change these!)
PI = 3.14159
GRAVITY = 9.8
MAX_STUDENTS = 30
SPEED_OF_LIGHT = 3e8  # 300,000,000

# Regular variables (can change)
temperature = 25
temperature = 30  # OK to change

# Constants (shouldn't change)
PI = 3.14159
PI = 3.14  # Technically works, but BAD PRACTICE!
```

## Using Constants

```python
# Circle calculations using constants
PI = 3.14159
RADIUS = 5

# Calculate area
area = PI * (RADIUS ** 2)
print(f"Area: {area}")

# Calculate circumference
circumference = 2 * PI * RADIUS
print(f"Circumference: {circumference}")
```

## Temperature Conversion Program

A practical example combining type casting:

```python
# User input as string
celsius_str = input("Enter temperature in Celsius: ")

# Convert to number
celsius = float(celsius_str)

# Define conversion constant
CONVERSION_FACTOR = 9/5
OFFSET = 32

# Convert to Fahrenheit
fahrenheit = (celsius * CONVERSION_FACTOR) + OFFSET

# Convert back to string for display
print(f"{celsius}°C = {fahrenheit}°F")
```

## Milestone Task: Unit Converter

Create a program that converts between different units!

### Requirements:
- Create constants for conversion factors
- Ask user for input (gets as string)
- Convert input to appropriate type
- Perform conversion calculation
- Display result with original and converted values
- Make it pretty!

### Example Output:

```
╔════════════════════════════════════════╗
║       UNIT CONVERTER - MILES TO KM     ║
╚════════════════════════════════════════╝

Enter distance in miles: 5
────────────────────────────────────────
5.0 miles = 8.05 kilometers
────────────────────────────────────────
```

## What's Next?

Next, you'll learn about **comments, escape sequences, and print customization** - ways to make your output look professional and add notes to your code!

---

## References

- Python Type Conversions: https://docs.python.org/3/library/functions.html
- Type Casting Tutorial: https://www.w3schools.com/python/python_casting.asp

