# 08: Inheritance - The Family Tree 

## What is Inheritance? 

**Inheritance** lets a new class **inherit attributes and methods** from an existing class:

```
Parent Class (General Features)
    ↑
    ├─ Child Class 1 (Specific Features)
    ├─ Child Class 2 (Specific Features)
    └─ Child Class 3 (Specific Features)
```

**Real-World Example:**
```
Person (Parent)
    ├─ Student (Child) - has all Person features + Student-specific features
    ├─ Professor (Child) - has all Person features + Professor-specific features
    └─ Principal (Child) - has all Person features + Principal-specific features
```

---

## Why Inheritance?

### Problem Without Inheritance:
```python
# LOTS OF DUPLICATION

class Student:
    def __init__(self, name, age, email):
        self.name = name
        self.age = age
        self.email = email
    
    def display_info(self):
        print(f"{self.name}, {self.age}")

class Professor:
    def __init__(self, name, age, email):
        self.name = name      # Duplicated!
        self.age = age        # Duplicated!
        self.email = email    # Duplicated!
    
    def display_info(self):
        print(f"{self.name}, {self.age}")  # Duplicated!

```

### Solution With Inheritance:
```python
# DRY - Don't Repeat Yourself 😅

class Person:
    """Parent class - common attributes"""
    def __init__(self, name, age, email):
        self.name = name
        self.age = age
        self.email = email
    
    def display_info(self):
        print(f"{self.name}, {self.age}")

class Student(Person):
    """Child class - inherits from Person"""
    def __init__(self, name, age, email, roll_number):
        super().__init__(name, age, email)  # Call parent's __init__
        self.roll_number = roll_number

class Professor(Person):
    """Child class - inherits from Person"""
    def __init__(self, name, age, email, employee_id):
        super().__init__(name, age, email)  # Call parent's __init__
        self.employee_id = employee_id

```

---

## Creating Inheritance 

### Step 1: Define Parent Class

```python
class Person:
    """The parent/superclass"""
    def __init__(self, name, age):
        self.name = name
        self.age = age
    
    def display(self):
        print(f"Name: {self.name}, Age: {self.age}")
```

### Step 2: Create Child Class

```python
class Student(Person):  # (Person) means inherit from Person
    """The child/subclass"""
    def __init__(self, name, age, roll_number):
        super().__init__(name, age)  # Call parent's __init__
        self.roll_number = roll_number
```

### Step 3: Use Both

```python
student = Student("Raj", 20, "CS101")
student.display()      # Inherited method!  # Name: Raj, Age: 20
print(student.name)    # Inherited attribute! # Raj
```

---

## Example 

```python
# Parent class
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age
    
    def display_basic_info(self):
        print(f"Name: {self.name}, Age: {self.age}")

# Child class 1
class Student(Person):
    def __init__(self, name, age, roll_number, gpa):
        super().__init__(name, age)
        self.roll_number = roll_number
        self.gpa = gpa
    
    def display_info(self):
        self.display_basic_info()
        print(f"Roll: {self.roll_number}, GPA: {self.gpa}")
    
    def study(self):
        print(f"{self.name} is studying")

# Child class 2
class Professor(Person):
    def __init__(self, name, age, employee_id, subject):
        super().__init__(name, age)
        self.employee_id = employee_id
        self.subject = subject
    
    def display_info(self):
        self.display_basic_info()
        print(f"ID: {self.employee_id}, Subject: {self.subject}")
    
    def teach(self):
        print(f"Prof. {self.name} is teaching {self.subject}")

# Child class 3
class Principal(Person):
    def __init__(self, name, age, employee_id, years_experience):
        super().__init__(name, age)
        self.employee_id = employee_id
        self.years_experience = years_experience
    
    def display_info(self):
        self.display_basic_info()
        print(f"ID: {self.employee_id}, Experience: {self.years_experience} years")
    
    def manage_college(self):
        print(f"{self.name} is managing the college")

# Usage
student = Student("Raj Kumar", 20, "CS101", 8.5)
professor = Professor("Dr. Sharma", 45, "EMP001", "Python")
principal = Principal("Dr. Patel", 55, "PRINCIPAL01", 20)

print("="*50)
student.display_info()      # Name: Raj Kumar, Age: 20, Roll: CS101, GPA: 8.5
student.study()             # Raj Kumar is studying

print("="*50)
professor.display_info()    # Name: Dr. Sharma, Age: 45, ID: EMP001, Subject: Python
professor.teach()           # Prof. Dr. Sharma is teaching Python

print("="*50)
principal.display_info()    # Name: Dr. Patel, Age: 55, ID: PRINCIPAL01, Experience: 20 years
principal.manage_college()  # Dr. Patel is managing the college
```

