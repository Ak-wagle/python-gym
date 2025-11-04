# Module 1.5: Input Statement & User Interaction

Your programs have been one-directional so far - they only print output. Now learn how to get information FROM users, not just print TO them!

## What is the input() Function?

`input()` is a function that pauses your program, asks the user for information, and returns what they typed as a **string**.

## Basic Input

### Simple Input

```python
name = input("What is your name? ")
print(f"Hello, {name}!")
```

Run this and you'll see:
```
What is your name? Wagle
Hello, Wagle!
```

### Multiple Inputs

```python
first_name = input("Enter first name: ")
last_name = input("Enter last name: ")
age = input("Enter age: ")

print(f"\nYour name: {first_name} {last_name}")
print(f"Your age: {age}")
```

## Remember: input() Returns a STRING!

This is the biggest thing to remember:

```python
# User types: 55
age = input("How old are you? ")
print(type(age))  # <class 'str'> - It's TEXT, not a number!
```

## The Golden Rule: Convert Input When Needed

```python
# Pattern you'll use constantly:
user_input = input("Enter a number: ")
number = int(user_input)  # Convert to use for math
result = number * 2
print(result)
```

```python
# Or shortcut (combine them):
number = int(input("Enter a number: "))
result = number * 2
print(result)
```

## Practical Example: Simple Calculator

```python
# Get two numbers
num1 = int(input("Enter first number: "))
num2 = int(input("Enter second number: "))

# Calculate
sum = num1 + num2
product = num1 * num2
average = (num1 + num2) / 2

# Display
print(f"\nSum: {sum}")
print(f"Product: {product}")
print(f"Average: {average}")
```

## Input with Formatting

Make input prompts clear and user-friendly:

```python
# Good prompts tell the user what format you want
age = int(input("Enter your age (number only): "))
email = input("Enter your email (e.g., name@example.com): ")
year = int(input("Enter birth year (e.g., 1999): "))

# Add visual separation
print("\n" + "=" * 30)
print("YOUR INFO")
print("=" * 30)
print(f"Age: {age}")
print(f"Email: {email}")
print(f"Birth Year: {year}")
```

## Common Mistakes

### ❌ Mistake 1: Forgetting input() Returns a String

```python
age = input("How old are you? ")
next_year_age = age + 1  # ERROR!
```

**Fix**: Convert to number
```python
age = int(input("How old are you? "))
next_year_age = age + 1  #  Works!
```

### ❌ Mistake 2: Converting Invalid Input

```python
# User types: "hello"
number = int(input("Enter a number: "))  #  ERROR! "hello" isn't a number
```

**What happens**: The program crashes with `ValueError`

**Later you'll learn**: Try-except blocks to handle this gracefully

### ❌ Mistake 3: Not Converting When Needed

```python
# User types: "5" and "3"
num1 = input("Number 1: ")  # "5" (string)
num2 = input("Number 2: ")  # "3" (string)
result = num1 + num2
print(result)  # "53" - String concatenation, not addition!
```

**Fix**: Convert before adding
```python
num1 = int(input("Number 1: "))
num2 = int(input("Number 2: "))
result = num1 + num2
print(result)  # 8 - Actual math!
```

### ❌ Mistake 4: Empty Input Causing Errors

```python
# User just presses Enter without typing anything
age = int(input("Age: "))  #  ERROR! Empty string can't convert to int
```

**Later fix**: Validation and try-except blocks

## Interactive Program Example

```python
print("╔════════════════════════════════════════╗")
print("║         WELCOME TO PIZZA SHOP          ║")
print("╚════════════════════════════════════════╝")
print()

# Get customer name
customer_name = input("What's your name? ")

# Get pizza size
print("\nPizza Sizes:")
print("1. Small - $10")
print("2. Medium - $15")
print("3. Large - $20")
size = input("Choose (1-3): ")

# Get quantity
quantity = int(input("How many pizzas? "))

# Calculate based on selection
if size == "1":
    price = 10
elif size == "2":
    price = 15
else:
    price = 20

total = price * quantity

# Display order
print("\n" + "=" * 40)
print(f"Order for: {customer_name}")
print(f"Quantity: {quantity}")
print(f"Price per pizza: ${price}")
print(f"TOTAL: ${total}")
print("=" * 40)
```

##  Milestone Task: Personal Information Collector

Create a program that collects user information and displays it in a formatted profile!

### Requirements:
- Ask for at least 5 pieces of information (name, age, email, city, hobby)
- Convert input to appropriate types where needed
- Display a formatted profile with all information
- Make it visually appealing with separators and formatting
- Calculate something (like years until retirement: 60 - age)

### Example Output:

```
╔════════════════════════════════════════════════╗
║          WELCOME TO PROFILE BUILDER            ║
╚════════════════════════════════════════════════╝

Please answer a few questions about yourself...

Name: Leonardo Da Vinci
Age: 56
Email: leo@gmail.com
City: Vinci
Favorite Hobby: Painting

╔════════════════════════════════════════════════╗
║                 YOUR PROFILE                   ║
╚════════════════════════════════════════════════╝

Full Name: Leonardo Da Vinci
Current Age: 56
Email Address: leo@gmail.com
Location: Vinci
Hobby: Painting

Years until retirement (age 60): 4

Thank you for using Profile Builder!
```

## What's Next?

Next module: **Operators** - Learn all the different operations you can do (+, -, *, /, ==, and, or, etc.)!

---

## References

- Python input() function: https://docs.python.org/3/library/functions.html#input
- User Input Guide: https://www.w3schools.com/python/python_user_input.asp

