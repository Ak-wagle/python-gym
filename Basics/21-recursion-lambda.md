# Module 6.4: Recursion & Lambda Functions

**Recursion** is when a function calls itself to solve a problem by breaking it into smaller subproblems. Every recursive function needs a base case (when to stop) and a recursive case (calling itself).

**Lambda functions** are small anonymous functions defined with `lambda` keyword - useful for simple operations passed to other functions. Both are powerful advanced techniques.

**Key Technical Properties (Recursion):**
- **Base case**: Condition that stops recursion
- **Recursive case**: Function calls itself with simpler input
- **Stack**: Each call uses memory (deep recursion can overflow)
- **Mathematical**: Natural for mathematical problems (factorial, fibonacci)

**Key Technical Properties (Lambda):**
- **Anonymous**: No `def name`, just lambda expression
- **Single expression**: Only one line of code
- **Returns immediately**: Implicit return
- **Inline**: Used where simple functions are needed

---

## Recursion Basics

### Simple Recursion: Countdown

```python
def countdown(n):
    """Recursively count down from n"""
    if n == 0:  # BASE CASE - stops recursion
        print("Done! ")
        return
    
    print(n)
    countdown(n - 1)  # RECURSIVE CASE - calls itself

countdown(5)
# Output: 5, 4, 3, 2, 1, Done!
```

### Factorial (Classic Recursion)

```python
def factorial(n):
    """Calculate factorial recursively (n!)"""
    # BASE CASE
    if n <= 1:
        return 1
    
    # RECURSIVE CASE
    return n * factorial(n - 1)

print(factorial(5))   # 120 (5*4*3*2*1)
print(factorial(0))   # 1
print(factorial(10))  # 3628800
```

**How it works:**
```
factorial(5)
  = 5 * factorial(4)
  = 5 * 4 * factorial(3)
  = 5 * 4 * 3 * factorial(2)
  = 5 * 4 * 3 * 2 * factorial(1)
  = 5 * 4 * 3 * 2 * 1  = 120
```

### Fibonacci Sequence

```python
def fibonacci(n):
    """Get nth fibonacci number"""
    if n <= 1:
        return n
    return fibonacci(n - 1) + fibonacci(n - 2)

for i in range(10):
    print(fibonacci(i), end=" ")
# 0 1 1 2 3 5 8 13 21 34
```
---

## Lambda Functions

### Basic Lambda Syntax

```python
# Traditional function
def double(x):
    return x * 2

# Lambda equivalent
double = lambda x: x * 2

print(double(5))  # 10

# One-liner lambda
add = lambda x, y: x + y
print(add(3, 4))  # 7
```

### When to Use Lambda

Lambda is useful when you need a simple function for a short time:

```python
# Lambda with map (apply function to each item)
prices = [10.00, 25.00, 15.50, 8.99]
with_tax = list(map(lambda p: p * 1.08, prices))
print(with_tax)  # [10.8, 27.0, 16.74, 9.71]

# Lambda with filter (keep items where condition is true)
scores = [85, 45, 92, 38, 88, 55]
passing = list(filter(lambda s: s >= 60, scores))
print(passing)  # [85, 92, 88]

# Lambda with sorted (custom sorting)
products = [
    {"name": "Laptop", "price": 1200},
    {"name": "Phone", "price": 800},
    {"name": "Tablet", "price": 400}
]
by_price = sorted(products, key=lambda p: p["price"])
for product in by_price:
    print(f"{product['name']}: ${product['price']}")
```

**Note about `map` and `filter`**: You'll learn these comprehensively in Module 10.2. These are functional programming tools.

---

## Practical Examples

### Example: Data Processing with Lambda

```python
# Calculate metrics on data
sales_data = [
    {"product": "Laptop", "quantity": 5, "price": 1200},
    {"product": "Mouse", "quantity": 50, "price": 25},
    {"product": "Monitor", "quantity": 12, "price": 350},
    {"product": "Keyboard", "quantity": 30, "price": 75}
]

# Calculate revenue per item
revenue = list(map(
    lambda item: (item["product"], item["quantity"] * item["price"]),
    sales_data
))

# Filter high-revenue items
high_revenue = list(filter(
    lambda item: item[1] > 5000,
    revenue
))

print("High Revenue Items:")
for product, total in high_revenue:
    print(f"  {product}: ${total:,.2f}")

# Sort by revenue
sorted_revenue = sorted(revenue, key=lambda item: item[1], reverse=True)
print("\nRanked by Revenue:")
for product, total in sorted_revenue:
    print(f"  {product}: ${total:,.2f}")
```

---

## Common Mistakes

### ❌ Mistake 1: Missing Base Case (Infinite Recursion)

```python
# No base case - will crash!
def bad_recursion(n):
    return bad_recursion(n - 1)  # Never stops!

# Include base case
def good_recursion(n):
    if n == 0:  # BASE CASE
        return 0
    return n + good_recursion(n - 1)
```

### ❌ Mistake 2: Forgetting Return in Recursion

```python
# Doesn't combine results
def sum_wrong(numbers):
    if not numbers:
        return 0
    numbers[0] + sum_wrong(numbers[1:])  # Missing return!

# Return the recursive result
def sum_correct(numbers):
    if not numbers:
        return 0
    return numbers[0] + sum_correct(numbers[1:])
```

---

## When to Use What

| Technique | Best For | Example |
|-----------|----------|---------|
| Recursion | Divide & conquer, trees, nested data | Factorial, search |
| Lambda | Simple one-liners with map/filter/sort | `map(lambda x: x*2, list)` |
| Regular Functions | Complex logic, reuse | API processing, business logic |

---

## Milestone Task: Quick Temperature Converter

Use lambda functions to convert temperatures.

### Requirements:
- Create a lambda to convert Celsius → Fahrenheit

    `Formula: (C * 9/5) + 32`
- Create a lambda to convert Fahrenheit → Celsius

    `Formula: (F - 32) * 5/9`
- Ask the user which conversion they want
- Ask for the temperature value
- Print the converted result

### Example Output

```bash
Choose Conversion:
1. Celsius to Fahrenheit
2. Fahrenheit to Celsius

Enter temperature: 25
Result: 77.0 °F
```

## Milestone Task: Countdown Timer (Recursive)

Write a recursive function that counts down from a given number to 1.

### Requirements:

- Function name: `countdown(n)`
- If n is greater than 0, print it, then call `countdown(n-1)`
- When n reaches 0, print: "Countdown Complete!"
- Get the starting number from user input

### Example Output:
```bash
Enter starting number: 5
5
4
3
2
1
Countdown Complete!

```
---

## What's Next?

Next module: **Built-in Modules** - Using Python's standard libraries!

---

## References

- Recursion: https://docs.python.org/3/tutorial/controlflow.html#defining-functions
- Lambda: https://docs.python.org/3/tutorial/controlflow.html#lambda-expressions
- Map/Filter: https://docs.python.org/3/library/functions.html#map

