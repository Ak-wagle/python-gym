# Module 4.3: Break, Continue & Pass

These three keywords **control the flow inside loops** - they change what happens during iteration without changing the main loop structure.

**Three Loop Control Statements:**

1. **`break`** - Immediately exits/terminates the loop entirely. Any code after the loop then executes.
2. **`continue`** - Skips the rest of the current iteration and jumps to the next iteration
3. **`pass`** - Does nothing (placeholder). Used when Python requires code but you don't want to do anything yet.

**Technical Impact:**
- `break`: Breaks the loop → execution goes to code AFTER the loop
- `continue`: Skips to next iteration → execution goes to the loop condition check
- `pass`: Does nothing → execution continues normally

---

## What is Break?

`break` **exits the loop immediately**, even if the condition is still True.

```python
# Without break - runs all 5 iterations
for i in range(5):
    print(i)  # 0, 1, 2, 3, 4

# With break - stops early when i == 2
for i in range(5):
    if i == 2:
        break  # Exit loop here
    print(i)  # 0, 1
print("Loop ended")  # This runs after break
```

## What is Continue?

`continue` **skips the rest of the current iteration** and goes to the next one.

```python
# Without continue - prints all numbers
for i in range(5):
    print(i)  # 0, 1, 2, 3, 4

# With continue - skips printing 2
for i in range(5):
    if i == 2:
        continue  # Skip to next iteration
    print(i)  # 0, 1, 3, 4 (2 is skipped!)
```

## What is Pass?

`pass` is a **placeholder** - it does nothing. Python requires at least one statement in a code block. Use `pass` when you don't have code yet.

```python
# ERROR - empty code block
while True:
    if some_condition:
        # Nothing here!

# FIX - use pass as placeholder
while True:
    if some_condition:
        pass  # TODO: Add code later

# Another use - defining empty function (learn more in Module 6.1)
def my_function():
    pass  # I'll write this later!
```

---

## Practical Examples: Break

### Example: Search Until Found

```python
# Find a specific number in a list
numbers = [5, 12, 8, 15, 3, 9, 20]
target = 15

for num in numbers:
    print(f"Checking {num}")
    if num == target:
        print(f"Found {target}!")
        break  # Stop searching when found
    else:
        print(f"Not it, continue searching")

# Output:
# Checking 5
# Not it, continue searching
# Checking 12
# Not it, continue searching
# Checking 8
# Not it, continue searching
# Checking 15
# Found 15!
```

---

## Practical Examples: Continue

### Example: Skip Even Numbers

```python
# Print only odd numbers
for i in range(10):
    if i % 2 == 0:
        continue  # Skip even numbers
    print(i)  # 1, 3, 5, 7, 9
```
---

## Practical Examples: Pass

### Example: Placeholder for Future Code

```python
# You're building a program, but not ready to code everything yet
def process_data():
    pass  # TODO: Write data processing code

def save_to_file():
    pass  # TODO: Write file saving code

def display_results():
    pass  # TODO: Write display code

# Test the structure first, fill in code later
process_data()
save_to_file()
display_results()
```

---


## Nested Loops with Break/Continue

```python
# Find first occurrence in 2D grid
grid = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

target = 6
found = False

for row in grid:
    for num in row:
        if num == target:
            print(f"Found {target}!")
            found = True
            break  # Break inner loop only!
    if found:
        break  # Break outer loop

print("Done searching")
```

**Important**: `break` only breaks the **innermost loop** it's in!

---

## Common Mistakes

### ❌ Mistake 1: Using Break Outside Loop

```python
# ERROR - break not in a loop
if x > 5:
    break  # SyntaxError! break must be inside loop

# Correct - break inside loop
while True:
    if x > 5:
        break
```

### ❌ Mistake 2: Pass vs Do Nothing

```python
# ERROR - can't leave empty
if condition:
    # Nothing here causes error

# Fix - use pass
if condition:
    pass  # Placeholder

# If you have code, don't use pass
if condition:
    pass  # Unnecessary!
    print("Something")  # This is the real code
```


## Milestone Task: Interactive Menu System

Create a complete menu-driven program using all three loop control statements!

### Requirements:
- Display menu loop (while loop with break)
- Skip invalid options (continue)
- Use pass for future features
- Handle user choices
- Add at least 3 menu options
- Include statistics/counter

### Example Output:

```
════════════════════════════════════════
MAIN MENU
════════════════════════════════════════
1. Play a Game
2. View Settings
3. View Statistics
4. Exit
════════════════════════════════════════
Enter choice (1-4): 5
Invalid choice! Please enter 1-4

════════════════════════════════════════
MAIN MENU
════════════════════════════════════════
1. Play a Game
2. View Settings
3. View Statistics
4. Exit
════════════════════════════════════════
Enter choice (1-4): 3

Statistics
Selections made: 0
Invalid choices: 1

════════════════════════════════════════
```

---

## What's Next?

Next module: **Strings (Advanced)** - Working with text in powerful ways!

---

## References

- Break and Continue: https://docs.python.org/3/tutorial/controlflow.html#break-and-continue-statements-and-else-clauses-on-loops
- Pass Statement: https://docs.python.org/3/reference/simple_stmts.html#pass

