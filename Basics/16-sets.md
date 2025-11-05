# Module 5.5: Sets

A **set** is an **unordered, mutable collection of unique items**. Unlike lists which can have duplicates, sets automatically eliminate duplicates and don't maintain order. Sets are optimized for checking membership and performing mathematical set operations (union, intersection, difference).

**Key Technical Properties:**
- **Unordered**: No indices or fixed positions
- **Unique**: No duplicate values allowed
- **Mutable**: Can add/remove items
- **Unindexed**: Can't access by position (no `set[0]`)
- **Hashable items**: Items must be immutable (strings, numbers, tuples)
- **Fast lookup**: Checking membership is very fast

**Why This Matters**: Sets are useful for removing duplicates, checking if items exist, and performing mathematical operations on collections (especially useful in robotics for filtering sensor readings or comparing datasets).

---

## Creating Sets

```python
# Set with values
colors = {"red", "green", "blue"}

# Empty set (note: {} is dictionary, use set() for empty)
empty = set()

# Set from list (removes duplicates)
numbers = set([1, 2, 2, 3, 3, 3, 4])  # {1, 2, 3, 4}

# Set from string (creates set of characters)
letters = set("hello")  # {'h', 'e', 'l', 'o'}

# Nested sets not allowed (items must be hashable)
# bad = {{1, 2}, {3, 4}}  # TypeError!
```

---

## Set Operations

### Adding and Removing Items

```python
colors = {"red", "green"}

# Add single item
colors.add("blue")      # {"red", "green", "blue"}

# Add multiple items
colors.update(["yellow", "purple"])  # Add from list

# Remove item (error if not exists)
colors.remove("red")    # Error if "red" not found

# Discard item (no error if not exists)
colors.discard("orange")  # No error

# Pop random item
item = colors.pop()

# Clear all items
colors.clear()          # set()
```

### Mathematical Set Operations

```python
math_students = {"Alice", "Bob", "Charlie", "Diana"}
cs_students = {"Bob", "Charlie", "Eve", "Frank"}

# Union - all students in either class
all_students = math_students | cs_students
# {"Alice", "Bob", "Charlie", "Diana", "Eve", "Frank"}

all_students = math_students.union(cs_students)  # Same

# Intersection - students in both classes
both = math_students & cs_students
# {"Bob", "Charlie"}

both = math_students.intersection(cs_students)  # Same

# Difference - math only (not in CS)
math_only = math_students - cs_students
# {"Alice", "Diana"}

math_only = math_students.difference(cs_students)  # Same

# Symmetric difference - in one or other but not both
either_not_both = math_students ^ cs_students
# {"Alice", "Diana", "Eve", "Frank"}
```

### Checking Membership and Subsets

```python
numbers = {1, 2, 3, 4, 5}
small = {1, 2, 3}

# Check if item in set
if 3 in numbers:
    print("3 is in the set")

# Check if subset
print(small.issubset(numbers))      # True (all items in numbers)
print(numbers.issuperset(small))    # True (contains all of small)

# Check if disjoint (no common items)
set_a = {1, 2, 3}
set_b = {4, 5, 6}
print(set_a.isdisjoint(set_b))      # True
```

---

## Practical Examples

### Example 1: Compare Two Datasets

```python
# Robot A visited waypoints
robot_a_waypoints = {(0, 0), (1, 1), (2, 2), (3, 3)}

# Robot B visited waypoints
robot_b_waypoints = {(0, 0), (1, 1), (5, 5), (6, 6)}

# Common waypoints
common = robot_a_waypoints & robot_b_waypoints
print(f"Both visited: {common}")

# Unique to A
unique_a = robot_a_waypoints - robot_b_waypoints
print(f"Only A: {unique_a}")

# All visited
all_waypoints = robot_a_waypoints | robot_b_waypoints
print(f"Total unique: {all_waypoints}")
```

---

## Common Mistakes

### ❌ Mistake 1: Using Mutable Items

```python
# ERROR - lists can't be in sets
bad_set = {[1, 2], [3, 4]}  # TypeError!

# Use tuples instead
good_set = {(1, 2), (3, 4)}
```

### ❌ Mistake 2: Empty Set Syntax

```python
# Wrong - this creates empty dict
empty = {}
print(type(empty))  # <class 'dict'>

# Correct
empty = set()
print(type(empty))  # <class 'set'>
```

### ❌ Mistake 3: Accessing by Index

```python
colors = {"red", "green", "blue"}

# ERROR - sets don't have indices
print(colors[0])  # TypeError!

# Convert to list or iterate
colors_list = list(colors)
print(colors_list[0])

 Or just check membership
if "red" in colors:
    print("Red is in the set")
```

---

## When to Use Sets

Use sets when:
- Need unique items only
- Checking if item exists (faster than lists)
- Need set operations (union, intersection)
- Order doesn't matter
- Removing duplicates

Don't use when:
- Need to access by index
- Need to maintain order
- Need to store mutable items (lists)

---

## Milestone Task: TODO

---

## What's Next?

Next module: **Slicing Operations** - Advanced techniques for extracting data!

---

## References

- Sets: https://docs.python.org/3/tutorial/datastructures.html#sets
- Set Methods: https://docs.python.org/3/library/stdtypes.html#set


