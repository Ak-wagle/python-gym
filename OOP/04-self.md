# 04: Understanding `self` - The Mirror of Identity

## The Core Problem: Multiple Objects, One Method

Without `self`, how would Python know which student is studying?

```python
class Student:
    def __init__(self, name):
        self.name = name
    
    def study(self):
        print("is studying")  # Which student??

student1 = Student("Raj")
student2 = Student("Priya")

student1.study()  # Whose data should this use? Raj's or Priya's?
student2.study()  # Same question!
```

**The Answer:** `self` tells Python which object to operate on!

---

## What is `self`? 

**`self` is a reference to the object that called the method.**

Think of it like a name tag:
- When Raj calls `student1.study()`, the method knows `self = student1`
- When Priya calls `student2.study()`, the method knows `self = student2`
- The method code is **shared**, but `self` is **unique** for each object

```python
class Student:
    def __init__(self, name):
        self.name = name
    
    def study(self):
        # self is the object that called this method
        print(f"{self.name} is studying")

student1 = Student("Raj")
student2 = Student("Priya")

student1.study()  # self = student1, prints: Raj is studying
student2.study()  # self = student2, prints: Priya is studying
```

**The Magic:**
```
When you write:  student1.study()
Python does:     Student.study(student1)
                          ↑ automatically passes student1
                 
When you write:  student2.study()
Python does:     Student.study(student2)
                          ↑ automatically passes student2
```

---

## `self` in `__init__` (Constructor)

In `__init__`, `self` is the newly created object:

```python
class Student:
    def __init__(self, name, roll_number):
        # self is the new Student object being created
        self.name = name                      # Attach name to THIS object
        self.roll_number = roll_number        # Attach roll_number to THIS object

# Create first object
student1 = Student("Raj", "CS101")
# During __init__: self = student1
# After: student1.name = "Raj", student1.roll_number = "CS101"

# Create second object
student2 = Student("Priya", "CS102")
# During __init__: self = student2
# After: student2.name = "Priya", student2.roll_number = "CS102"

print(student1.name)                         # Raj (stored in student1's namespace)
print(student2.name)                         # Priya (stored in student2's namespace)
```

**Memory Perspective:**
After creating both objects:
```bash
student1 ─→ ┌─────────────────────┐
            │ Student Object 1    │
            │ name: "Raj"         │
            │ roll_number: "CS101"│
            └─────────────────────┘

student2 ─→ ┌─────────────────────┐
            │ Student Object 2    │
            │ name: "Priya"       │
            │ roll_number: "CS102"│
            └─────────────────────┘

```

Each object has its OWN namespace (thanks to self!) 

---

## `self` in Methods

Every method automatically receives `self` as the first parameter:

```python
class Student:
    def __init__(self, name, gpa):
        self.name = name
        self.gpa = gpa
    
    def study(self, subject):
        # self = the student studying
        print(f"{self.name} is studying {subject}")
    
    def get_info(self):
        # self = the student whose info we want
        return f"{self.name} has GPA {self.gpa}"
    
    def compare_gpa(self, other_student):
        # self = this student, other_student = different student
        if self.gpa > other_student.gpa:
            return f"{self.name} has higher GPA than {other_student.name}"
        else:
            return f"{self.name} has lower or equal GPA"

student1 = Student("Raj", 8.5)
student2 = Student("Priya", 9.2)

student1.study("Python")                    # Raj is studying Python
print(student2.get_info())                  # Priya has GPA 9.2
print(student1.compare_gpa(student2))       # Raj has lower or equal GPA
```

**Method Call Breakdown:**
```
student1.study("Python")
     ↓
Method receives:
- self = student1
- subject = "Python"
     ↓
Executes: print(f"{student1.name} is studying Python")
     ↓
Output: Raj is studying Python
```

---

## Practice Exercise

Create a `Course` class with:
- `__init__`: takes name, credits, max_students
- `enroll_student(self, student_name)`: adds to enrollment list
- `get_enrollment_count(self)`: returns how many students
- `compare_size(self, other_course)`: compares enrollment with another course

Then create 2 courses and enroll students in both.

---

## Next Module
Coming Next: Now that you understand `self`, let's explore what data objects can store! [05-attributes.md](./05-attributes.md)