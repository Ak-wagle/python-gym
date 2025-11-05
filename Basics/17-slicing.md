# Module 5.6: Slicing Operations

**Slicing** is the technique of extracting a portion (substring or sub-sequence) from a sequence using the syntax `sequence[start:stop:step]`. Slicing works on all sequences: strings, lists, and tuples. It creates a **new object** without modifying the original - this is different from indexing which returns a single item.

**Key Technical Properties:**
- **Syntax**: `[start:stop:step]`
- **Start**: Inclusive (included in slice)
- **Stop**: Exclusive (NOT included in slice)
- **Step**: Interval (default 1)
- **Creates copy**: Doesn't modify original
- **Works on all sequences**: Strings, lists, tuples
- **Negative indices work**: Count from end

**Why This Matters**: Slicing is essential for extracting substrings, subsequences, reversing data, and working with portions of sensor data or waypoint lists in robotics applications.

---

## Slicing Syntax Deep Dive

### Basic Slicing: `sequence[start:stop]`

```python
text = "Hello World"
#       012345678910      (positions)

# Extract portion
print(text[0:5])    # "Hello" (index 0 up to, not including, 5)
print(text[6:11])   # "World"
print(text[0:])     # "Hello World" (from 0 to end)
print(text[:5])     # "Hello" (from start to 5)
print(text[:])      # "Hello World" (entire string)
```

**Rule**: The slice goes from `start` (inclusive) to `stop` (exclusive).

### Negative Indexing in Slicing

```python
text = "Hello World"
#       -11-10-9-8-7-6-5-4-3-2-1 (negative positions)

print(text[-5:])     # "World" (last 5 characters)
print(text[:-6])     # "Hello" (everything except last 6)
print(text[-5:-1])   # "Worl" (5th from end, up to last char)
```

### Step Parameter: `sequence[start:stop:step]`

```python
text = "Hello World"

# Every 2nd character
print(text[::2])     # "HloWrd"

# Every 2nd starting from index 1
print(text[1::2])    # "el ol"

# Every 3rd character
print(text[::3])     # "HoWl"

# Reverse (step = -1)
print(text[::-1])    # "dlroW olleH"

# Reverse every 2nd
print(text[::-2])    # "dl ol"

# Start from end, go backwards
print(text[-1::-1])  # "dlroW olleH" (reverse)
```

---

## Practical Slicing Examples

### Example 1: Extract Parts of Data

```python
# Sensor reading: "TEMP:25.3,HUM:65.2,PRESS:1013"
sensor_data = "TEMP:25.3,HUM:65.2,PRESS:1013"

# Extract temperature value
temp_start = sensor_data.find(":") + 1
temp_end = sensor_data.find(",")
temp = sensor_data[temp_start:temp_end]
print(f"Temperature: {temp}°C")

# Extract humidity value
hum_start = sensor_data.find("HUM:") + 4
hum_end = sensor_data.find(",", hum_start)
humidity = sensor_data[hum_start:hum_end]
print(f"Humidity: {humidity}%")
```

**Note about `.find()`**: You learned this in Module 5.1 (Strings). It finds the position of text.


---

## Slicing Lists vs Strings

Both support slicing, but strings create strings while lists create lists:

```python
# Strings
text = "Hello"
portion = text[1:4]    # "ell" (string)

# Lists
items = [1, 2, 3, 4, 5]
portion = items[1:4]   # [2, 3, 4] (list)

# Tuples
coords = (10, 20, 30)
portion = coords[1:]   # (20, 30) (tuple)
```

---

---

## Common Mistakes

### ❌ Mistake 1: Slice Modifying Original

```python
text = "Hello"

# Slicing creates new, doesn't modify original
part = text[1:4]  # "ell"
print(text)       # Still "Hello"

# Strings are immutable anyway!
# But with lists:
items = [1, 2, 3, 4, 5]
subset = items[1:4]  # [2, 3, 4]
subset[0] = 99       # Changes subset, not original
print(items)         # Still [1, 2, 3, 4, 5]
```

### ❌ Mistake 2: Trying to Slice Non-Sequences

```python
# Can't slice numbers
num = 12345
print(num[1:3])  # TypeError!

# Convert to string first
num_str = str(num)
print(num_str[1:3])  # "23"
```

---

## Milestone Task: TODO

---

## What's Next?

Next module: **Functions** - Create reusable blocks of code!

---

## References

- Slicing: https://docs.python.org/3/tutorial/introduction.html#strings
- Sequence Types: https://docs.python.org/3/library/stdtypes.html#sequence-types-list-tuple-range

