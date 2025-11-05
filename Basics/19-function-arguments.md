# Module 6.2: Function Arguments

**Function arguments** are the techniques for passing data to functions. Python supports multiple argument types: positional arguments (ordered by position), keyword arguments (specified by name), default arguments (preset values), *args (variable positional), and **kwargs (variable keyword). This flexibility makes functions powerful and adaptable.

**Key Technical Properties:**
- **Positional**: Arguments matched by position/order
- **Keyword**: Arguments specified by name (order doesn't matter)
- **Default**: Parameters with preset values
- **Variable-length**: `*args` for variable positional arguments
- **Variable-keyword**: `**kwargs` for variable keyword arguments
- **Flexible**: Can combine different types
- **Order matters**: Positional before keyword, defaults at end

**Why This Matters**: Advanced argument techniques are essential for writing flexible functions that can handle many different input scenarios, crucial for robot API design and general library functions.

---

## Positional Arguments

Arguments matched by position/order:

```python
def save_user(username, email, age):
    """Save user information"""
    print(f"{username}, {email}, {age} years old")

# Position matters!
save_user("john_doe", "john@example.com", 28)  # Correct
save_user(28, "john@example.com", "john_doe")  # Wrong order!
```

---

## Keyword Arguments

Specify argument names - order doesn't matter:

```python
def create_config(host, port, timeout):
    """Create server configuration"""
    print(f"Connecting to {host}:{port} with {timeout}s timeout")

# Using keywords - any order
create_config(port=8080, host="localhost", timeout=30)
create_config(host="192.168.1.1", timeout=60, port=5000)
create_config("localhost", 8080, 30)  # Still works positionally
```

---

## Default Arguments

Provide default values for parameters:

```python
def log_message(message, level="INFO", timestamp=True):
    """Log a message with options"""
    if timestamp:
        print(f"[{level}] {message}")
    else:
        print(f"{message}")

# Use defaults
log_message("System started")
# [INFO] System started

# Override some defaults
log_message("Error occurred", "ERROR")
# [ERROR] Error occurred

# Override all
log_message("Debug info", "DEBUG", False)
# Debug info
```

**Important**: Default parameters must come AFTER non-default parameters:

```python
# ERROR - non-default after default
def bad_function(name="Unknown", age):  # SyntaxError!
    pass

# Correct - defaults at end
def good_function(age, name="Unknown"):
    pass
```

---

## *args (Variable Positional Arguments)

Accept any number of positional arguments:

```python
def calculate_total(*prices):
    """Calculate total price from multiple items"""
    total = sum(prices)
    print(f"Total: ${total:.2f}")

calculate_total(10.50)                        # $10.50
calculate_total(10.50, 25.00)                 # $35.50
calculate_total(10.50, 25.00, 15.75, 8.99)    # $60.24
```
```python
# Inside function, args is a tuple
def process_files(*filenames):
    """Process multiple files"""
    for i, filename in enumerate(filenames, 1):
        print(f"{i}. Processing {filename}")

process_files("data.csv")
process_files("data.csv", "config.json", "log.txt")
```
```python
# Mixing regular and *args
def create_database(db_name, *tables):
    """Create database with tables"""
    print(f"Database: {db_name}")
    print(f"Tables ({len(tables)}):")
    for table in tables:
        print(f"  - {table}")

create_database("sales_db", "customers", "orders", "products")
```

**Inside the function**: `*prices` becomes a **tuple** of all extra arguments.

---

## **kwargs (Variable Keyword Arguments)

Accept any number of keyword arguments:

```python
def configure_app(**settings):
    """Configure application with various settings"""
    for key, value in settings.items():
        print(f"{key}: {value}")

configure_app(debug=True, port=8000, theme="dark")
# debug: True
# port: 8000
# theme: dark
```
### Real example: Robot configuration
```python
def initialize_robot(name, **params):
    """Initialize robot with flexible parameters"""
    print(f"Robot: {name}")
    for param, value in params.items():
        print(f"  {param}: {value}")

initialize_robot(
    "TurtleBot3",
    wheel_diameter=0.066,
    max_speed=0.26,
    sensors=["lidar", "imu", "camera"],
    firmware_version="1.2.1"
)
```

**Inside the function**: `**settings` becomes a **dictionary** of keyword arguments.

---

## Combining All Argument Types

```python
def process_request(method, url, *headers, **options):
    """Process HTTP request with flexible parameters"""
    print(f"\n{method} {url}")
    
    print(f"Headers ({len(headers)}):")
    for header in headers:
        print(f"  {header}")
    
    print(f"Options:")
    for key, value in options.items():
        print(f"  {key}: {value}")

process_request(
    "GET",
    "https://api.example.com/users",
    "Authorization: Bearer token123",
    "Content-Type: application/json",
    timeout=30,
    retries=3,
    cache=True
)
```

**Order Rule**: Regular parameters → *args → keyword defaults → **kwargs

---

## Unpacking Arguments

Use `*` and `**` when CALLING functions:
### Unpacking lists/tuples into positional arguments
```python
def calculate_average(num1, num2, num3):
    """Calculate average of three numbers"""
    return (num1 + num2 + num3) / 3

prices = [10.00, 15.00, 20.00]
result = calculate_average(*prices)  # Unpacks to: 10.00, 15.00, 20.00
print(f"Average: ${result:.2f}")  # Average: $15.00
```

### Unpacking dictionary into keyword arguments
```python
def send_email(to, subject, body, priority="normal"):
    """Send email with options"""
    print(f"To: {to}")
    print(f"Subject: {subject}")
    print(f"Body: {body}")
    print(f"Priority: {priority}")

email_data = {
    "to": "admin@company.com",
    "subject": "System Alert",
    "body": "CPU usage high",
    "priority": "high"
}

send_email(**email_data)  # Unpacks dictionary
# To: admin@company.com
# Subject: System Alert
# Body: CPU usage high
# Priority: high
```

---

## Practical Examples

### Example: Flexible Calculator

```python
def calculate(*numbers, operation="sum"):
    """Calculate with various operations"""
    if not numbers:
        return 0
    
    if operation == "sum":
        return sum(numbers)
    elif operation == "average":
        return sum(numbers) / len(numbers)
    elif operation == "product":
        result = 1
        for num in numbers:
            result *= num
        return result
    elif operation == "max":
        return max(numbers)

# Use with different operations
print(calculate(10, 20, 30))                    # sum: 60
print(calculate(10, 20, 30, operation="average"))  # 20.0
print(calculate(2, 3, 4, operation="product"))     # 24
print(calculate(5, 15, 8, operation="max"))        # 15
```

---

## Common Mistakes

### ❌ Mistake 1: Default Arguments in Wrong Position

```python
# ERROR - non-default after default
def bad_order(name="Unknown", age, department):
    pass

# Correct - defaults at end
def good_order(age, department, name="Unknown"):
    pass
```

### ❌ Mistake 2: **kwargs Becomes Dictionary

```python
def print_config(**config):
    """Print configuration"""
    # config is a DICTIONARY
    for key, value in config.items():
        print(f"{key}: {value}")

print_config(host="localhost", port=8000, debug=True)
```

### ❌ Mistake 3: Wrong Unpacking Type

```python
# Using * with dictionary
params = {"name": "john", "age": 28}
some_function(*params)  # Wrong! Only gives keys

# Use ** for dictionary
some_function(**params)  # Correct!

# Using ** with list
values = [10, 20, 30]
some_function(**values)  # Error!

# Use * for list
some_function(*values)  # Correct!
```

---

## Milestone Task: Robot Task Manager

### Requirements:

- Takes a robot name
- Accepts multiple tasks using *args
- Accepts robot settings using **kwargs
- Displays the robot’s task list and current setup

### Example Output:
```bash
========================================
ROBOT: Atlas
========================================

Tasks Assigned:
 - Lift crates
 - Scan area
 - Patrol region

Settings:
 speed: 2.5 m/s
 battery_mode: Eco
 sensors_active: True
========================================
```
---

## What's Next?

Next module: **Scope - Global vs. Local** - Understanding variable accessibility!

---

## References

- Arguments: https://docs.python.org/3/tutorial/controlflow.html#more-on-defining-functions
- *args and **kwargs: https://docs.python.org/3/faq/programming.html#what-are-the-differences-between-the-different-ways-i-can-define-a-function

