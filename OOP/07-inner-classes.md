# 07: Inner Classes - Nested Organization

## What is an Inner Class? 

An **inner class** is a class defined **inside another class**. It's a way to organize related functionality:

```python
# Outer class
class College:
    name = "Tech University"
    
    # Inner class
    class Department:
        def __init__(self, dept_name):
            self.dept_name = dept_name

# Access
cse_dept = College.Department("Computer Science")
print(cse_dept.dept_name)  # Computer Science
```

**Real-World Analogy:**
- College is like a building
- Department is like a section within that building
- You access it via: `Building.Section`

---

## Why Use Inner Classes? 🤔

### 1. Logical Grouping
Keep related classes together:

```python
class Student:
    """Student representation"""
    
    class Address:
        """Student's address - related to Student"""
        def __init__(self, street, city):
            self.street = street
            self.city = city
    
    class ContactInfo:
        """Student's contact - related to Student"""
        def __init__(self, email, phone):
            self.email = email
            self.phone = phone
    
    def __init__(self, name):
        self.name = name
        self.address = None
        self.contact = None
```

### 2. Encapsulation
Hide implementation details:

```python
class Bank:
    """Bank system"""
    
    class Account:
        """Private account class - implementation detail"""
        def __init__(self, account_no, balance):
            self.account_no = account_no
            self.balance = balance
    
    def create_account(self, account_no):
        return self.Account(account_no, 0)
```

### 3. Prevent Name Conflicts
Use namespacing to avoid clashes:

```python
# Without inner classes - confusing names
class StudentAddress:
    pass

class ProfessorAddress:
    pass

# With inner classes - clear hierarchy
class Student:
    class Address:
        pass

class Professor:
    class Address:
        pass
```

---

## Creating and Using Inner Classes

### Step 1: Define the Inner Class

```python
class College:
    name = "Tech University"
    
    # Inner class - nested within College
    class Department:
        def __init__(self, dept_name, faculty_count):
            self.dept_name = dept_name
            self.faculty_count = faculty_count
        
        def display_info(self):
            print(f"Department: {self.dept_name}")
            print(f"Faculty: {self.faculty_count}")
```

### Step 2: Access the Inner Class

```python
# Create instance via outer class
cse = College.Department("Computer Science", 15)
cse.display_info()  # Department: Computer Science, Faculty: 15

ec = College.Department("Electronics", 10)
ec.display_info()   # Department: Electronics, Faculty: 10
```

**Syntax:**
```
OuterClass.InnerClass(arguments)
```

---

## College System Example 

```python
class College:
    """Main college class"""
    university_name = "Advanced Tech University"
    
    class Student:
        """Student inner class"""
        def __init__(self, name, roll_number):
            self.name = name
            self.roll_number = roll_number
        
        def introduce(self):
            print(f"I'm {self.name} ({self.roll_number})")
    
    class Course:
        """Course inner class"""
        def __init__(self, course_name, credits):
            self.course_name = course_name
            self.credits = credits
        
        def display_course(self):
            print(f"Course: {self.course_name} ({self.credits} credits)")
    
    class Department:
        """Department inner class"""
        def __init__(self, dept_name, head_professor):
            self.dept_name = dept_name
            self.head_professor = head_professor
            self.courses = []
        
        def add_course(self, course):
            self.courses.append(course)
        
        def display_info(self):
            print(f"\n{'='*50}")
            print(f"Department: {self.dept_name}")
            print(f"Head: {self.head_professor}")
            print(f"Courses: {len(self.courses)}")
            for course in self.courses:
                print(f"  - {course.course_name}")
            print(f"{'='*50}\n")

# Usage
# Create students
student1 = College.Student("Raj Kumar", "CS101")
student2 = College.Student("Priya Singh", "CS102")

# Create courses
python_course = College.Course("Python Programming", 4)
db_course = College.Course("Database Systems", 3)
web_course = College.Course("Web Development", 3)

# Create department
cse_dept = College.Department("Computer Science", "Dr. Sharma")
cse_dept.add_course(python_course)
cse_dept.add_course(db_course)
cse_dept.add_course(web_course)

# Display
student1.introduce()        # I'm Raj Kumar (CS101)
student2.introduce()        # I'm Priya Singh (CS102)
cse_dept.display_info()     # Shows department info
```

**Output:**
```
I'm Raj Kumar (CS101)
I'm Priya Singh (CS102)

==================================================
Department: Computer Science
Head: Dr. Sharma
Courses: 3
  - Python Programming
  - Database Systems
  - Web Development
==================================================
```

---

## Accessing `self` in Inner Classes 

Inner classes **don't automatically access the outer class** instance:

```python
class Outer:
    outer_attr = "Outer"
    
    class Inner:
        inner_attr = "Inner"
        
        def display(self):
            # CAN'T access outer instance like this
            # print(self.outer_attr)  # Error!
            
            # CAN access the Inner class
            print(self.inner_attr)  # Inner
            
            # CAN access Outer class directly
            print(Outer.outer_attr)  # Outer

inner_obj = Outer.Inner()
inner_obj.display()
```

---

## Multiple Levels of Nesting

You can nest classes deeper, but be careful about complexity:

```python
class University:
    """Level 1"""
    def __init__(self, name):
        self.name = name
    
    class College:
        """Level 2"""
        def __init__(self, college_name):
            self.college_name = college_name
        
        class Department:
            """Level 3"""
            def __init__(self, dept_name):
                self.dept_name = dept_name
            
            class Program:
                """Level 4"""
                def __init__(self, program_name):
                    self.program_name = program_name

# Access
uni = University("National Institute")
college = uni.College("Engineering College")
dept = college.Department("Computer Science")
program = dept.Program("B.Tech")

print(f"Program: {program.program_name}")  # Program: B.Tech
```

**⚠️ Warning:** Deep nesting gets confusing. Usually 2 levels is enough.

---

## Practice Exercise

Create a `Department` class with inner classes:
- `Course` (inner) - with name, credits
- `Professor` (inner) - with name, subject
- `Department` methods to add courses and professors

---

## Next Module

Coming Next: Inner classes let you organize structure. Now let's learn how classes can inherit from each other! [08-inheritance.md](./08-inheritance.md)
