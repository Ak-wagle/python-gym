# Module 5.4: Dictionaries

A **dictionary** is an **unordered, mutable collection of key-value pairs**. Instead of accessing items by position (index), you access them by meaningful **keys**. This makes dictionaries perfect for structured data where labels matter (like robot configurations, sensor data with labels, or any mapping of names to values).

**Key Technical Properties:**
- **Unordered**: Items don't have fixed positions (Python 3.7+ maintains insertion order as implementation detail)
- **Mutable**: Can add, remove, and modify key-value pairs
- **Key-based access**: Use meaningful keys instead of indices: `dict["name"]` vs `list[0]`
- **Heterogeneous**: Both keys and values can be mixed types
- **Hashable keys**: Keys must be immutable (strings, numbers, tuples work; lists don't)
- **Mutable values**: Values can be any type including lists and dicts

**Why This Matters**: Dictionaries are essential for robotics - storing configuration parameters, sensor readings with labels, robot states, etc. Much cleaner than remembering position indices!

---

## Creating Dictionaries

### Dictionary Syntax

```python
# Empty dictionary
empty = {}

# Dictionary with key-value pairs
person = {
    "name": "Sachin",
    "age": 40,
    "city": "Mumbai"
}

# Different value types
mixed = {
    "name": "Dhoni",
    "age": 30,
    "height": 5.9,
    "is_student": False,
    "grades": [85, 92, 78]  # Can use lists!
}

# Using dict() constructor
from_tuples = dict([("a", 1), ("b", 2)])  # {'a': 1, 'b': 2}

# Nested dictionaries
student = {
    "name": "Kohli",
    "info": {
        "age": 20,
        "major": "CS"
    }
}
```

---

## Accessing Dictionary Items

### Getting Values

```python
person = {
    "name": "Alexander",
    "age": 55,
    "city": "Pune"
}

# Access by key
print(person["name"])  # "Alexander"
print(person["age"])   # 55

# Using .get() method (safer)
print(person.get("name"))  # "Alexander"
print(person.get("country"))  # None (doesn't error)
print(person.get("country", "Unknown"))  # "Unknown" (default value)

# Check if key exists
if "age" in person:
    print("Age exists:", person["age"])

# Get all keys
print(person.keys())    # dict_keys(['name', 'age', 'city'])

# Get all values
print(person.values())  # dict_values(['Alexander', 55, 'Pune'])

# Get all key-value pairs
print(person.items())   # dict_items([('name', 'Alexander'), ('age', 55), ...])
```

**Note about `.get()`**: This is safer than direct access because it doesn't error if key doesn't exist.

---

## Modifying Dictionaries

### Adding/Updating Items

```python
person = {"name": "Alexander", "age": 55}

# Add new key-value
person["city"] = "NYC"  # {'name': 'Alexander', 'age': 55, 'city': 'NYC'}

# Update existing value
person["age"] = 56      # {'name': 'Alexander', 'age': 56, 'city': 'NYC'}

# Using .update() to add multiple
person.update({"country": "USA", "zip": 10001})

# Using .setdefault() (add only if not exists)
person.setdefault("email", "alexander@gmail.com")
```

### Removing Items

```python
person = {"name": "Alexander", "age": 55, "city": "NYC"}

# Remove and get value
value = person.pop("city")  # Returns "NYC"
print(value)                # "NYC"
print(person)               # {'name': 'Alexander', 'age': 55}

# Remove without getting value
del person["age"]           # {'name': 'Alexander'}

# Remove all items
person.clear()              # {}
```

---

## Iterating Through Dictionaries

### Looping Through Items

```python
person = {"name": "Alexander", "age": 55, "city": "NYC"}

# Loop through keys
for key in person:
    print(key, person[key])

# Loop through keys explicitly
for key in person.keys():
    print(key, person[key])

# Loop through values only
for value in person.values():
    print(value)

# Loop through key-value pairs (best way!)
for key, value in person.items():
    print(f"{key}: {value}")
```

---

## Dictionary Methods

```python
robot = {
    "name": "R2D2",
    "battery": 85,
    "status": "active"
}

# Get all keys
print(robot.keys())       # dict_keys(['name', 'battery', 'status'])

# Get all values
print(robot.values())     # dict_values(['R2D2', 85, 'active'])

# Get all key-value pairs
print(robot.items())      # dict_items([...])

# Copy dictionary
copy = robot.copy()       # Separate dictionary

# Pop with default
value = robot.pop("missing", "default")  # Returns "default"

# SetDefault
robot.setdefault("version", "1.0")

# Merge two dictionaries (Python 3.9+)
dict1 = {"a": 1, "b": 2}
dict2 = {"b": 3, "c": 4}
merged = dict1 | dict2  # {"a": 1, "b": 3, "c": 4}
```

---

## Practical Examples

### Example 1: Robot Configuration

```python
# Robot setup with dictionaries
robot_config = {
    "name": "TurtleBot",
    "type": "differential_drive",
    "battery": 95,
    "position": {"x": 0, "y": 0},
    "sensors": {
        "lidar": True,
        "camera": True,
        "imu": True
    }
}

# Access nested values
print(f"Robot: {robot_config['name']}")
print(f"Position: {robot_config['position']}")
print(f"Has camera: {robot_config['sensors']['camera']}")

# Update configuration
robot_config['battery'] = 87
robot_config['position']['x'] = 10
print(robot_config)
```

---

## Dictionary Comprehension 

Create dictionaries from existing data:

```python
# Create dictionary from lists
keys = ["a", "b", "c"]
values = [1, 2, 3]
result = {k: v for k, v in zip(keys, values)}
# {'a': 1, 'b': 2, 'c': 3}

# Transform existing dictionary
prices = {"apple": 0.5, "banana": 0.3}
doubled = {item: price * 2 for item, price in prices.items()}
# {'apple': 1.0, 'banana': 0.6}

# Filter dictionary
scores = {"Varun": 90, "Arun": 75, "Sharan": 85}
passing = {name: score for name, score in scores.items() if score >= 80}
# {'Varun': 90, 'Sharan': 85}
```

**Note about comprehensions**: You'll learn these properly in Module 10.1. For now, just know they're powerful!

---

## Common Mistakes

### ❌ Mistake 1: Using Mutable Types as Keys

```python
# ERROR - lists can't be keys
config = {["sensor", "type"]: "lidar"}  # TypeError!

# Use tuples instead
config = {("sensor", "type"): "lidar"}
```

### ❌ Mistake 2: Accessing Non-existent Key

```python
person = {"name": "Alice"}

# ERROR - key doesn't exist
print(person["age"])  # KeyError!

# Use .get() for safety
print(person.get("age"))  # None
print(person.get("age", 0))  # 0 (default)
```

---

## Milestone Task: TODO
---

## What's Next?

Next module: **Sets** - Unordered collections of unique items!

---

## References

- Dictionaries: https://docs.python.org/3/tutorial/datastructures.html#dictionaries
- Dictionary Methods: https://docs.python.org/3/library/stdtypes.html#mapping-types-dict

