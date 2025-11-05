# Module 4.1: For Loops & Iteration

Loops let you **repeat code** without writing it multiple times. A `for` loop repeats code a specific number of times.

## The range() Function

**What is range()?**

- range() is a built-in function in Python that generates a sequence of numbers.

- It returns an iterable object, meaning you can loop over it, but it does not create an array or a list unless you explicitly convert it.

Syntax:
```python
range(start, stop, step)
```

- start: The starting number (inclusive). Default is 0.

- stop: The number at which to stop (exclusive). The sequence will not include this number.

- step: The step between each number. Default is 1.

### range(stop) - Start at 0, go up to (but not including) stop
```python
r = range(10)
print(list(r))      # Output: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

### range(start, stop) - Start at start, go up to (not including) stop
```python
r = range(3, 9)
print(list(r))      # Output: [3, 4, 5, 6, 7, 8]
```

### range(start, stop, step) - Count by steps
```python
r = range(2, 10, 2)
print(list(r))      # Output: [2, 4, 6, 8]
```

### Backwards with negative step
```python
r = range(10, 0, -2)
print(list(r))      # Output: [10, 8, 6, 4, 2]
```

**Note:**

*You’ll see that we are using the keyword **list()** in these examples. Don’t worry too much about it for now, just think of it as a way to list the objects in that range. We'll dive into the **list()** function in more detail in future tutorials.*

**Awesome fact:**

Range objects are lazy: They don’t store all the numbers in memory; instead, they generate numbers as needed. This laziness makes them memory efficient.

## Basic For Loop

- The for loop in Python is used to iterate over a sequence (like a list, tuple, string, or range) and execute a block of code repeatedly for each item in that sequence.

- It's one of the most commonly used loops because it’s easy to read and write

**Example 1: Repeat something multiple times**
```python
# Repeat 5 times
for i in range(5):
    print("Hello!")
```
**What happens:**

- `range(5)` generates the numbers 0, 1, 2, 3, 4.

- The loop will run 5 times, and in each iteration, it will print "Hello!".

- The value of i starts at 0 and increments by 1 after each iteration until the loop has run 5 times.

- In this case, i is not used inside the loop; it just helps to control the number of iterations.

**Output**
```bash
Hello!
Hello!
Hello!
Hello!
Hello!
```
**Example 2: Loop with an index variable `(i)`**
```python
# i is the loop variable that changes with each iteration
for i in range(3):
    print(f"Iteration {i}")
```

**What happens:**

- `range(3)` generates the numbers 0, 1, 2.

- The loop will run 3 times, and the variable `i` will take the values 0, 1, 2 in successive iterations.

- `i` starts at 0 in the first iteration, then increments by 1 in each subsequent iteration until it reaches 2 (because range(3) stops at 3).

- Inside the loop, we use `i` to print the current iteration number (using f"Iteration {i}" to format the output).

**Output:**
```bash
Iteration 0
Iteration 1
Iteration 2
```

## Practical Examples

### Multiplication Table

```python
number = 5

print(f"Multiplication table for {number}:")
for i in range(1, 11):
    print(f"{number} × {i} = {number * i}")
```

### Sum of Numbers

```python
# Sum numbers 1 to 10
total = 0
for i in range(1, 11):
    total += i
print(f"Sum: {total}")  # 55
```
**Shortcut:** `sum(range(1, 11))`


### Print Pattern
1. Triangle pattern
```python
for i in range(1, 6):
    print("*" * i)
```
Output:
```bash
*
**
***
****
*****
```
2. Try Square pattern
```python
for i in range(1, 4):
    for j in range(1, 4):
        print("*", end=" ")
    print()  # New line after each row
```

## Common Mistakes

### ❌ Mistake 1: Off-by-One Error

```python
# User wants 5 iterations but gets 4!
for i in range(5):
    print(i)  # 0, 1, 2, 3, 4

# Remember: range() doesn't include the stop value!
# If you want 1-5, use range(1, 6)

for i in range(1, 6):
    print(i)  # 1, 2, 3, 4, 5 
```

### ❌ Mistake 2: Modifying Loop Variable Inside Loop

```python
# This is confusing and usually wrong
for i in range(5):
    print(i)
    i = 10  # Doesn't actually skip ahead! (Python ignores this)

# Better: Use break or continue (next module)
```

## Milestone Task: Number Pattern Generator

Create a program that generates cool number patterns!

### Requirements:
- Generate multiple patterns using for loops
- Use range() with different start/stop/step values
- Create both vertical and horizontal patterns
- Make it visually interesting

### Example Output:

```
╔════════════════════════════════════════╗
║       NUMBER PATTERN GENERATOR         ║
╚════════════════════════════════════════╝

Pattern 1: Numbers 1 to 10
1 2 3 4 5 6 7 8 9 10

Pattern 2: Even Numbers
2 4 6 8 10 12 14 16 18 20

Pattern 3: Countdown
10 9 8 7 6 5 4 3 2 1

Pattern 4: Squares
1² = 1  |  2² = 4  |  3² = 9  |  4² = 16  |  5² = 25

Pattern 5: Multiplication Table (5×5)
1 2 3 4 5
2 4 6 8 10
3 6 9 12 15
4 8 12 16 20
5 10 15 20 25

Statistics:
Total numbers generated: 50
Sum: 500
Average: 10.0
```

## What's Next?

Next module: **While Loops** - Repeat until a condition is met (unknown number of iterations)!

---

## References

- For Loops: https://docs.python.org/3/tutorial/controlflow.html#for-statements
- Range Function: https://docs.python.org/3/library/stdtypes.html#range

