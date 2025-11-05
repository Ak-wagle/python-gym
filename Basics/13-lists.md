# Module 5.2: Lists

A **list** is a **mutable, ordered collection** of items. "Mutable" means you can change, add, or remove elements after creation - unlike strings which are immutable. Lists are Python's most versatile data structure and store items in order with numerical indices starting at 0.

**Key Technical Properties:**
- **Ordered**: Items have positions (index 0, 1, 2, etc.)
- **Mutable**: Can modify items: `list[0] = new_value`
- **Heterogeneous**: Can contain different types: `[1, "hello", 3.14, True]`
- **Indexable**: Access by position: `list[0]` = first item
- **Sliceable**: Extract portions: `list[0:3]`
- **Iterable**: Loop through items
- **Dynamic**: Grow and shrink with `.append()` and `.remove()`

**Why This Matters**: Lists are critical for robotics - storing sensor readings, coordinate points, waypoints, task queues, etc.

---

## Creating Lists

```python
# Empty list
empty = []

# List with initial values
numbers = [1, 2, 3, 4, 5]
names = ["Alice", "Bob", "Charlie"]

# Mixed types (not recommended, but works)
mixed = [1, "hello", 3.14, True, None]

# Using list() constructor
digits = list(range(5))  # [0, 1, 2, 3, 4]
chars = list("ABC")      # ['A', 'B', 'C']

# Nested lists (list inside list)
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]
print(matrix[0])      # [1, 2, 3] (first row)
print(matrix[0][1])   # 2 (first row, second element)
```

**Note about `range()`**: You learned this in Module 4.1 for loops. `list(range(5))` converts it to a list.

---

## Accessing List Items

### Indexing

```python
fruits = ["apple", "banana", "cherry", "date"]

# Positive indexing (left to right)
print(fruits[0])    # "apple"
print(fruits[2])    # "cherry"

# Negative indexing (right to left)
print(fruits[-1])   # "date" (last)
print(fruits[-2])   # "cherry" (second to last)

# Index out of range
# print(fruits[10]) # IndexError!
```

### Slicing

```python
fruits = ["apple", "banana", "cherry", "date"]

print(fruits[0:2])      # ["apple", "banana"]
print(fruits[1:])       # ["banana", "cherry", "date"]
print(fruits[:3])       # ["apple", "banana", "cherry"]
print(fruits[::2])      # ["apple", "cherry"] (every 2nd)
print(fruits[::-1])     # ["date", "cherry", "banana", "apple"] (reversed)
```

---

## Modifying Lists

### Adding Items

```python
numbers = [1, 2, 3]

# Add single item at end
numbers.append(4)           # [1, 2, 3, 4]

# Add item at specific position
numbers.insert(1, 1.5)      # [1, 1.5, 2, 3, 4]

# Add multiple items (extends)
numbers.extend([5, 6])      # [1, 1.5, 2, 3, 4, 5, 6]

# Concatenate lists
new_list = numbers + [7, 8] # New list, doesn't modify original
```

### Removing Items

```python
numbers = [1, 2, 3, 4, 5]

# Remove by value (first occurrence)
numbers.remove(3)           # [1, 2, 4, 5]

# Remove by index
numbers.pop(0)              # Removes 1, returns [2, 4, 5]
last = numbers.pop()        # Removes last, returns [2, 4]

# Remove all items
numbers.clear()             # []

# Delete by index
del numbers[0]              # Remove first item
```

### Modifying Items

```python
numbers = [1, 2, 3, 4, 5]

# Change single item
numbers[0] = 10             # [10, 2, 3, 4, 5]

# Change slice
numbers[1:3] = [20, 30]     # [10, 20, 30, 4, 5]
```

---

## List Methods for Analysis

### Finding Items

```python
fruits = ["apple", "banana", "cherry", "banana"]

# Find first index
index = fruits.index("banana")  # 1

# Find all indices (need loop - you'll learn in next sections)
print(fruits.count("banana"))   # 2 (appears twice)

# Check if item exists
if "apple" in fruits:
    print("Apple is in the list")
```

### Sorting and Reversing

```python
numbers = [3, 1, 4, 1, 5, 9]

# Sort (modifies original)
numbers.sort()              # [1, 1, 3, 4, 5, 9]

# Sort descending
numbers.sort(reverse=True)  # [9, 5, 4, 3, 1, 1]

# Reverse (modifies original)
numbers.reverse()           # [1, 1, 3, 4, 5, 9]

# Get sorted copy without modifying
sorted_nums = sorted(numbers)  # Returns new sorted list
```

