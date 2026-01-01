# 10: Encapsulation - Data Protection 

## The Privacy Spectrum 

Python supports three levels of attribute visibility:

| Level | Prefix | Visibility | Use Case |
|-------|--------|------------|----------|
| **Public** | none | Accessible anywhere | Normal attributes |
| **Protected** | `_` | Internal use, but accessible | Subclass modifications |
| **Private** | `__` | Hidden, name-mangled | Sensitive data |

---

## Public Attributes - Open Access 

Public attributes can be accessed and modified freely:

```python
class Student:
    def __init__(self, name):
        self.name = name       # Public attribute

student = Student("Raj")
print(student.name)            # Raj
student.name = "Priya"         # Can change freely
print(student.name)            # Priya
```

**When to use:** General-purpose data

---

## Protected Attributes - Internal Use 

Single underscore `_` indicates "internal use" (by convention, not enforced):

```python
class Student:
    def __init__(self, name, internal_id):
        self.name = name
        self._internal_id = internal_id  # Protected
    
    def get_internal_id(self):
        return self._internal_id

student = Student("Raj", "PRIVATE123")
print(student._internal_id)  # Can access, but shouldn't! 
```

Clear intent: "_internal_id" means "use carefully"

**Convention:**
- `_attribute` = "I'm internal, use my getter/setter methods instead"
- Python allows access but signals: "Don't touch directly!"

**When to use:** Data meant for subclasses or internal methods

---

## Private Attributes - Name Mangling 

Double underscore `__` triggers **name mangling** (actual privacy):

```python
class Student:
    def __init__(self, name, password):
        self.name = name
        self.__password = password  # Private!
    
    def get_password(self):
        return self.__password

student = Student("Raj", "secret123")

# Try to access directly
print(student.__password)  #  AttributeError!

# But it's still there, just renamed!
print(student._Student__password)  # secret123 (name mangled)

# Use the method instead
print(student.get_password())  # secret123 
```

**Name Mangling Details:**
```
__password becomes _ClassName__password

Why? To prevent accidental conflicts in inheritance!

class Student:
    def __init__(self):
        self.__marks = 85

class ScholarStudent(Student):
    def __init__(self):
        super().__init__()
        self.__marks = 95  # Different attribute!
        # student.__marks refers to ScholarStudent's, not Student's
```

**When to use:** Sensitive data (passwords, IDs, internal state)

---

## Getters and Setters 🎚️

**Getter** = method to read a private attribute  
**Setter** = method to write a private attribute

```python
class Student:
    def __init__(self, name, gpa):
        self.__name = name
        self.__gpa = gpa
    
    # Getter for name
    def get_name(self):
        return self.__name
    
    # Setter for name
    def set_name(self, new_name):
        if new_name and len(new_name) > 0:
            self.__name = new_name
        else:
            print("Invalid name!")
    
    # Getter for GPA
    def get_gpa(self):
        return self.__gpa
    
    # Setter for GPA with validation
    def set_gpa(self, new_gpa):
        if 0.0 <= new_gpa <= 10.0:
            self.__gpa = new_gpa
        else:
            print("GPA must be between 0 and 10!")

student = Student("Raj", 8.5)
print(student.get_name())      # Raj
student.set_name("Rajesh")     # Updated
print(student.get_name())      # Rajesh

student.set_gpa(15.0)          # Rejected!
student.set_gpa(9.5)           # Accepted
print(student.get_gpa())       # 9.5
```

---

## The @property Decorator - Pythonic Access

Instead of `get_name()` and `set_name()`, use `@property` for elegant syntax:

```python
class Student:
    def __init__(self, name, gpa):
        self.__name = name
        self.__gpa = gpa
    
    # Getter - looks like attribute access!
    @property
    def name(self):
        return self.__name
    
    # Setter - looks like assignment!
    @name.setter
    def name(self, new_name):
        if new_name and len(new_name) > 0:
            self.__name = new_name
        else:
            print("Invalid name!")
    
    @property
    def gpa(self):
        return self.__gpa
    
    @gpa.setter
    def gpa(self, new_gpa):
        if 0.0 <= new_gpa <= 10.0:
            self.__gpa = new_gpa
        else:
            print("GPA must be between 0 and 10!")

student = Student("Raj", 8.5)

# Read like normal attribute
print(student.name)     # Raj

# Assign like normal attribute
student.name = "Rajesh"
print(student.name)     # Rajesh

# But with validation!
student.gpa = 15.0      # Prints: GPA must be between 0 and 10!
student.gpa = 9.5       # Works
print(student.gpa)      # 9.5
```

**Magic:** This looks like direct attribute access but calls methods behind the scenes!

---

## Read-Only Properties

Sometimes you want a getter but NO setter (read-only):

```python
class Student:
    def __init__(self, name, roll):
        self.__name = name
        self.__roll = roll  # Should never change!
    
    @property
    def roll(self):
        """Can read roll number"""
        return self.__roll
    
    # NO setter for roll - it's read-only!

student = Student("Raj", "CS101")
print(student.roll)     # CS101

student.roll = "CS102"  # AttributeError: can't set attribute!
```

---

## Practice Exercise 

Create a `BankAccount` class with:
- **Private:** balance, pin
- **Protected:** transaction_history
- **Public:** account_holder
- Methods: deposit(), withdraw() (with validation), check_balance()

---

## Next Module

Coming Next: Polymorphism - Many Forms [11-polymorphism.md](./11-polymorphism.md)
