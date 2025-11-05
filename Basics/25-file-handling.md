# Module 8.1: File Handling

**File handling** in Python allows reading from and writing to files on disk. The `open()` function returns a file object with methods like `.read()`, `.write()`, `.readline()`, etc.

Files must be opened (mode: 'r'=read, 'w'=write, 'a'=append) and closed to free resources. Context managers (`with` statement) automatically handle closing files safely.

**Key Technical Properties:**
- **File modes**: 'r' (read), 'w' (write), 'a' (append), 'b' (binary)
- **File object**: Returned by `open()`, provides methods
- **Context manager**: `with` statement automatically closes
- **Encoding**: UTF-8 default, specify if needed
- **Position**: Cursor moves as you read/write
- **Seekable**: Can move cursor with `.seek()`

---

## Basic File Operations

### Reading Files

```python
# Way 1: Read entire file
with open("config.txt", "r") as file:
    content = file.read()  # Returns entire content as string
    print(content)

# Way 2: Read line by line
with open("config.txt", "r") as file:
    for line in file:
        print(line.strip())  # .strip() removes \n

# Way 3: Read all lines into list
with open("config.txt", "r") as file:
    lines = file.readlines()  # Returns list of lines
    print(lines)  # ['line1\n', 'line2\n']
```

### Writing Files

```python
# Create/overwrite file
with open("users.txt", "w") as file:
    file.write("john_doe\n")
    file.write("jane_smith\n")
    file.write("bob_wilson\n")

# Append to existing file
with open("users.txt", "a") as file:
    file.write("alice_johnson\n")
```

### Context Manager (`with` statement)

Always use `with` - it automatically closes the file:

```python
# GOOD - file closed automatically
with open("data.txt", "r") as file:
    data = file.read()

# BAD - file might not close properly
file = open("data.txt", "r")
data = file.read()
# If error occurs, file stays open!
```

---

## Working with Different File Types

### Text Files (Log Files, Configs)

```python
# Write application logs
logs = [
    "2025-11-05 10:00:00 - Application started",
    "2025-11-05 10:00:05 - Database connected",
    "2025-11-05 10:00:10 - Server listening on port 8000",
    "2025-11-05 10:02:30 - Request from 192.168.1.100"
]

with open("application.log", "w") as file:
    for log in logs:
        file.write(log + "\n")

# Read and process logs
with open("application.log", "r") as file:
    for line in file:
        timestamp, message = line.strip().split(" - ")
        print(f"[{timestamp}] {message}")
```

### CSV Files (Data Export/Import)

```python
import csv

# Write CSV data
employees = [
    ["john_doe", "Engineering", 100000],
    ["jane_smith", "Sales", 80000],
    ["bob_wilson", "Marketing", 75000]
]

with open("employees.csv", "w", newline="") as file:
    writer = csv.writer(file)
    writer.writerow(["Name", "Department", "Salary"])  # Header
    writer.writerows(employees)

# Read CSV data
with open("employees.csv", "r") as file:
    reader = csv.reader(file)
    header = next(reader)  # Get header
    print(f"Columns: {header}")
    
    for row in reader:
        name, dept, salary = row
        print(f"{name}: {dept} - ${salary}")
```

**Note about `newline=""`**: This prevents extra blank lines in CSV files.

### JSON Files (Structured Data)

```python
import json

# Write JSON configuration
config = {
    "database": {
        "host": "localhost",
        "port": 5432,
        "name": "app_db"
    },
    "cache": {
        "enabled": True,
        "ttl": 3600
    },
    "logging": {
        "level": "INFO",
        "file": "app.log"
    }
}

with open("config.json", "w") as file:
    json.dump(config, file, indent=2)

# Read JSON configuration
with open("config.json", "r") as file:
    loaded_config = json.load(file)
    print(f"Database: {loaded_config['database']['host']}")
    print(f"Cache TTL: {loaded_config['cache']['ttl']}")
```

---

## File Navigation

### Get File Information

```python
import os

filename = "data.txt"

# Check if file exists
if os.path.exists(filename):
    # Get file size
    size = os.path.getsize(filename)
    print(f"Size: {size} bytes")
    
    # Get modification time
    import time
    mod_time = os.path.getmtime(filename)
    print(f"Modified: {time.ctime(mod_time)}")

# List files in directory
files = os.listdir(".")
for file in files:
    if file.endswith(".txt"):
        print(f"Text file: {file}")
```

### Work with Paths

```python
import os

# Join paths correctly (works on all OS)
data_dir = "data"
filename = "results.csv"
filepath = os.path.join(data_dir, filename)
print(filepath)  # "data/results.csv" or "data\\results.csv"

# Create directory if doesn't exist
if not os.path.exists(data_dir):
    os.makedirs(data_dir)
    print(f"Created directory: {data_dir}")
```

---

## Practical Examples

### Example 1: Application Data Saver

```python
import os
import json

def save_data(filename, data):
    """Save data to JSON file"""
    with open(filename, "w") as f:
        json.dump(data, f, indent=2)
    print(f"✓ Saved to {filename}")

def load_data(filename):
    """Load data from JSON file"""
    if not os.path.exists(filename):
        print(f"✗ File not found: {filename}")
        return None
    
    with open(filename, "r") as f:
        data = json.load(f)
    print(f"✓ Loaded from {filename}")
    return data

# Use it
user_data = {
    "username": "john_doe",
    "email": "john@example.com",
    "preferences": {
        "theme": "dark",
        "notifications": True
    }
}

save_data("user_profile.json", user_data)
loaded = load_data("user_profile.json")
print(loaded)
```

---

## Common Mistakes

### ❌ Mistake 1: Not Closing Files

```python
#  File not closed
file = open("data.txt", "r")
content = file.read()

# Use with statement
with open("data.txt", "r") as file:
    content = file.read()
```

### ❌ Mistake 2: Writing to Read-Only File

```python
# Opens as read, then tries to write
with open("data.txt", "r") as file:
    file.write("new data")  # io.UnsupportedOperation!

# Use correct mode
with open("data.txt", "w") as file:
    file.write("new data")
```

---

## Milestone Task: Simple Note Saver

### Description:

- Create a program that:
- Asks the user to enter a note
- Saves the note into a text file
- Reads the file back
- Displays the saved content

### Example Output

```bash
Enter your note: Python is fun to learn!

Saving note...
Note saved successfully!

Reading note from file...

Your Note:
Python is fun to learn!
```

## What's Next?

Next module: **CSV & JSON** - Advanced file format handling!

---

## References

- File I/O: https://docs.python.org/3/tutorial/inputoutput.html
- JSON: https://docs.python.org/3/library/json.html
- CSV: https://docs.python.org/3/library/csv.html