---

## Understanding `super()` 

`super()` lets you **call the parent class's methods**:

```python
class Person:
    def __init__(self, name):
        self.name = name
        print(f"Person __init__ called")

class Student(Person):
    def __init__(self, name, roll):
        super().__init__(name)  # ← Calls Person.__init__
        self.roll = roll
        print(f"Student __init__ called")

student = Student("Raj", "CS101")
```

Output:
```bash
# Person __init__ called
# Student __init__ called
```

**Why `super()` is Needed:**
```
Without super():
- You must hardcode the parent class name
- Doesn't work well with multiple inheritance
- Less flexible

With super():
- Automatically finds the parent class
- Works with inheritance chains
- More Pythonic
```

---

## Method Overriding 

**Override** = redefine a parent method in child class:

```python
class Person:
    def display(self):
        print("I am a person")

class Student(Person):
    def display(self):  # Override parent's method
        print("I am a student")
        super().display()  # Can still call parent's version

class Professor(Person):
    def display(self):  # Override parent's method
        print("I am a professor")
        # Not calling parent's display

# Usage
student = Student()
student.display()
# Output:
# I am a student
# I am a person

professor = Professor()
professor.display()
# Output:
# I am a professor
```

---

## The Power of Polymorphism Through Inheritance

Different classes, same method name, different behavior:

```python
class Person:
    def work(self):
        pass  # To be overridden

class Student(Person):
    def work(self):
        print("Student: Studying and doing assignments")

class Professor(Person):
    def work(self):
        print("Professor: Teaching and conducting research")

class Principal(Person):
    def work(self):
        print("Principal: Managing the college")

# Now we can treat all the same!
people = [
    Student(),
    Professor(),
    Principal(),
]

for person in people:
    person.work()  # Different output for each!

# Output:
# Student: Studying and doing assignments
# Professor: Teaching and conducting research
# Principal: Managing the college
```

**This is POLYMORPHISM** - same method name, different behaviors! (Same Same but Different 😅)

--- 

## Checking Inheritance Relationships

```python
class Person:
    pass

class Student(Person):
    pass

student = Student()

# Check if student is instance of Student
print(isinstance(student, Student))  # True

# Check if student is instance of Person (parent)
print(isinstance(student, Person))   # True

# Check inheritance relationship
print(issubclass(Student, Person))   # True
print(issubclass(Person, Student))   # False

# Get class info
print(type(student))                 # <class 'Student'>
print(Student.__bases__)             # (<class 'Person'>,)
print(Student.__mro__)               # Method Resolution Order - we'll learn soon!
```

---

## Accessing Parent and Child Attributes

```python
class Person:
    def __init__(self, name):
        self.name = name            # Parent attribute

class Student(Person):
    def __init__(self, name, roll):
        super().__init__(name)
        self.roll = roll            # Child attribute

student = Student("Raj", "CS101")

# Access parent attribute
print(student.name)    # Raj (inherited)

# Access child attribute
print(student.roll)    # CS101

# Both are accessible!
print(f"{student.name} - {student.roll}")  # Raj - CS101
```

---

## Inheritance Hierarchy

```python
class Person:
    """Level 0 - Base class"""
    pass

class Staff(Person):
    """Level 1 - Staff inherits from Person"""
    pass

class TeachingStaff(Staff):
    """Level 2 - TeachingStaff inherits from Staff"""
    pass

class Professor(TeachingStaff):
    """Level 3 - Professor inherits from TeachingStaff"""
    pass

# Each level inherits from previous
professor = Professor()
print(isinstance(professor, Professor))      # True
print(isinstance(professor, TeachingStaff))  # True
print(isinstance(professor, Staff))          # True
print(isinstance(professor, Person))         # True
```

---

## Technical Detail: Method Resolution Order (MRO) 

Python searches for methods in this order:
1. The object's own class
2. Parent classes (left to right)
3. Grandparent classes
4. Until `object` class

```python
class Person:
    def display(self):
        print("Person")

class Student(Person):
    def display(self):
        print("Student")

class GoodStudent(Student):
    pass

obj = GoodStudent()
obj.display()
# Search: GoodStudent → Student → Person
# Found in Student! Prints: Student
```

---

## Practice Exercise 

Create a college hierarchy:
- **Person** (parent) - name, age
- **Student** (child) - add roll_number, gpa
- **Staff** (child) - add employee_id
- **Professor** (child of Staff) - add subject
- **NonTeachingStaff** (child of Staff) - add department

Create instances and test inheritance!

---

## Next Module
→ Next: Advanced Inheritance [09-advanced-inheritance.md](./09-advanced-inheritance.md)