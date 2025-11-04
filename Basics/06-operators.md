# Module 2.1: Operators in Python

Operators are **actions** you perform on data. They're how you do math, compare values, and make decisions.

## Arithmetic Operators: Math!

Use these to do calculations:

```python
# Addition
print(10 + 5)    # 15

# Subtraction
print(10 - 5)    # 5

# Multiplication
print(10 * 5)    # 50

# Division (always gives float)
print(10 / 5)    # 2.0
print(10 / 3)    # 3.333...

# Floor Division (removes decimal)
print(10 // 3)   # 3 (not 3.33)
print(-10 // 3)  # -4

# Modulus (remainder)
print(10 % 3)    # 1 (10 divided by 3 = 3 remainder 1)
print(10 % 2)    # 0 (10 is even)
print(11 % 2)    # 1 (11 is odd)

# Exponent (power)
print(2 ** 3)    # 8 (2 to the power of 3)
print(2 ** 10)   # 1024
print(9 ** 0.5)  # 3.0 (square root)
```

## Relational Operators: True or False?

These compare values and return `True` or `False`:

```python
# Equal to
print(5 == 5)      # True
print(5 == 3)      # False
print("cat" == "cat")  # True

# Not equal to
print(5 != 3)      # True
print(5 != 5)      # False

# Greater than
print(10 > 5)      # True
print(5 > 10)      # False

# Less than
print(5 < 10)      # True
print(10 < 5)      # False

# Greater than or equal
print(5 >= 5)      # True
print(5 >= 3)      # True

# Less than or equal
print(5 <= 5)      # True
print(5 <= 10)     # True
```

## Logical Operators: Combining Conditions

Combine multiple True/False checks:

### AND - All must be True

**AND** Truth Table
|  A  |  B  |  Output  |
|-----|-----|----------|
|False|False|False     |
|False|True |False     |
|True |False|False     |
|True |True |True      |

```python
age = 34
has_license = True

print(age >= 18 and has_license)  # True (both are true)
print(age >= 18 and not has_license)  # False (second is false)
```

In Practical
```python
if age >= 18 and has_license:
    print("You can drive!")
```

### OR - At least one must be True

**OR** Truth Table
|  A  |  B  |  Output  |
|-----|-----|----------|
|False|False|False     |
|False|True |True      |
|True |False|True      |
|True |True |True      |

```python
is_weekend = False
is_holiday = True

print(is_weekend or is_holiday)  # True (holiday is true)
print(is_weekend or False)  # False (both false)
```

In Practical
```python
if is_weekend or is_holiday:
    print("No work today!")
```

### NOT - Reverses True/False

**NOT** Truth Table


| A | ~A |
|---|----|
|False|True|
|True|False|

```python
is_raining = True
print(not is_raining)  # False

is_sunny = False
print(not is_sunny)  # True
```

In Practical
```python
if not is_raining:
    print("Go outside!")
```

## Assignment Operators: Shortcuts

Modify variables more concisely:

```python
x = 10

# Long way
x = x + 5

# Short hand (same result)
x += 5  # x is now 15

# Other shortcuts
x -= 3   # x = x - 3
x *= 2   # x = x * 2
x /= 4   # x = x / 4
x //= 2  # x = x // 2
x %= 3   # x = x % 3
x **= 2  # x = x ** 2
```

## Operator Precedence: What Runs First?

Operators run in a specific order (PEMDAS + more):

```python
# Wrong order gives wrong answer!
print(2 + 3 * 4)    # 14 (NOT 20!)
                    # Because * comes before +
                    # So: 3*4=12, then 2+12=14

# Use parentheses to control order
print((2 + 3) * 4)  # 20 (now + runs first)
```

### Full precedence (highest to lowest):
1. **
2. *, /, //, %
3. +, -
4. ==, !=, <, >, <=, >=
5. and
6. or

## Practical Examples

### Age Checker

```python
age = 25
is_student = True
has_job = True

# Can apply for senior discount?
if age >= 60 or (is_student and not has_job):
    print("You qualify for discount!")

# Voting age?
if age >= 18:
    print("You can vote!")
```

### Grade Calculator

```python
math_score = 85
english_score = 78
science_score = 92

average = (math_score + english_score + science_score) / 3
print(f"Average: {average:.1f}")

if average >= 90:
    print("Grade: A")
elif average >= 80:
    print("Grade: B")
elif average >= 70:
    print("Grade: C")
```

### Even or Odd Checker

```python
number = 7

if number % 2 == 0:
    print(f"{number} is even")
else:
    print(f"{number} is odd")
```

## Common Mistakes

### ❌ Mistake 1: Using = Instead of ==

```python
age = 25
if age = 25:  #  ERROR! This is assignment, not comparison
    print("You're 25")

# Fix:
if age == 25:  #  Correct - two equals for comparison
    print("You're 25")
```

### ❌ Mistake 2: Forgetting Parentheses for Complex Logic

```python
# Confusing without parentheses
if age > 18 and employed or student:  # What gets checked with what?

# Clear with parentheses
if (age > 18 and employed) or student:  # This is what we meant
```

### ❌ Mistake 3: Using 'and' When You Mean 'or'

```python
# Wrong: Both conditions must be true
if has_money and wants_pizza:
    print("Buy pizza")  # Both must be true

# Sometimes you need OR: At least one condition true
if is_weekend or is_holiday:
    print("No work")  # At least one must be true
```

### ❌ Mistake 4: Forgetting Operator Precedence

```python
# Looks like it checks "score > 50 AND score < 100"
# But actually checks "(score > 50) AND (score < 100)" which is WRONG
if score > 50 and score < 100:
    print("In range")  # This is actually correct!

# Real mistake:
if score > 50 or score < 100:  # Almost always true! (most numbers are > 50 OR < 100)
    print("In range")
```

##  Milestone Task: Student Grade Evaluator

Create a program that evaluates student performance using operators!

### Requirements:
- Input: 3 subject scores (math, english, science)
- Calculate average
- Use operators to check:
  - If average >= 90: "Excellent! "
  - If 80-89: "Good! "
  - If 70-79: "OK, keep studying "
  - If < 70: "Need improvement "
- Identify highest and lowest scores using comparison operators
- Check if ALL scores are above 80 (use 'and')
- Check if ANY score is below 60 (use 'or')

### Example Output:

```
╔════════════════════════════════════════╗
║        STUDENT GRADE EVALUATOR         ║
╚════════════════════════════════════════╝

Math Score: 85
English Score: 92
Science Score: 78

╔════════════════════════════════════════╗
║                RESULTS                 ║
╚════════════════════════════════════════╝

Average Score: 85.0
Overall Grade: Good! 

Highest Score: 92 (English)
Lowest Score: 78 (Science)

All scores above 80? No 
Any score below 60? No 

Keep up the great work! 
```

## What's Next?

Next module: **Control Flow - If/Else Statements** - Now you'll USE these operators to make decisions!

---

## References

- Operators in Python: https://docs.python.org/3/tutorial/introduction.html#using-python-as-a-calculator
- Operator Precedence: https://docs.python.org/3/reference/expressions.html#operator-precedence

