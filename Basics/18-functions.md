# Module 6.1: Defining & Calling Functions

A **function** is a reusable block of code that performs a specific task. Functions are the foundation of programming organization - they allow you to write code once and use it many times, reducing repetition and improving code maintainability. A function consists of a definition (where you write what it does) and calls (where you use it).

**Key Technical Properties:**
- **Reusable**: Define once, call many times
- **Organized**: Groups related code together
- **Maintainable**: Changes in one place fix everywhere
- **Modular**: Functions can call other functions
- **Returns values**: Can send data back to caller
- **Parameters**: Accept input data
- **Scope**: Variables inside functions are isolated

**Why This Matters**: In robotics, functions organize robot behaviors (move_forward, turn_left, read_sensor). Functions are essential for complex programs and are the foundation for Classes (you'll learn in OOP Module).

---

## What is a Function?

A function is a block of reusable code. Instead of writing the same code over and over, write it once in a function, then **call** it whenever needed.

### Without Functions (Repetitive)

```python
# Calculate goal scoring streak (without functions)
player1_name = "Cristiano Ronaldo"
player1_goals = 50
print(f"{player1_name} scored {player1_goals} goals")

player2_name = "Lionel Messi"
player2_goals = 45
print(f"{player2_name} scored {player2_goals} goals")

player3_name = "Robert Lewandowski"
player3_goals = 48
print(f"{player3_name} scored {player3_goals} goals")
```

### With Functions (Clean)

```python
def display_stats(name, goals):
    """Display player statistics"""
    print(f"{name} scored {goals} goals")

# Now use the function
display_stats("Cristiano Ronaldo", 50)
display_stats("Lionel Messi", 45)
display_stats("Robert Lewandowski", 48)
```

Much cleaner!

---

## Defining Functions

### Basic Function Syntax
The `def` keyword is used to define a function. It’s short for "define" and marks the start of a function definition

```python
def function_name(parameters):
    """Documentation string (docstring)"""
    # Function code here
    # Do something
    return result

# Call the function
output = function_name(arguments)
```
- `def`: This keyword tells Python you are defining a function.

- `function_name`: The name of the function. Follow standard naming conventions (e.g., lowercase with underscores).

- `parameters`: The inputs the function will accept. These are optional but allow flexibility.

- `return`: Sends back the result from the function to the caller.

### Example: Simple Function

```python
def greet_player(name):
    """Greet a player by name"""
    message = f"Welcome, {name}!"
    print(message)
    return message

# Call the function
greet_player("Serena Williams")  # Welcome, Serena Williams!
result = greet_player("Virat Kohli")  # Welcome, Virat Kohli!
print(result)  # "Welcome, Virat Kohli!"
```

### Docstrings (Documentation)

Always document your functions:

```python
def calculate_average(numbers):
    """
    Calculate average of a list of numbers.
    
    Args:
        numbers: List of integers or floats
    
    Returns:
        Float: The average value
    
    Example:
        >>> calculate_average([10, 20, 30])
        20.0
    """
    if not numbers:
        return 0
    return sum(numbers) / len(numbers)
```

---

## Return Statements

### Returning Values

```python
def add(a, b):
    """Add two numbers"""
    result = a + b
    return result

sum_result = add(5, 3)
print(sum_result)  # 8

# One-liner
def multiply(x, y):
    return x * y

product = multiply(4, 7)
print(product)  # 28
```

### Returning Multiple Values (Tuple)

```python
def get_athlete_stats(name):
    """Return athlete statistics"""
    if name == "Michael Phelps":
        return name, 28, "Swimming"  # Returns tuple
    elif name == "Usain Bolt":
        return name, 8, "Track & Field"
    else:
        return name, 0, "Unknown"

# Unpack the tuple
name, medals, sport = get_athlete_stats("Michael Phelps")
print(f"{name} won {medals} medals in {sport}")
# Michael Phelps won 28 medals in Swimming
```

### Early Return (Exit Function Early)

```python
def check_player_eligibility(age, experience):
    """Check if player is eligible"""
    if age < 18:
        return False  # Exit early
    if experience < 2:
        return False  # Exit early
    return True  # Reached if both conditions passed

print(check_player_eligibility(25, 5))  # True
print(check_player_eligibility(16, 10)) # False
```

---

## Function Parameters

### Required Parameters

```python
def calculate_bmi(weight, height):
    """Calculate Body Mass Index"""
    bmi = weight / (height ** 2)
    return bmi

result = calculate_bmi(75, 1.80)  # Must provide both
print(f"BMI: {result:.2f}")  # BMI: 23.15
```

### Default Parameters

```python
def greet(name, greeting="Hello"):
    """Greet someone with optional greeting"""
    return f"{greeting}, {name}!"

print(greet("Rafael Nadal"))  # Hello, Rafael Nadal!
print(greet("Rafael Nadal", "Hola"))  # Hola, Rafael Nadal!
```

### Parameters vs Arguments

```python
# Parameters: Used in function definition
def player_info(name, sport):  # name and sport are PARAMETERS
    return f"{name} plays {sport}"

# Arguments: Values passed when calling
player_info("Sachin Tendulkar", "Cricket")  # These are ARGUMENTS
```

**Note about `*args` and `**kwargs`**: You'll learn these in Module 6.2. For now, just know they allow flexible parameters.

---

## Practical Examples

### Example 1: Grade Calculator

```python
def calculate_grade(score):
    """Determine grade from score"""
    if score >= 90:
        return "A"
    elif score >= 80:
        return "B"
    elif score >= 70:
        return "C"
    elif score >= 60:
        return "D"
    else:
        return "F"

# Test with students' exam scores
students = {
    "Simone Biles": 95,
    "Shaquille O'Neal": 78,
    "Mia Hamm": 88,
    "Roger Federer": 92
}

for student, score in students.items():
    grade = calculate_grade(score)
    print(f"{student}: {score} ({grade})")
```

### Example 2: Distance Calculator

```python
def calculate_distance(x1, y1, x2, y2):
    """Calculate distance between two points"""
    import math
    distance = math.sqrt((x2 - x1)**2 + (y2 - y1)**2)
    return distance

# Check distance between two locations
loc1 = (0, 0)      # Stadium location
loc2 = (3, 4)      # Training ground

dist = calculate_distance(loc1[0], loc1[1], loc2[0], loc2[1])
print(f"Distance: {dist:.2f} km")  # Distance: 5.00 km
```

**Note about `import math`**: You'll learn imports in Module 7.1. For now, just know it gives access to math functions.

---

## Common Mistakes

### ❌ Mistake 1: Forgetting `return` Statement

```python
# Function doesn't return anything
def add_numbers(a, b):
    result = a + b
    # Missing return!

output = add_numbers(5, 3)
print(output)  # None

# Add return
def add_numbers(a, b):
    result = a + b
    return result  # Now returns 8

output = add_numbers(5, 3)
print(output)  # 8
```

### ❌ Mistake 2: Function Called Before Definition

```python
# ERROR - calling before defining
greet("Serena")

def greet(name):
    print(f"Hello, {name}!")

# Define first, then call
def greet(name):
    print(f"Hello, {name}!")

greet("Serena")
```

### ❌ Mistake 3: Wrong Number of Arguments

```python
def calculate_average(a, b):
    return (a + b) / 2

# Provides 3 arguments, function expects 2
average = calculate_average(10, 20, 30)  # TypeError!

# Provide correct number
average = calculate_average(10, 20)  # 15
```

### ❌ Mistake 4: Variables Inside Function Don't Exist Outside

```python
def get_athlete_name():
    athlete = "Usain Bolt"  # Variable inside function
    return athlete

# Can't access athlete here
print(athlete)  # NameError!

# Get it from return value
name = get_athlete_name()
print(name)  # "Usain Bolt"
```

---

## Milestone Task: Build Your Command-Line Calculator
Create a simple calculator program that performs basic math operations using functions.

### Requirements:

1. Create four functions: `add()`, `subtract()`, `multiply()`, `divide()`
2. Each function should take two numbers and return the result
3. Ask the user which operation they want to perform
4. Get two numbers from the user
5. Print the result in a clean, readable format
6. Handle division by zero correctly

### Example Output:

```
╔══════════════════════════════════════╗
║           SIMPLE CALCULATOR          ║
╚══════════════════════════════════════╝

Select Operation:
1. Add
2. Subtract
3. Multiply
4. Divide
5. Exit
Enter choice: 2
Enter first number: 3
Enter second number: 2

──────────────────────────────────────
Result: 3.0 - 2.0 = 1.0
──────────────────────────────────────

```

---

## What's Next?

Next module: **Function Arguments** - Advanced parameter techniques (defaults, *args, **kwargs)!

---

## References

- Functions: https://docs.python.org/3/tutorial/controlflow.html#defining-functions
- Docstrings: https://docs.python.org/3/tutorial/controlflow.html#more-on-defining-functions
- Return Statement: https://docs.python.org/3/reference/simple_stmts.html#return

