# Module 6.3: Scope - Global vs. Local

**Scope** defines the region of code where a variable is accessible. Python uses the **LEGB rule** (Local, Enclosing, Global, Built-in) to search for variables. Variables defined inside functions are **local** (exist only in that function), while variables defined outside are **global** (exist everywhere). Understanding scope prevents bugs and unintended variable modifications.

**Key Technical Properties:**
- **Local scope**: Inside functions, variables only exist there
- **Global scope**: Defined outside functions, accessible everywhere
- **Enclosing scope**: For nested functions (Module 6.4)
- **Built-in scope**: Python's built-in names
- **LEGB rule**: Search order for variable lookup
- **Global keyword**: Modify global variables from inside functions
- **Shadowing**: Local variable can hide global one

---

## Local Scope

Variables inside functions are LOCAL - only exist within that function:

```python
def process_payment(amount, card_number):
    """Process payment with local variables"""
    fee = amount * 0.02  # LOCAL variable
    total = amount + fee
    print(f"Processing ${total}")

process_payment(100, "4532...")  # Works fine
print(fee)  # NameError! fee doesn't exist here
```

### Local Variables Don't Affect Each Other

```python
def calculate_discount_1():
    """First discount calculation"""
    discount = 0.10  # LOCAL to this function
    return discount

def calculate_discount_2():
    """Second discount calculation"""
    discount = 0.15   # Different LOCAL variable!
    return discount

print(calculate_discount_1())  # 0.10
print(calculate_discount_2())  # 0.15
# Each function has its own 'discount'
```

---

## Global Scope

Variables defined outside functions are GLOBAL - accessible everywhere:

```python
API_BASE_URL = "https://api.example.com"  # GLOBAL variable

def fetch_users():
    """Function can access global variables"""
    print(f"Fetching from {API_BASE_URL}/users")

def fetch_orders():
    """Another function using same global"""
    print(f"Fetching from {API_BASE_URL}/orders")

fetch_users()   # Fetching from https://api.example.com/users
fetch_orders()  # Fetching from https://api.example.com/orders

# Global accessible everywhere
print(API_BASE_URL)  # https://api.example.com (works outside too)
```

---

## The `global` Keyword

To modify a global variable from inside a function, use `global`:

```python
# Without global keyword (creates local, doesn't change global)
counter = 0

def increment_wrong():
    """Doesn't modify global"""
    counter = counter + 1  # UnboundLocalError! Python thinks counter is local
    return counter
```
```python
# With global keyword (modifies actual global)
counter = 0

def increment_correct():
    """Modifies global variable"""
    global counter  # Tell Python to use the global one
    counter = counter + 1
    return counter

result = increment_correct()
print(result)   # 1
print(counter)  # 1 (modified!)
```

### Real Example: Database Connection Counter

```python
# Track database connections (global state)
active_connections = 0
total_queries = 0

def open_connection():
    """Open new database connection"""
    global active_connections
    active_connections += 1
    print(f"Connections: {active_connections}")

def close_connection():
    """Close database connection"""
    global active_connections
    active_connections -= 1
    print(f"Connections: {active_connections}")

def execute_query():
    """Execute database query"""
    global total_queries
    total_queries += 1
    return f"Query #{total_queries}"

# Simulate usage
open_connection()   # Connections: 1
open_connection()   # Connections: 2
print(execute_query())  # Query #1
close_connection()  # Connections: 1
```

---

## Variable Shadowing

A local variable can "hide" a global one:

```python
MAX_RETRIES = 3  # GLOBAL

def retry_with_override():
    """Local shadows global"""
    MAX_RETRIES = 5  # LOCAL (shadows global)
    print(f"Retries: {MAX_RETRIES}")  # Prints 5 (local)

retry_with_override()  # Retries: 5 (uses local)
print(MAX_RETRIES)     # 3 (global still 3)
```

---

## Practical Examples

### Example: Robot State Management

```python
# Global robot state
robot_status = {
    "battery": 100,
    "position": (0, 0),
    "moving": False
}

def move_robot(x, y):
    """Move robot to position"""
    global robot_status
    
    if robot_status["battery"] < 10:
        print("Battery too low!")
        return False
    
    robot_status["moving"] = True
    robot_status["position"] = (x, y)
    robot_status["battery"] -= 5
    robot_status["moving"] = False
    
    print(f"Moved to {robot_status['position']}")
    print(f"Battery: {robot_status['battery']}%")
    return True

def charge_robot():
    """Charge robot battery"""
    global robot_status
    robot_status["battery"] = 100
    print("Robot fully charged!")

def get_status():
    """Display robot status"""
    print(f"\nStatus:")
    for key, value in robot_status.items():
        print(f"  {key}: {value}")

# Simulate
move_robot(10, 20)
move_robot(15, 25)
get_status()
charge_robot()
```


---

## LEGB Rule (Variable Lookup Order)

Python searches for variables in this order:

1. **L**ocal - Inside current function
2. **E**nclosing - In outer functions (Module 6.4)
3. **G**lobal - Outside all functions
4. **B**uilt-in - Python's built-in names (print, len, etc.)

```python
message = "Global"  # GLOBAL

def outer():
    message = "Enclosing"  # ENCLOSING
    
    def inner():
        message = "Local"  # LOCAL
        print(message)  # Prints "Local" (uses local first)
    
    inner()

outer()

# Without local, searches enclosing
def outer2():
    message = "Enclosing"
    
    def inner2():
        print(message)  # No local, uses enclosing: "Enclosing"
    
    inner2()

outer2()

# Without both, uses global
def test():
    print(message)  # No local/enclosing, uses global: "Global"

test()
```

---
## Common Mistakes

### ❌ Mistake : Forgetting `global` Keyword

```python
counter = 0

# Doesn't work - creates local counter
def increment():
    counter = counter + 1  # UnboundLocalError!

# Works - tells Python to use global
def increment():
    global counter
    counter = counter + 1
```

---

## Milestone Task: Robot Energy Tracker

Track a robot’s battery level.

The battery level is a global variable, and functions will use and modify it.

### Requirements:
- Create a global variable `battery_level` (start at 100)
- Write a function `use_energy(amount)` that lowers the battery (local uses global)
- Write a function `recharge()` that sets battery back to 100
- Display battery level after each action

### Example Output
```bash
Battery Level: 100%
Robot is moving...
Battery Level: 80%
Recharging robot...
Battery Level: 100%
```
---

## What's Next?

Next module: **Recursion & Lambda Functions** - Advanced function techniques!

---

## References

- Python Scope: https://docs.python.org/3/tutorial/controlflow.html#python-scopes-and-namespaces
- Global Keyword: https://docs.python.org/3/reference/simple_stmts.html#global

