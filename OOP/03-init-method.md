# 03: The `__init__` Method - Your Object's Birth Certificate

## The Initialization Problem 🤔

Without `__init__`, creating meaningful objects is awkward:

WITHOUT __init__ - The painful way

```python
class Student:
   pass

student1 = Student()
# Now manually assign everything
student1.name = "Raj"
student1.roll_number = "CS101"
student1.gpa = 8.5

student2 = Student()
student2.name = "Priya"
student2.roll_number = "CS102"
student2.gpa = 9.2
```
This is messy, repetitive, and error-prone!

---

## Solution: The `__init__` Method
WITH __init__ - The clean way

```python
class Student:
   def __init__(self, name, roll_number, gpa):
       self.name = name
       self.roll_number = roll_number
       self.gpa = gpa

# Create students in one line!
student1 = Student("Raj", "CS101", 8.5)
student2 = Student("Priya", "CS102", 9.2)

print(student1.name)  # Raj
print(student2.gpa)   # 9.2
```

**Magic:** `__init__` is called **automatically** when you create an object!

---

## How `__init__` Works

### The Lifecycle

```
You write:     student1 = Student("Raj", "CS101", 8.5)
                       ↓
       Python creates empty object in memory
                       ↓
       Python calls __init__(student1, "Raj", "CS101", 8.5)
                       ↓
       self.name = "Raj"
       self.roll_number = "CS101"
       self.gpa = 8.5
                       ↓
       student1 is now initialized and ready to use!
```

### Visual Representation

```
┌──────────────────────────────────┐
│ Student.__init__ Execution       │
├──────────────────────────────────┤
│ Parameters:                      │
│  self → student1 (the object)    │
│  name → "Raj"                    │
│  roll_number → "CS101"           │
│  gpa → 8.5                       │
├──────────────────────────────────┤
│ Assignments:                     │
│  student1.name = "Raj"           │
│  student1.roll_number = "CS101"  │
│  student1.gpa = 8.5              │
└──────────────────────────────────┘
```

---

## Understanding `self` in `__init__`

`self` **always refers to the object being created**:

```python
class Student:
   def __init__(self, name, roll_number):
       self.name = name                     # self = the new object
       self.roll_number = roll_number       # assign its attributes
       print(f"Created: {self.name}")       # Can use self here too!

student1 = Student("Raj", "CS101")           # Created: Raj
student2 = Student("Priya", "CS102")         # Created: Priya
```

**What's happening:**
```
student1 = Student("Raj", "CS101")
        ↓
   self = student1
   self.name = "Raj"           → student1.name = "Raj"
   self.roll_number = "CS101"  → student1.roll_number = "CS101"

student2 = Student("Priya", "CS102")
        ↓
   self = student2
   self.name = "Priya"         → student2.name = "Priya"
   self.roll_number = "CS102"  → student2.roll_number = "CS102"
```

---

## Parameter Passing in `__init__`

### Important: self is NOT a parameter you pass!

```python
class Student:
   def __init__(self, name, roll_number):
       self.name = name
       self.roll_number = roll_number

# CORRECT
student = Student("Raj", "CS101")

# WRONG - self is automatic!
student = Student(student, "Raj", "CS101")  # ERROR!
```

---

## Real-World College Example

```python
class Professor:
   def __init__(self, name, employee_id, subject, department):
       self.name = name
       self.employee_id = employee_id
       self.subject = subject
       self.department = department
       self.students_taught = 0
       print(f"✓ Professor {name} initialized")

class Course:
   def __init__(self, course_name, credits, professor):
       self.course_name = course_name
       self.credits = credits
       self.professor = professor
       self.enrollment = 0

# Create instances
prof1 = Professor("Dr. Sharma", "EMP001", "Python", "CSE")
prof2 = Professor("Dr. Verma", "EMP002", "Database", "CSE")

course1 = Course("Advanced Python", 4, prof1)
course2 = Course("Database Systems", 3, prof2)

print(course1.course_name)     # Advanced Python
print(course1.professor.name)  # Dr. Sharma
```

**Output:**
```
✓ Professor Dr. Sharma initialized
✓ Professor Dr. Verma initialized
Advanced Python
Dr. Sharma
```

---

## Default Parameters in `__init__`

You can provide **default values** for parameters:

