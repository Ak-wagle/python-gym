# Module 5.3: Tuples

A **tuple** is an **immutable, ordered collection** of items. Like lists, tuples maintain order and support indexing/slicing, but unlike lists, **you cannot modify them after creation**. This immutability makes tuples useful for data that shouldn't change (like coordinates, sensor readings that are final, or function return values).

**Key Technical Properties:**
- **Ordered**: Items have positions (index 0, 1, 2, etc.)
- **Immutable**: Cannot add, remove, or modify items
- **Heterogeneous**: Can contain different types
- **Indexable**: Access by position like lists
- **Sliceable**: Extract portions like lists
- **Hashable**: Can be used as dictionary keys (you'll learn dicts in Module 5.4)
- **Iterable**: Can loop through items

**Why This Matters**: Tuples are useful for protecting data from accidental modification, returning multiple values from functions (Module 6.1), and as dictionary keys in robotics applications.

---

## Creating Tuples

### Tuple Syntax

```python
# Empty tuple
empty = ()

# Single item (MUST have comma!)
single = (5,)      # (5,) is tuple, (5) is just 5!
print(type(single))  # <class 'tuple'>

# Multiple items
coordinates = (10, 20)
rgb_color = (255, 128, 0)

# Without parentheses (still tuple)
point = 1, 2, 3    # (1, 2, 3)

# Mixed types
mixed = (1, "hello", 3.14, True)

# Nested tuples
nested = ((1, 2), (3, 4), (5, 6))

# Using tuple() constructor
from_list = tuple([1, 2, 3])       # (1, 2, 3)
from_string = tuple("ABC")         # ('A', 'B', 'C')
```

---

## Accessing Tuple Items

### Indexing and Slicing

```python
point = (10, 20, 30)

# Indexing
print(point[0])     # 10
print(point[-1])    # 30

# Slicing
print(point[0:2])   # (10, 20)
print(point[::-1])  # (30, 20, 10) - reversed
```

---

## Tuple Methods and Operations

Since tuples are immutable, there are only two methods:

```python
numbers = (1, 2, 3, 2, 4, 2)

# Count occurrences
print(numbers.count(2))   # 3

# Find first index
print(numbers.index(3))   # 2
# print(numbers.index(5)) # ValueError if not found
```

### Tuple Unpacking (Powerful!)

```python
# Extract values from tuple
coordinates = (10, 20)
x, y = coordinates
print(f"X: {x}, Y: {y}")  # X: 10, Y: 20

# Unpack with different names
rgb = (255, 128, 0)
red, green, blue = rgb

# Unpack multiple
colors = ("red", "green", "blue")
c1, c2, c3 = colors
print(c1, c2, c3)  # red green blue

# Unpack with extras (rest goes to list)
first, *rest, last = (1, 2, 3, 4, 5)
print(first)   # 1
print(rest)    # [2, 3, 4]
print(last)    # 5
```

**Note about `*rest`**: This advanced unpacking you'll see more of in Module 6.2. It captures remaining items.

---

## Tuples vs Lists

| Feature | Tuple | List |
|---------|-------|------|
| Mutable | No | Yes |
| Syntax | `()` | `[]` |
| Speed | Faster | Slower |
| Memory | Less | More |
| Dictionary Key | Can be | Cannot be |
| When to Use | Fixed data | Changing data |

---

## Practical Examples

### Example: Storing Sensor Readings (Robotics!)

```python
# Three sensor readings (temperature, humidity, pressure)
# Once recorded, shouldn't change
sensor_reading = (25.3, 65.2, 1013.25)

# Access individual values
temp, humidity, pressure = sensor_reading
print(f"Temp: {temp}°C, Humidity: {humidity}%, Pressure: {pressure} hPa")

# Store multiple readings
readings = [
    (25.3, 65.2, 1013.25),  # Time 0
    (25.5, 64.8, 1013.30),  # Time 1
    (25.7, 64.5, 1013.35),  # Time 2
]

for i, (t, h, p) in enumerate(readings):
    print(f"Reading {i}: Temp={t}, Humidity={h}")
```

---

## Common Mistakes

### ❌ Mistake 1: Forgetting Comma for Single-Item Tuple

```python
# This is just an integer, not a tuple
single = (5)
print(type(single))  # <class 'int'>

# Add comma to make it a tuple
single = (5,)
print(type(single))  # <class 'tuple'>
```

### ❌ Mistake 2: Trying to Modify Tuple

```python
point = (1, 2)

# ERROR - tuples are immutable
point[0] = 3  # TypeError!

# Create new tuple instead
point = (3, 2)
```

### ❌ Mistake 3: Unpacking Wrong Number of Values

```python
# Too few variables
x, y = (1, 2, 3)  # ValueError! 3 values into 2 variables

# Correct number
x, y, z = (1, 2, 3)

# Or use *rest
x, *rest = (1, 2, 3)  # x=1, rest=[2,3]
```

### ❌ Mistake 4: Tuple with One Element Confusion

```python
# These are different!
t1 = (1)           # Integer 1, not a tuple
t2 = (1,)          # Tuple with one element

print(type(t1))    # <class 'int'>
print(type(t2))    # <class 'tuple'>
```

---

## Milestone Task: TODO

---

## What's Next?

Next module: **Dictionaries** - Store data with meaningful keys instead of just indices!

---

## References

- Tuples: https://docs.python.org/3/tutorial/datastructures.html#tuples-and-sequences
- Tuple Methods: https://docs.python.org/3/library/stdtypes.html#tuple

