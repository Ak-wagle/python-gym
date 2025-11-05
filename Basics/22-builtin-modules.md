# Module 7.1: Built-in Modules

**Built-in modules** are Python's standard library - pre-installed packages that provide additional functionality without external installation. Common modules include `math` (mathematical functions), `random` (random number generation), `datetime` (date/time operations), and many others.

You import them with `import module_name` and access functions via `module_name.function()`.

**Key Technical Properties:**
- **Pre-installed**: No pip installation needed
- **Organized**: Functions grouped by purpose
- **Namespaced**: Functions accessed via module name
- **Well-documented**: Official Python documentation
- **Efficient**: Optimized, tested, production-ready
- **Aliasing**: Can import with shorter names (`import numpy as np`)

---

## Math Module

```python
import math

# Constants
print(math.pi)      # 3.14159...
print(math.e)       # 2.71828...

# Basic functions
print(math.sqrt(16))        # 4.0
print(math.ceil(4.3))       # 5 (round up)
print(math.floor(4.7))      # 4 (round down)
print(math.fabs(-10))       # 10.0 (absolute value)

# Trigonometric
print(math.sin(math.pi/2))  # 1.0
print(math.cos(0))          # 1.0
print(math.tan(math.pi/4))  # 1.0

# Power and logs
print(math.pow(2, 8))       # 256.0
print(math.log(10))         # Natural log
print(math.log10(100))      # Log base 10: 2.0

# Practical: Calculate distance
x1, y1 = 0, 0
x2, y2 = 3, 4
distance = math.sqrt((x2-x1)**2 + (y2-y1)**2)
print(f"Distance: {distance}")  # 5.0
```

---

## Random Module

```python
import random

# Random float (0.0 to 1.0)
print(random.random())      # 0.3849...

# Random integer in range
print(random.randint(1, 10))    # Random 1-10
print(random.randrange(0, 100, 5))  # Multiple of 5

# Choose from sequence
options = ["option1", "option2", "option3"]
print(random.choice(options))

# Shuffle list
deck = ["A", "B", "C", "D"]
random.shuffle(deck)
print(deck)  # Shuffled

# Sample (without replacement)
sample = random.sample(range(1, 100), 5)  # 5 random numbers 1-99
print(sample)

# Practical: Simulation
def roll_die():
    return random.randint(1, 6)

rolls = [roll_die() for _ in range(5)]
print(f"Rolls: {rolls}")
```

---

## DateTime Module

```python
from datetime import datetime, timedelta, date

# Current date/time
now = datetime.now()
print(now)  # 2025-11-05 15:30:45.123456

# Date components
print(now.year)      # 2025
print(now.month)     # 11
print(now.day)       # 5
print(now.hour)      # 15
print(now.minute)    # 30

# Create specific datetime
birth_date = datetime(1990, 5, 15)
print(birth_date)  # 1990-05-15 00:00:00

# Date arithmetic
today = date.today()
tomorrow = today + timedelta(days=1)
next_week = today + timedelta(weeks=1)
past = today - timedelta(days=30)

print(f"Today: {today}")
print(f"Tomorrow: {tomorrow}")
print(f"Next week: {next_week}")

# Duration between dates
start = datetime(2025, 1, 1)
end = datetime(2025, 12, 31)
duration = end - start
print(f"Days: {duration.days}")

# Format date/time
formatted = now.strftime("%Y-%m-%d %H:%M:%S")
print(formatted)  # 2025-11-05 15:30:45

# Parse string to datetime
date_string = "2025-11-05"
parsed = datetime.strptime(date_string, "%Y-%m-%d")
print(parsed)
```

---

## Other Useful Modules

```python
# String operations
import string
print(string.ascii_lowercase)    # 'abcdefghijklmnopqrstuvwxyz'
print(string.digits)             # '0123456789'

# Operating system
import os
print(os.getcwd())              # Current directory
print(os.listdir('.'))          # Files in current dir

# System information
import sys
print(sys.version)              # Python version
print(sys.platform)             # Operating system

# Regular expressions
import re
text = "Contact: email@example.com"
match = re.search(r'\S+@\S+', text)
if match:
    print(f"Found: {match.group()}")

# Statistics
from statistics import mean, median, stdev
data = [10, 20, 30, 40, 50]
print(f"Mean: {mean(data)}")
print(f"Median: {median(data)}")
print(f"Std Dev: {stdev(data)}")
```

---

## Practical Examples

### Example 1: Sensor Data Logger

```python
from datetime import datetime
import math
import random

def log_sensor_data():
    """Log simulated sensor data"""
    timestamp = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
    
    # Simulate sensor readings
    temperature = 20 + random.uniform(-2, 2)  # 18-22°C
    pressure = 1013 + random.uniform(-5, 5)   # 1008-1018 hPa
    
    # Calculate dew point (simplified)
    dew_point = temperature - (100 - 50) / 5
    
    print(f"{timestamp} | Temp: {temperature:.1f}°C | "
          f"Pressure: {pressure:.1f}hPa | Dew: {dew_point:.1f}°C")

# Log multiple readings
for _ in range(3):
    log_sensor_data()
```

### Example 2: Event Scheduler

```python
from datetime import datetime, timedelta
import calendar

def schedule_event(event_name, start_time, duration_hours):
    """Schedule and display event"""
    end_time = start_time + timedelta(hours=duration_hours)
    
    day_name = calendar.day_name[start_time.weekday()]
    
    print(f"\nEvent: {event_name}")
    print(f"Day: {day_name}")
    print(f"Start: {start_time.strftime('%Y-%m-%d %H:%M')}")
    print(f"End: {end_time.strftime('%Y-%m-%d %H:%M')}")
    print(f"Duration: {duration_hours} hours")

# Schedule meetings
meeting1 = datetime(2025, 11, 10, 14, 30)  # Nov 10, 2:30 PM
schedule_event("Team Meeting", meeting1, 1)

meeting2 = datetime(2025, 11, 12, 9, 0)    # Nov 12, 9:00 AM
schedule_event("Project Review", meeting2, 2)
```

---

## Milestone Task: Lucky Number Game
### Description:

Create a small program that:
- Generates a random lucky number
- Calculates something fun using the math module
- Shows the current date and time
- Displays everything in a neat output

Example Output:
```bash
=================================
        LUCKY NUMBER DRAW
=================================

Current Time: 2025-11-05 14:31:27
Your Lucky Number: 64
Square Root of Lucky Number: 8.0

            Good Luck!
=================================

```
---

## What's Next?

Next module: **External Libraries & pip** - Beyond the standard library!

---

## References

- Math: https://docs.python.org/3/library/math.html
- Random: https://docs.python.org/3/library/random.html
- DateTime: https://docs.python.org/3/library/datetime.html
- Standard Library: https://docs.python.org/3/library/