### Copying Lists

```python
original = [1, 2, 3]

# Wrong way - creates reference, not copy
copy_wrong = original
copy_wrong[0] = 99
print(original)  # [99, 2, 3] - original changed!

# Correct ways to copy
copy1 = original.copy()     # Shallow copy
copy2 = original[:]         # Slice copy
copy3 = list(original)      # Using list() constructor

copy1[0] = 99
print(original)  # [1, 2, 3] - original unchanged
```

**Note about shallow vs deep copy**: You'll learn more about this when needed. For now, use `.copy()`.

---

## Iterating Through Lists

### For Loop with Values

```python
fruits = ["apple", "banana", "cherry"]

for fruit in fruits:
    print(fruit)
# Output:
# apple
# banana
# cherry
```

### For Loop with Index

```python
fruits = ["apple", "banana", "cherry"]

for i in range(len(fruits)):
    print(f"{i}: {fruits[i]}")
# Output:
# 0: apple
# 1: banana
# 2: cherry

# Or use enumerate (cleaner)
for index, fruit in enumerate(fruits):
    print(f"{index}: {fruit}")
```

**Note about `enumerate()`**: This useful function gives you both index and value. You'll see it often!

---

## List Comprehension 

Create new lists by transforming existing ones:

```python
numbers = [1, 2, 3, 4, 5]

# Multiply each by 2
doubled = [x * 2 for x in numbers]  # [2, 4, 6, 8, 10]

# Filter even numbers
evens = [x for x in numbers if x % 2 == 0]  # [2, 4]

# Convert to strings
strings = [str(x) for x in numbers]  # ['1', '2', '3', '4', '5']
```

**Note about list comprehensions**: You'll learn this properly in Module 10.1. For now, just know they're a powerful way to create lists.

---

## Practical Examples

### Example 1: Student Grade Tracker

```python
students = ["Sachin", "Dhoni", "Virat"]
grades = [85, 92, 78]

# Display grades
for i, student in enumerate(students):
    grade = grades[i]
    if grade >= 90:
        status = "Excellent"
    elif grade >= 80:
        status = "Good"
    else:
        status = "Pass"
    
    print(f"{student}: {grade} ({status})")

# Statistics
average = sum(grades) / len(grades)
highest = max(grades)
lowest = min(grades)

print(f"\nAverage: {average:.1f}")
print(f"Highest: {highest}")
print(f"Lowest: {lowest}")
```


---

## Common Mistakes

### ❌ Mistake 1: Confusing Reference vs Copy

```python
# Wrong - creates reference
list1 = [1, 2, 3]
list2 = list1
list2[0] = 99
print(list1)  # [99, 2, 3] - Oops, original changed!

# Correct - create copy
list2 = list1.copy()
list2[0] = 99
print(list1)  # [1, 2, 3] - Original safe
```

### ❌ Mistake 2: Index Out of Range

```python
numbers = [1, 2, 3]

# ERROR
print(numbers[5])   # IndexError!

# Check length first
if len(numbers) > 5:
    print(numbers[5])
else:
    print("Index out of range")
```

### ❌ Mistake 3: Forgetting Parentheses for Methods

```python
numbers = [1, 2, 3]

# Wrong - forgot ()
numbers.sort  # This doesn't sort!

# Correct - include ()
numbers.sort()  # This sorts!
```

---

## Milestone Task: To-Do List Application

Create a to-do list manager using list operations!

### Requirements:
- Add tasks to list
- View all tasks with numbers
- Mark tasks complete
- Delete tasks
- Show statistics (total, completed, pending)
- Save progress during session

### Example Output:

```bash
========================================
📋 TO-DO LIST (0 tasks)
========================================
No tasks! You're free!

Options:
A. Add task
D. Delete task
C. Clear all
Q. Quit
========================================
Choice (A/D/C/Q): A
New task: complete HW
✅ Added: complete HW

========================================
📋 TO-DO LIST (1 tasks)
========================================
1. complete HW

Options:
A. Add task
D. Delete task
C. Clear all
Q. Quit
========================================
Choice (A/D/C/Q): 
```

---

## What's Next?

Next module: **Tuples** - Immutable lists (can't be changed)!

---

## References

- Lists: https://docs.python.org/3/tutorial/datastructures.html#more-on-lists
- List Methods: https://docs.python.org/3/tutorial/datastructures.html#using-lists-as-stacks

