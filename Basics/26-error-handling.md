# Module 9.1: Error Handling

**Exceptions** are errors that occur during program execution. Python uses **try-except-else-finally** blocks to handle exceptions gracefully without crashing.

The `try` block contains risky code, `except` catches specific errors, `else` runs if no error, and `finally` always runs. Different exception types (ValueError, TypeError, IOError) help identify and handle specific problems.

**Key Technical Properties:**
- **Exception types**: ValueError, TypeError, KeyError, IndexError, IOError, etc.
- **try block**: Code that might raise an exception
- **except block**: Handle specific exception type
- **Multiple except**: Different handlers for different errors
- **else block**: Runs only if no exception
- **finally block**: Always runs (cleanup code)
- **raise**: Manually raise exceptions
- **custom exceptions**: Create your own exception types

---

## Basic Try-Except

### Simple Try-Except

```python
# Handle division by zero
try:
    result = 10 / 0
except ZeroDivisionError:
    print("Cannot divide by zero!")
    result = 0

print(result)  # 0
```

### Multiple Exception Handlers

```python
def parse_config(config_str):
    """Parse configuration string"""
    try:
        # Try to parse as integer
        value = int(config_str)
        if value < 0 or value > 100:
            raise ValueError("Value must be 0-100")
        return value
    
    except ValueError as e:
        print(f"Invalid value: {e}")
        return 0
    
    except TypeError:
        print("Wrong type - expected string or number")
        return 0

print(parse_config("50"))      # 50
print(parse_config("200"))     # Invalid value...
print(parse_config(None))      # Wrong type...
```

---

## Common Exception Types

```python
# ValueError - wrong value for type
try:
    port = int("invalid_port")
except ValueError:
    print("Port must be a number")

# TypeError - wrong type
try:
    total = "data" + 100
except TypeError:
    print("Can't add string and number")

# IndexError - wrong list index
try:
    items = ["a", "b", "c"]
    print(items[10])
except IndexError:
    print("Index out of range")

# KeyError - dictionary key not found
try:
    config = {"host": "localhost"}
    print(config["port"])
except KeyError:
    print("Key doesn't exist")

# FileNotFoundError - file doesn't exist
try:
    with open("missing_config.json") as f:
        data = f.read()
except FileNotFoundError:
    print("Configuration file not found")

# ZeroDivisionError - division by zero
try:
    result = 100 / 0
except ZeroDivisionError:
    print("Can't divide by zero")
```

---

## Try-Except-Else

The `else` block runs ONLY if no exception occurred:

```python
def calculate_statistics(data):
    """Calculate stats with error handling"""
    try:
        if not data:
            raise ValueError("Empty dataset")
        average = sum(data) / len(data)
    except ValueError as e:
        print(f"Error: {e}")
        return 0
    else:
        # Only runs if NO exception
        print(f"Calculated successfully: {average:.2f}")
        return average

print(calculate_statistics([10, 20, 30]))  # Calculates
print(calculate_statistics([]))             # Error message
```

---

## Try-Except-Finally

The `finally` block ALWAYS runs, used for cleanup:

```python
def read_configuration(filename):
    """Read file, ensure cleanup"""
    file = None
    try:
        file = open(filename, "r")
        config = file.read()
        print(f"Read {len(config)} bytes")
    except FileNotFoundError:
        print("Configuration file not found")
    finally:
        # Always run (close file if opened)
        if file:
            file.close()
            print("File closed")

# Better way with 'with'
def read_configuration_better(filename):
    """Better approach using context manager"""
    try:
        with open(filename, "r") as file:
            config = file.read()
            print(f"Read {len(config)} bytes")
    except FileNotFoundError:
        print("Configuration file not found")
```

---

## Raising Exceptions

Manually raise exceptions for invalid data:

```python
def validate_database_config(config):
    """Validate database configuration"""
    if not config.get("host"):
        raise ValueError("Database host required")
    if not config.get("port"):
        raise ValueError("Database port required")
    if config["port"] < 1 or config["port"] > 65535:
        raise ValueError("Invalid port number")
    
    print(f"✓ Config valid: {config['host']}:{config['port']}")
    return True

# Use it
try:
    validate_database_config({})
except ValueError as e:
    print(f"Error: {e}")

try:
    validate_database_config({"host": "localhost", "port": 5432})
except ValueError as e:
    print(f"Error: {e}")

try:
    validate_database_config({"host": "localhost", "port": 99999})
except ValueError as e:
    print(f"Error: {e}")
```

---

## Custom Exceptions

Create your own exception types:

```python
class ConfigurationError(Exception):
    """Raised when configuration is invalid"""
    pass

class DatabaseError(Exception):
    """Raised when database operation fails"""
    pass

def connect_database(host, port, username):
    """Connect to database with validation"""
    if not host:
        raise ConfigurationError("Host is required")
    if not username:
        raise ConfigurationError("Username is required")
    
    # Simulate connection failure
    if host == "bad.server":
        raise DatabaseError(f"Cannot connect to {host}")
    
    print(f"✓ Connected to {host}:{port} as {username}")

# Use custom exceptions
try:
    connect_database("localhost", 5432, "admin")
except ConfigurationError as e:
    print(f"Config problem: {e}")
except DatabaseError as e:
    print(f"Connection problem: {e}")
```

---

## Catching All Exceptions

Use bare `except:` only as last resort:

```python
# Better - catch specific exception
try:
    port = int(input("Port: "))
except ValueError:
    print("Must be a number")

# Last resort - catch any exception
try:
    # Code that might fail
    risky_operation()
except Exception as e:
    # Catch any Exception type
    print(f"Error occurred: {e}")

# Avoid - catches EVERYTHING including system exits
try:
    something()
except:  # TOO broad!
    pass
```

---
## Milestone Task: Username Checker
### Description:

- Ask the user for a username.
- The username must:
    - Be at least 4 characters long
    - If it isn’t, raise and handle an error

### Example Output:
```bash
Enter username: sam
Error: Username must be at least 4 characters long.
Enter username: arjun_24
Username accepted ✅
```

---

## What's Next?

Next module: **List Comprehension & Generators** - Pythonic data processing!

---

## References

- Exceptions: https://docs.python.org/3/tutorial/errors.html
- Try-Except: https://docs.python.org/3/tutorial/errors.html#handling-exceptions
- Built-in Exceptions: https://docs.python.org/3/library/exceptions.html