```python
class Student:
   def __init__(self, name, roll_number, gpa=0.0, department="Undecided"):
       self.name = name
       self.roll_number = roll_number
       self.gpa = gpa
       self.department = department
```

Create with all parameters
```python
student1 = Student("Raj", "CS101", 8.5, "Computer Science")
```

Create with defaults
```python
student2 = Student("Priya", "CE101")  # gpa=0.0, department="Undecided"
```

Mix and match
```python
student3 = Student("Arjun", "EC101", department="Electronics")

print(student1.gpa)         # 8.5
print(student2.gpa)         # 0.0
print(student2.department)  # Undecided
print(student3.department)  # Electronics
```

**Use Case:**
```python
class Department:
   def __init__(self, name, head="TBD", budget=100000):
       self.name = name
       self.head = head
       self.budget = budget

# Can create quickly
cse = Department("Computer Science")  # Uses defaults

# Or customize
ec = Department("Electronics", head="Dr. Singh", budget=150000)
```

---

## Multiple Objects, Independent Data

Each object maintains its **own copy** of attributes:

```python
class Student:
   def __init__(self, name, gpa):
       self.name = name
       self.gpa = gpa

student1 = Student("Raj", 8.5)
student2 = Student("Priya", 9.2)

# Change student1's data
student1.gpa = 8.7

# student2 is unaffected
print(student1.gpa)                # 8.7
print(student2.gpa)                # 9.2 (unchanged!)

# Prove they're different objects
print(student1 is student2)        # False
print(id(student1))                # Different memory address
print(id(student2))                # Different memory address
```

**Memory Layout:**
```
┌─ Memory Address 0x7f1 ─────┐
│ Student Object 1           │
│ name: "Raj"                │
│ gpa: 8.7 ✓ (modified)      │
└────────────────────────────┘

┌─ Memory Address 0x8a2 ─────┐
│ Student Object 2           │
│ name: "Priya"              │
│ gpa: 9.2 (unchanged)       │
└────────────────────────────┘

student1 → 0x7f1
student2 → 0x8a2
```

---

## Technical Deep Dive: `__new__` vs `__init__` 

Python actually uses **two methods** to create objects:

### `__new__()` - Object Creation & Memory Allocation
```python
def __new__(cls, *args, **kwargs):
   # Step 1: Allocate memory
   # Step 2: Return the newly created object
   return super().__new__(cls)
```

**What it does:**
- Allocates memory for the object
- Called BEFORE `__init__`
- Returns the created object
- You rarely override this

### `__init__()` - Object Initialization
```python
def __init__(self, name, roll_number):
   # Step 1: Receive the object from __new__
   # Step 2: Initialize its attributes
   self.name = name
   self.roll_number = roll_number
```

**What it does:**
- Called AFTER `__new__`
- Receives the object that `__new__` created
- Sets up initial state
- This is what you usually override

### The Complete Flow

![__new__ vs __init__](image-2.png)
```
student = Student("Raj", "CS101")
       ↓
  Student.__new__ runs
  ├─ Allocates memory
  ├─ Creates empty Student object
  └─ Returns the object
       ↓
  Student.__init__ runs
  ├─ Receives the object as 'self'
  ├─ Sets self.name = "Raj"
  ├─ Sets self.roll_number = "CS101"
  └─ Returns None (implicitly)
       ↓
  student now references the initialized object
```

**Visualization:**
```
Timeline:
Time 0: __new__ creates empty shell in memory
       Memory Address: 0x7f8c4029a2b0
       Content: {}
      
Time 1: __init__ fills in the data
       Content: {name: "Raj", roll_number: "CS101"}
      
Time 2: Variable student points to this object
       student → 0x7f8c4029a2b0
```

---

##  Try It Yourself!

Create a `Course` class with `__init__` that takes:
- `course_name`
- `credits`
- `instructor_name`
- `capacity` (optional, default=30)

Then create 3 course objects:
1. "Python Programming", 4 credits, "Dr. Sharma"
2. "Database Systems", 3 credits, "Dr. Verma", capacity=20
3. "Web Development", 3 credits, "Prof. Singh"

---

## Next Module

Coming Next: You now understand HOW `__init__` works. But what exactly is `self` and why is it so important? [04-self.md](./04-self.md)
