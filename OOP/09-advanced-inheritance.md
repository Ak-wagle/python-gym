# 09: Advanced Inheritance - Multiple Inheritance & MRO 

## What is Multiple Inheritance? 

**Multiple inheritance** = a class inherits from **multiple parent classes**:

```python
# Single Inheritance (one parent)
class Student(Person):
    pass

# Multiple Inheritance (multiple parents)
class TA(Student, TeachingAssistant):  # Inherits from TWO classes!
    pass
```

**Real-World Example:**
```
TeachingAssistant
├─ Has teaching abilities (from TeachingStaff)
└─ Also has student knowledge (from Student)
```

---

## Creating Multiple Inheritance 

```python
class Person:
    def __init__(self, name):
        self.name = name
    
    def display_person_info(self):
        print(f"Person: {self.name}")

class Student(Person):
    def __init__(self, name, roll_number):
        super().__init__(name)
        self.roll_number = roll_number
    
    def study(self):
        print(f"{self.name} is studying")

class TeachingStaff(Person):
    def __init__(self, name, subject):
        super().__init__(name)
        self.subject = subject
    
    def teach(self):
        print(f"{self.name} is teaching {self.subject}")

# Multiple Inheritance: TA inherits from BOTH Student and TeachingStaff

class TeachingAssistant(Student, TeachingStaff):
    def __init__(self, name, roll_number, subject):
        # Call both parents? This gets tricky!
        Student.__init__(self, name, roll_number)
        TeachingStaff.__init__(self, name, subject)

# Create and use
ta = TeachingAssistant("Raj", "CS101", "Python")
ta.study()                    # Raj is studying
ta.teach()                    # Raj is teaching Python
ta.display_person_info()      # Person: Raj
```

---

## The Diamond Problem

The **Diamond Problem** occurs when a class inherits from multiple parents that share a common ancestor:

```
        Person
         /    \
        /      \
    Student  TeachingStaff
       |        |
       \       /
        \     /
   TeachingAssistant
```

**The Problem:**
```python
class Person:
    def display(self):
        print("Person")

class Student(Person):
    def display(self):
        print("Student")

class TeachingStaff(Person):
    def display(self):
        print("TeachingStaff")

class TA(Student, TeachingStaff):
    pass

ta = TA()
ta.display()  # Which display() should be called?
# Person → Student → TeachingStaff
```
Ambiguity! 😕

---

## Method Resolution Order (MRO)

**MRO** is the **order** Python searches for methods in an inheritance hierarchy:

### How MRO Works

Python uses the **C3 Linearization Algorithm** to determine MRO:

```python
class Person:
    pass

class Student(Person):
    pass

class TeachingStaff(Person):
    pass

class TA(Student, TeachingStaff):
    pass
```
See the MRO
```python
print(TA.mro())
# Output: [<class 'TA'>, <class 'Student'>, <class 'TeachingStaff'>, <class 'Person'>, <class 'object'>]
```

Or use __mro__

```python
print(TA.__mro__)
# Same output
```

**Search Order:**
```
TA → Student → TeachingStaff → Person → object
```

**Rules of MRO (C3 Linearization):**
1. **Left-to-right**: Search left parent before right
2. **Depth-first**: Search each parent fully before next
3. **Once per class**: Each class appears only once
4. **Preserve order**: Parent order in all definitions

---

## Using `super()` with Multiple Inheritance 

`super()` respects MRO and is **the preferred way** to call parent methods:

```python
class A:
    def show(self):
        print("A")

class B(A):
    def show(self):
        print("B")
        super().show()

class C(A):
    def show(self):
        print("C")
        super().show()

class D(B, C):
    def show(self):
        print("D")
        super().show()

d = D()
d.show()
# Output:
# D
# B
# C
# A

# Follows MRO: D → B → C → A → object
print(D.__mro__)
# [D, B, C, A, object]
```

**Why `super()` is Better:**
- Automatically follows MRO
- Works with any inheritance depth
- Respects the inheritance chain
- Cooperative multiple inheritance

---

## Checking Inheritance Relationships 

```python
class Person:
    pass

class Student(Person):
    pass

class TeachingStaff(Person):
    pass

class TA(Student, TeachingStaff):
    pass

ta = TA()

# Check direct parent
print(isinstance(ta, Student))       # True
print(isinstance(ta, TeachingStaff)) # True
print(isinstance(ta, Person))        # True (through both paths)

# Check subclass relationships
print(issubclass(TA, Student))       # True
print(issubclass(TA, TeachingStaff)) # True
print(issubclass(TA, Person))        # True

# See full inheritance chain
print(TA.__bases__)  
print(TA.mro())       
```

---

## Practice Exercise 

Create a multi-level college hierarchy:
- **Person** (base) - name, age
- **Student(Person)** - add roll_number
- **Staff(Person)** - add employee_id
- **ResearchAssistant(Student, Staff)** - has both roles
- Print MRO and test all methods

---

## Next module

Now that you understand complex inheritance, let's learn how to protect sensitive data! Coming Next: [10-encapsulation.md](./10-encapsulation.md)