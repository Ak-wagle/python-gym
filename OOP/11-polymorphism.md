# 11: Polymorphism - Many Forms 

## What is Polymorphism? 

**Polymorphism** = "many forms" - same method name, different implementations:

```python
class Student:
    def work(self):
        print("Student: Studying books")

class Professor:
    def work(self):
        print("Professor: Teaching and researching")

class Principal:
    def work(self):
        print("Principal: Managing the college")

# Same method name, different behaviors!
student = Student()
professor = Professor()
principal = Principal()

student.work()      # Student: Studying books
professor.work()    # Professor: Teaching and researching
principal.work()    # Principal: Managing the college
```

---

## Polymorphism Through Inheritance

Override parent methods to create polymorphic behavior:

```python
class Person:
    """Parent class with base behavior"""
    def display_role(self):
        print("I am a person")

class Student(Person):
    """Child overrides method"""
    def display_role(self):
        print("I am a student")

class Professor(Person):
    """Child overrides method"""
    def display_role(self):
        print("I am a professor")

class TeachingAssistant(Person):
    """Child overrides method"""
    def display_role(self):
        print("I am a TA - both student and professor!")

# Create different objects
people = [
    Student(),
    Professor(),
    TeachingAssistant()
]

# Call SAME method on different objects
for person in people:
    person.display_role()  # Different output each time!
```
Output:
```bash
I am a student
I am a professor
I am a TA - both student and professor!
```

**This is POLYMORPHISM!** Same method `display_role()` behaves differently for each class.

---

## Polymorphic Collections 

Store different types in one list, treat them uniformly:

```python
class Shape:
    def area(self):
        pass

class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius
    
    def area(self):
        return 3.14 * self.radius ** 2

class Square(Shape):
    def __init__(self, side):
        self.side = side
    
    def area(self):
        return self.side ** 2

class Rectangle(Shape):
    def __init__(self, length, width):
        self.length = length
        self.width = width
    
    def area(self):
        return self.length * self.width

# One list with different shapes
shapes = [
    Circle(5),
    Square(4),
    Rectangle(3, 6)
]

# Polymorphic iteration
print("SHAPES AND THEIR AREAS:")
total_area = 0
for shape in shapes:
    area = shape.area()  # Polymorphism!
    print(f"Area: {area:.2f}")
    total_area += area

print(f"Total area: {total_area:.2f}")
```

---

## Duck Typing 🦆

**Duck Typing** = "If it walks like a duck and quacks like a duck, it's a duck!"

In Python, you don't need inheritance for polymorphism:

```python
# These classes don't inherit from common parent
class Smartphone:
    def ring(self):
        print("Ring ring! ")

class Doorbell:
    def ring(self):
        print("Ding dong! ")

class Bell:
    def ring(self):
        print("Ring a ding! ")

# But they all have ring() method
objects = [Smartphone(), Doorbell(), Bell()]

# Python doesn't care about inheritance!
for obj in objects:
    obj.ring()  # Works regardless of class!
```
Output:
```bash
Ring ring! 
Ding dong! 
Ring a ding! 
```

**Why Python accepts this:**
- Python uses **dynamic typing**
- Doesn't check class inheritance
- Only checks if method exists
- "If it has the method, use it!"

---

## Practice Exercise

Create a `Department` hierarchy:
- **Department** (base) - name, budget
- **CSE(Department)** - override show_details() for CS specifics
- **Electronics(Department)** - override show_details() for EC specifics
- Store multiple departments in a list and call show_details() on each

---

## Next Module 🤔