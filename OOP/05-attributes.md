# 05: Attributes - What Objects Know

## Types of Attributes 

Every object can have two types of attributes:

### 1. Instance Variables 
- **Unique to each object**
- Each object has its own copy
- Defined in `__init__` or other instance methods
- Accessed via `self.attribute`

### 2. Class Variables 
- **Shared by all objects** of the class
- Defined at class level (outside methods)
- Accessed via `ClassName.variable` or `self.variable`
- Modified changes affect all objects

---

## Instance Variables (The Personal Way) 

```python
class Student:
    def __init__(self, name, roll_number, gpa):
        # These are INSTANCE variables
        self.name = name           # Unique to THIS student
        self.roll_number = roll_number  # Unique to THIS student
        self.gpa = gpa             # Unique to THIS student

# Create two students
student1 = Student("Raj", "CS101", 8.5)
student2 = Student("Priya", "CS102", 9.2)

# Each has their OWN data
print(student1.name)  # Raj
print(student2.name)  # Priya

# Modify one student's data
student1.gpa = 8.7
print(student1.gpa)   # 8.7
print(student2.gpa)   # 9.2 (unchanged!)
```

**Memory Visualization:**
```
┌─ student1's namespace ─┐
│ name: "Raj"            │
│ roll_number: "CS101"   │
│ gpa: 8.7               │
└────────────────────────┘

┌─ student2's namespace ─┐
│ name: "Priya"          │
│ roll_number: "CS102"   │
│ gpa: 9.2               │
└────────────────────────┘
```

--- 


## Class Variables (The Shared Way) 

```python
class Student:
    # This is a CLASS variable - shared by all Student objects!
    college_name = "Tech University"
    total_students = 0
    
    def __init__(self, name):
        self.name = name
        # Increment class variable when new student is created
        Student.total_students += 1

# Create students
student1 = Student("Raj")
student2 = Student("Priya")
student3 = Student("Arjun")

# Access class variable via object
print(student1.college_name)  # Tech University
print(student2.college_name)  # Tech University

# Access class variable via class
print(Student.college_name)   # Tech University

# Class variable showing total
print(Student.total_students)  # 3
```

**Memory Visualization:**
```
┌─── Class Namespace (SHARED) ────┐
│ college_name: "Tech University" │
│ total_students: 3               │
└─────────────────────────────────┘
                ↑
           ┌────┴────┐
  Shared by all Student objects

    ├─ student1's namespace ─┐
    │  name: "Raj"           │
    │                        │
    ├─ student2's namespace ─┐
    │  name: "Priya"         │
    │                        │
    ├─ student3's namespace ─┐
    │  name: "Arjun"         │
    └────────────────────────┘
```

---

## The Namespace Hierarchy 

Python searches for attributes in this order:

```
When you write: student1.college_name

Python searches:
1. Instance namespace (student1's own attributes)
   └─ Is 'college_name' in student1.__dict__? NO
2. Class namespace (Student class attributes)
   └─ Is 'college_name' in Student.__dict__? YES ✓
   └─ Return "Tech University"
```

### Visual Namespace Search
```
                         ┌──────────────────────┐
                         │ Instance Namespace   │
                         │ (student1.__dict__)  │
                         │                      │
student1.college_name ──→│ name: "Raj"          │ ←─ Check first
                         │ roll_number: "CS101" │
                         └──────────────────────┘
                                    ↓ NOT FOUND
                         ┌──────────────────────┐
                         │ Class Namespace      │
                         │ (Student.__dict__)   │
                         │                      │
                         │ college_name: "Uni"  │✓ Found!
                         │ total_students: 5    │
                         └──────────────────────┘
```

---

## Shadowing: Instance vs Class Variables  [TODO]

When an instance and class variable have the same name, instance variable **wins**:

```python
class Student:
    scholarship = 10000  # Class variable
    
    def __init__(self, name):
        self.name = name

student1 = Student("Raj")
student2 = Student("Priya")

# Initially, both use class variable
print(student1.scholarship)  # 10000 (from class)
print(student2.scholarship)  # 10000 (from class)

# Give student1 a special scholarship
student1.scholarship = 15000  # Creates INSTANCE variable

print(student1.scholarship)  # 15000 (from instance) ✓ Instance wins!
print(student2.scholarship)  # 10000 (from class)

# Modify class variable
Student.scholarship = 12000

print(student1.scholarship)  # 15000 (has own copy now)
print(student2.scholarship)  # 12000 (uses class variable)
```

**What Happened:**
```
Before assigning to student1:
student1.scholarship ──→ Instance? NO ──→ Class? YES ──→ 10000

After assigning to student1:
student1.scholarship ──→ Instance? YES ──→ 15000
student2.scholarship ──→ Instance? NO ──→ Class? YES ──→ 12000
```

---

## Inspecting Namespaces with `__dict__` 

Python exposes object's attributes via `__dict__`:

```python
class Student:
    college_name = "Tech Uni"
    
    def __init__(self, name, gpa):
        self.name = name
        self.gpa = gpa

student1 = Student("Raj", 8.5)

# See instance variables
print(student1.__dict__)
# Output: {'name': 'Raj', 'gpa': 8.5}

# See class variables
print(Student.__dict__)
# Output: {'college_name': 'Tech Uni', '__init__': <function...>, ...}

# Check if attribute exists
print('name' in student1.__dict__)        # True (instance variable)
print('college_name' in student1.__dict__) # False (class variable)
print('college_name' in Student.__dict__)  # True
```

---

## Modifying Class Variables (Be Careful!) 

There are two ways to access class variables, and they behave differently:

```python
class Student:
    total = 0

# Method 1: Via instance
s1 = Student()
s1.total = 10  # Creates INSTANCE variable, doesn't change class!

# Method 2: Via class
Student.total = 100  # Modifies the actual class variable

print(s1.total)        # 10 (instance variable)
print(Student.total)   # 100 (class variable)
```

---

## Practice Exercise 

Create a `Course` class with:
- **Class variables:** total_courses, university_name
- **Instance variables:** course_name, credits, instructor

Track total courses created. Create 3 courses and verify the count.

---

## Next Module

Coming Next: Methods - What Objects Do [06-methods.md](./06-methods.md)