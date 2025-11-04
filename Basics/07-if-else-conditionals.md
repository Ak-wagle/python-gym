# Module 3.1: If-Else Conditional Statements

Conditionals let your program **make decisions**. Instead of doing the same thing every time, your code can behave differently based on conditions.

## The If Statement: "If something is true, do this"

### Basic If

```python
age = 20

if age >= 18:
    print("You are an adult")

# If the condition is false, nothing happens
```

### If-else: "If true, do this. Otherwise, do that"

```python
age = 15

if age >= 18:
    print("You are an adult")
else:
    print("You are a minor")
```

### if-elif-else: Multiple Conditions

```python
score = 85

if score >= 90:
    print("Grade: A")
elif score >= 80:
    print("Grade: B")
elif score >= 70:
    print("Grade: C")
else:
    print("Grade: F")
```

## Indentation: CRITICAL!

Python uses **indentation** (spaces) to show which code belongs to the if statement:

```python
# Correct - Indented code runs if condition is true
if age >= 18:
    print("Adult")
    print("Can vote")
print("This always runs")
```
```python
# WRONG - Missing indentation (error!)
if age >= 18:
print("Adult")  # IndentationError!
```

## Nested If Statements

Put if statements inside other if statements:

```python
age = 20
has_license = True

if age >= 18:
    print("You are an adult")
    if has_license:
        print("You can drive!")
    else:
        print("Get a license first")
else:
    print("You're too young")
```

## Comparison and Logical Operators

Use operators you learned in Module 2.1:

```python
age = 25
is_employed = True
has_saved = True

# Multiple conditions
if age >= 21 and is_employed:
    print("You can apply for loan")

# OR condition
if age < 13 or age > 65:
    print("Special pricing applies")

# NOT condition
if not is_employed:
    print("You need a job")
```

## The Ternary Operator: One-Line If-else

For simple if-else, use the ternary operator:

### Long way
```python
age = 20

if age >= 18:
    status = "Adult"
else:
    status = "Minor"
print(status)
```

### Short way
```python
age = 20
status = "Adult" if age >= 18 else "Minor"
print(status)
```

### Even more complex 😁
```python
message = "Can vote" if age >= 18 and is_citizen else "Cannot vote"
print(message)
```

## Practical Examples

### Login System

```python
username = input("Username: ")
password = input("Password: ")

if username == "admin" and password == "secret":
    print("Login successful! ")
else:
    print("Login failed! ")
```

### Temperature Guide

```python
temp = int(input("Temperature in Celsius: "))

if temp < 0:
    print("Freezing! ")
elif temp < 15:
    print("Cold - wear a jacket")
elif temp < 25:
    print("Nice weather")
elif temp < 35:
    print("Hot - drink water")
else:
    print("Way too hot! ")
```

### Ticket Price Calculator

```python
age = int(input("Age: "))
is_student = input("Are you a student? (yes/no): ") == "yes"

base_price = 15

if age < 12:
    price = base_price * 0.5  # Half price
    print(f"Child ticket: ${price}")
elif is_student:
    price = base_price * 0.75  # 25% discount
    print(f"Student ticket: ${price}")
elif age > 65:
    price = base_price * 0.7  # 30% discount
    print(f"Senior ticket: ${price}")
else:
    print(f"Regular ticket: ${base_price}")
```

## Common Mistakes


### ❌ Mistake 1: Forgetting Indentation

```python
# ERROR - Missing indentation
if age >= 18:
print("Adult")

# Correct - Indented
if age >= 18:
    print("Adult")
```

### ❌ Mistake 2: Unnecessary Extra Logic

```python
# Overcomplicated
if age >= 18 and age < 65:
    is_working_age = True
else:
    is_working_age = False

# Simpler
is_working_age = 18 <= age < 65

# Or with ternary
is_working_age = True if 18 <= age < 65 else False
```
## Milestone Task: Magic Forest Adventure - Choose Your Path

### Requirements:

- Present a fun scenario and ask the user to choose their path.
- Use if-elif-else statements to handle different choices.
- Provide different outcomes based on the user's selection (e.g., winning or game over).
- Make the game entertaining and easy to understand (at least 2-3 decision points).
- Include some ASCII art or nice formatting to make it visually appealing.
- Some choices should lead to a "Game Over," while others should lead to victory.

### Example Output
```python
╔======================================╗
║        MAGIC FOREST ADVENTURE        ║
╚======================================╝

You find yourself standing at the edge of a magical forest...
There are three paths ahead of you, each leading to a new adventure.

1. A path with sparkling rainbow flowers
2. A path with colorful mushrooms and glowing lights
3. A dark path with strange whispers coming from the trees

Which path do you take? (1-3): 2

You walk down the mushroom path and find a friendly gnome...
He gives you a magical key that opens a hidden treasure chest!
YOU WIN! 
```

## What's Next?

Next module: **Match-Case Statements** - A cleaner way to handle many conditions (Python 3.10+)!

---

## References

- Conditional Statements: https://docs.python.org/3/tutorial/controlflow.html#if-statements
- Python If-Else: https://www.w3schools.com/python/python_conditions.asp

