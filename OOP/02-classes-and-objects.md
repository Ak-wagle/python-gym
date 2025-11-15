# 02: Classes and Objects - Building Your Blueprint

## The Blueprint

Imagine an **admission form** at your college:

```
COLLEGE ADMISSION FORM (TEMPLATE/BLUEPRINT)
━━━━━━━━━━━━━━━━━━━━━━━━
□ Full Name: ___________
□ Roll Number: ________
□ Department: _________
□ Email: _______________
━━━━━━━━━━━━━━━━━━━━━━━━
```

This form is **reusable**. Every new student fills it, but each form has **different data**.

```
FILLED FORM 1              FILLED FORM 2
━━━━━━━━━━━━━━━━━━━        ━━━━━━━━━━━━━━━━━━━
Name: Donald               Name: Kamala
Roll: RA101                Roll: RA102
Dept: RA                   Dept: RA
Email: donald@gmail.com    Email: kamala@gmail.com
```

**In OOP terms:**
- **Class** = The blank admission form (blueprint)
- **Objects** = Filled forms (actual instances)

So referring to the Class (i.e., the main blank application form), you can create n number of objects (i.e., n number of students' actual applications).

---

## Creating Your First Class 

### Step 1: Define the Class

```python
class Student:
    pass  # We'll add content soon
```

**What's in it:** 
- `class` is a keyword that tells Python we're defining a class
- `Student` is the **class name** (convention: PascalCase)
- `:` indicates a code block follows
- `pass` is a placeholder (means "do nothing for now")

### Step 2: Create Objects (Instances)

```python
# Creating two Student objects
student1 = Student()
student2 = Student()

print(type(student1))  # <class '__main__.Student'>
print(type(student2))  # <class '__main__.Student'>
```

**Important:** 
- `Student()` **creates a new object** (the parentheses are crucial!)
- Each object is **independent**
- They are different objects in memory

---

## Understanding Object Identity

Every object has a unique **identity** in memory:

```python
student1 = Student()
student2 = Student()

print(id(student1))  # Example: 140734567891824
print(id(student2))  # Example: 140734567891936 (different!)

print(student1 == student2)  # False (different objects)
print(student1 is student2)  # False (different identities)
```

**Technical Details:**
- `id()` returns the **memory address** of an object
- `==` checks if values are equal
- `is` checks if they're the **same object**
- Each time you create an object, Python allocates new memory

---

## Adding Attributes (What Objects Know) 

Now let's give our Student class some **attributes**:

```python
class Student:
    def __init__(self, name, roll_number):
        self.name = name
        self.roll_number = roll_number
```

Let's break this down:

### The `__init__` Method
- **`__init__`** = "initialize" (called automatically when you create an object)
- **`self`** = refers to the object being created
- Think of it as a **constructor** (like in Java/C++)

### Creating Objects with Data

```python
# Create students with specific data
student1 = Student("Donald", "RA101")
student2 = Student("Kamala", "RA102")

# Access attributes using dot notation
print(student1.name)           # Donald
print(student1.roll_number)    # RA101
print(student2.name)           # Kamala
print(student2.roll_number)    # RA102
```

**Magic Behind the Scenes:**

When you write: `student1 = Student("Donald", "RA101")`

**Python does this:**
1. Creates a new Student object
2. Calls `__init__` with the object and arguments
3. `self` automatically becomes student1
4. `self.name = "Donald"` stores data in student1's memory

---

## Multiple Attributes Example 

```python
class Student:
    def __init__(self, name, roll_number, department, gpa):
        self.name = name
        self.roll_number = roll_number
        self.department = department
        self.gpa = gpa

# Create multiple students
students = [
    Student("Arjun", "CS101", "Computer Science", 8.5),
    Student("Sneha", "EC101", "Electronics", 9.2),
    Student("Karan", "ME101", "Mechanical", 8.8)
]

# Access each student's data
for student in students:
    print(f"{student.name} ({student.roll_number}) - GPA: {student.gpa}")
```

Here the three student objects are kept in a list, so the objects are accessed as: `students[0]`, `students[1]`, `students[2]`

**Output:**
```
Arjun (CS101) - GPA: 8.5
Sneha (EC101) - GPA: 9.2
Karan (ME101) - GPA: 8.8
```

---

## Adding Methods (What Objects Do)

Methods are **functions inside a class** that define behaviors:

```python
class Student:
    def __init__(self, name, roll_number, gpa):
        self.name = name
        self.roll_number = roll_number
        self.gpa = gpa
    
    def study(self, subject):
        """Method: Student studies a subject"""
        print(f"{self.name} is studying {subject}")
    
    def display_info(self):
        """Method: Display student information"""
        print(f"Name: {self.name}")
        print(f"Roll: {self.roll_number}")
        print(f"GPA: {self.gpa}")

# Create and use
student1 = Student("Donald", "RA101", 8.5)

student1.study("Python")       # Donald is studying Python
student1.display_info()        # Shows all info
```

**Technical Detail:**
- **`self`** is always the first parameter in methods
- It represents the object calling the method
- You don't pass it when calling the method!

**When you write:**
```python
student1.study("Python")
```

**Python automatically does:**
```python
Student.study(student1, "Python")
# self = student1, subject = "Python"
```

---

## Two Ways to Call Methods

### Way 1: Using the Object (Recommended) 
```python
student1.study("Python")  # self is automatically student1
```

### Way 2: Using the Class (Explicit) 
```python
Student.study(student1, "Python")  # Manually pass the object
```

Both work, but **Way 1 is Pythonic**!

---

## Complete College Example 

```python
class Student:
    def __init__(self, name, roll_number, department):
        self.name = name
        self.roll_number = roll_number
        self.department = department
        self.grades = {}  # Empty dictionary for grades
    
    def add_grade(self, subject, grade):
        """Add a grade for a subject"""
        self.grades[subject] = grade
        print(f"✓ Grade added: {subject} = {grade}")
    
    def display_profile(self):
        """Display complete student profile"""
        print(f"\n{'='*40}")
        print(f"Student Profile")
        print(f"{'='*40}")
        print(f"Name: {self.name}")
        print(f"Roll Number: {self.roll_number}")
        print(f"Department: {self.department}")
        print(f"Grades: {self.grades}")
        print(f"{'='*40}\n")

# Usage
student1 = Student("Donald Trumpesh", "RA101", "Robotics and Automation")
student1.add_grade("Python", "A")
student1.add_grade("C++", "A+")
student1.display_profile()

student2 = Student("Kamala Harish", "RA102", "Robotics and Automation")
student2.add_grade("Python", "B+")
student2.add_grade("C++", "A")
student2.display_profile()
```

**Output:**
```
✓ Grade added: Python = A
✓ Grade added: C++ = A+

========================================
Student Profile
========================================
Name: Donald Trumpesh
Roll Number: RA101
Department: Robotics and Automation
Grades: {'Python': 'A', 'C++': 'A+'}
========================================

✓ Grade added: Python = B+
✓ Grade added: C++ = A

========================================
Student Profile
========================================
Name: Kamala Harish
Roll Number: RA102
Department: Robotics and Automation
Grades: {'Python': 'B+', 'C++': 'A'}
========================================
```

---

## Comparing Objects 

```python
student1 = Student("Donald", "RA101", "RA")
student2 = Student("Donald", "RA101", "RA")    # Same data, different object
student3 = student1                            # Same object

print(student1 == student2)    # False (different objects)
print(student1 is student3)    # True  (same object in memory)

# Check how Python stores them
print(id(student1))  # Address 1
print(id(student2))  # Address 2 (different!)
print(id(student3))  # Address 1 (same as student1)
```

**Important:** Two objects with identical data are **not equal** unless they're the same object!

---

## Object Creation Process 

When you write `student1 = Student("Donald", "RA101", "RA")`, Python does this:

```
Step 1: __new__() - Allocate Memory
├─ Calls object.__new__()
├─ Creates empty object in heap memory
└─ Assigns unique ID/address

Step 2: __init__() - Initialize Data
├─ Automatically called by __new__()
├─ Receives the newly created object as 'self'
├─ Populates attributes (self.name, self.roll_number)
└─ Returns None (implicitly)

Step 3: Bind to Variable
├─ Assigns the object reference to student1
└─ student1 now "points to" that memory location
```

**Visual Representation:**
```
Memory Heap
┌─────────────────────────┐
│ Student Object #1       │
├─────────────────────────┤
│ name: "Donald"          │
│ roll_number: "RA101"    │
│ (id: 0x7f8c...)         │
└─────────────────────────┘
        ↑
        │ references
        │
    student1 (variable)
```

---

## Try It Yourself!

Create a Professor class with:
- Attributes: name, employee_id, subject, department
- Methods: teach(), display_info()

```python
class Professor:
    # Try to fill this in!
    pass
```

**Solution Template:**
```python
class Professor:
    def __init__(self, name, employee_id, subject, department):
        self.name = name
        self.employee_id = employee_id
        self.subject = subject
        self.department = department
    
    def teach(self, topic):
        print(f"Prof. {self.name} is teaching {topic} in {self.subject}")
    
    def display_info(self):
        print(f"Professor: {self.name}")
        print(f"Employee ID: {self.employee_id}")
        print(f"Subject: {self.subject}")
        print(f"Department: {self.department}")
```

---

## Diagrams [TODO]

> - A class blueprint vs multiple objects
> - Memory representation with object IDs
> - Method call flow with self parameter
> - The `__init__` execution process

---

## Next Module

**Coming Next:** Deep dive into `__init__`, the birth certificate of objects! -> [03-init-method.md](./03-init-method.md)