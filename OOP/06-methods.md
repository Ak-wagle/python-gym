# 06: Methods - What Objects Do 

## Three Types of Methods 

Python classes support three kinds of methods, each with different purposes:

| Type | Receives | Use Case | Example |
|------|----------|----------|---------|
| **Instance** | `self` (the object) | Operate on specific object data | `student.study()` |
| **Class** | `cls` (the class) | Operate on class-level data | `Student.get_total()` |
| **Static** | Nothing special | Utility functions (no state) | `Student.is_leap_year(2024)` |

---

## Instance Methods: The Most Common 

Instance methods **operate on individual objects** and use `self`:

```python
class Student:
    def __init__(self, name, gpa):
        self.name = name
        self.gpa = gpa
    
    # Instance method
    def study(self, subject):
        print(f"{self.name} is studying {subject}")
    
    # Instance method
    def display_info(self):
        print(f"Name: {self.name}, GPA: {self.gpa}")
    
    # Instance method that returns a value
    def is_excellent_student(self):
        return self.gpa >= 9.0

# Usage
student1 = Student("Raj", 9.2)
student1.study("Python")              # Raj is studying Python
student1.display_info()               # Name: Raj, GPA: 9.2
if student1.is_excellent_student():
    print("✓ Excellent student!")     # ✓ Excellent student!
```

---

## Class Methods: Operating on the Class 

Class methods receive **the class itself** (not an instance) as the first parameter:

```python
class Student:
    total_students = 0  # Class variable
    
    def __init__(self, name):
        self.name = name
        Student.total_students += 1
    
    # Class method - decorated with @classmethod
    @classmethod
    def get_total_students(cls):
        return cls.total_students
    
    @classmethod
    def reset_counter(cls):
        cls.total_students = 0
    
    @classmethod
    def create_from_string(cls, student_string):
        """Create student from 'Name,Roll' format"""
        parts = student_string.split(",")
        name = parts[0].strip()
        return cls(name)

# Usage
s1 = Student("Raj")
s2 = Student("Priya")
s3 = Student("Arjun")

# Call class method via class
print(f"Total: {Student.get_total_students()}")  # 3

# Can also call via instance
print(f"Total: {s1.get_total_students()}")       # 3

# Create from string
s4 = Student.create_from_string("Sneha")
print(f"Total: {Student.get_total_students()}")  # 4
```

**Key Differences:**
```
Instance Method:
- Receives self (the object)
- Can access/modify instance variables
- Called via object: student1.method()
- No decorator needed

Class Method:
- Receives cls (the class)
- Can access/modify class variables
- Called via class: Student.method() or object: student1.method()
- Requires @classmethod decorator
```

---

## Static Methods: Utility Functions

Static methods **don't receive** `self` or `cls`. They're like regular functions but grouped with the class:

```python
class Student:
    @staticmethod
    def is_valid_gpa(gpa):
        """Check if GPA is in valid range"""
        return 0.0 <= gpa <= 10.0
    
    @staticmethod
    def is_weekend(day):
        """Check if it's a weekend"""
        return day in ["Saturday", "Sunday"]
    
    @staticmethod
    def calculate_percentage(marks, total=100):
        """Convert marks to percentage"""
        return (marks / total) * 100

# Usage - no need for objects!
print(Student.is_valid_gpa(8.5))       # True
print(Student.is_valid_gpa(15.0))      # False
print(Student.is_weekend("Monday"))    # False
print(Student.is_weekend("Saturday"))  # True
print(Student.calculate_percentage(85)) # 85.0
```

**When to Use Static Methods:**
- Utility functions related to the class
- Don't need object or class state
- Helper functions that logically belong to the class

---

## All Three Methods in a Program

```python
class College:
    total_colleges = 0  # Class variable
    
    def __init__(self, name, city):
        self.name = name              # Instance variable
        self.city = city              # Instance variable
        College.total_colleges += 1
    
    # INSTANCE METHOD - operates on specific college
    def display_info(self):
        print(f"{self.name} in {self.city}")
    
    # CLASS METHOD - operates on class-level data
    @classmethod
    def total_in_country(cls):
        return f"Total colleges: {cls.total_colleges}"
    
    # STATIC METHOD - utility function
    @staticmethod
    def is_valid_city(city):
        valid_cities = ["Delhi", "Mumbai", "Bangalore"]
        return city in valid_cities

# Create instances
college1 = College("Tech University", "Delhi")
college2 = College("Engineering College", "Bangalore")

# Instance method - operates on specific college
college1.display_info()           # Tech University in Delhi

# Class method - operates on class
print(College.total_in_country()) # Total colleges: 2

# Static method - utility
print(College.is_valid_city("Delhi"))  # True
print(College.is_valid_city("Chennai")) # False
```

---

## Practice Exercise 

Create a `Course` class with:
- **Instance method:** `enroll_student(name)` - adds to course
- **Class method:** `total_courses_created()` - returns total created
- **Static method:** `is_valid_credits(credits)` - checks if 1-4 range

---
 
## Next Module

Coming Next: Inner Classes - Classes Within Classes [07-inner-classes.md](./07-inner-classes.md)