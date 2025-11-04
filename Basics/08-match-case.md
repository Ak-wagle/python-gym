# Module 3.2: Match-Case Statements (Python 3.10+)

`match-case` is a **cleaner way** to handle multiple conditions. It's like a more organized if-elif-else.

## Why Match-Case?

Old way (if-elif-else) - gets messy with many conditions

```python
if grade == "A":
    print("Excellent!")
elif grade == "B":
    print("Good!")
elif grade == "C":
    print("Average")
elif grade == "D":
    print("Poor")
else:
    print("Unknown")

```
New way (match-case) - cleaner!
```python
match grade:
    case "A":
        print("Excellent!")
    case "B":
        print("Good!")
    case "C":
        print("Average")
    case "D":
        print("Poor")
    case _:
        print("Unknown")
```

## Match-Case Syntax

```python
match variable:
    case value1:
        # Code if variable == value1
    case value2:
        # Code if variable == value2
    case _:
        # Default case (like else)
```

## Examples

### Simple String Matching

```python
day = "Monday"

match day:
    case "Monday":
        print("Monday blues...")
    case "Friday":
        print("TGIF!")
    case "Saturday":
        print("Weekend mode!")
    case "Sunday":
        print("Chill day...")
    case _:
        print("Unknown day")
```

### HTTP Status Codes

```python
status = 404

match status:
    case 200:
        print("Success!")
    case 201:
        print("Created!")
    case 400:
        print("Bad Request")
    case 404:
        print("Not Found")
    case 500:
        print("Server Error")
    case _:
        print("Unknown status code")
```

### Multiple Values in One Case

```python
fruit = "apple"

match fruit:
    case "apple" | "pear" | "banana":
        print("That's a fruit!")
    case "carrot" | "broccoli":
        print("That's a vegetable!")
    case _:
        print("Unknown food")
```

## Match-Case with Conditions

You can add conditions to cases:

```python
score = 85

match score:
    case score if score >= 90:
        print("Grade: A")
    case score if score >= 80:
        print("Grade: B")
    case score if score >= 70:
        print("Grade: C")
    case _:
        print("Grade: F")
```

## Match-Case vs if-elif

| When to Use | Best Choice |
|-----------|----------|
| Checking one variable for many specific values | match-case |
| Complex conditions with and/or logic | if-elif-else |
| Simple 2-3 conditions | if-else |
| Many conditions with patterns | match-case |

## Common Mistakes

### ❌ Mistake 1: Forgetting the Default Case (_)

```python
match choice:
    case "1":
        print("Option 1")
    case "2":
        print("Option 2")
    # What if user enters "3"? Nothing happens!

# Fix: Always include default case
match choice:
    case "1":
        print("Option 1")
    case "2":
        print("Option 2")
    case _:
        print("Invalid choice!")
```

### ❌ Mistake 2: Forgetting Colons

```python
match grade  # ❌ Missing colon
    case "A":
        print("Excellent")

# Fix:
match grade:  # ✅ Colon after variable
    case "A":
        print("Excellent")
```

### ❌ Mistake 3: Wrong Indentation

```python
match color:
case "red":    # ❌ Not indented
    print("Red")

# Fix:
match color:
    case "red":  # ✅ Indented
        print("Red")
```

## Milestone Task: Traffic Light Simulator

Create a traffic light program using match-case!

### Requirements:
- Ask user for light color (red, yellow, green)
- Use match-case to determine action
- Include multiple related values in one case (e.g., "r" and "red")
- Display ASCII art for the light
- Make it interactive (allow multiple lights)

### Example Output:

```
╔════════════════════════════════════════╗
║       TRAFFIC LIGHT SIMULATOR          ║
╚════════════════════════════════════════╝

Enter light color (red/yellow/green): red

        ┌─────────┐
        │  🔴     │   ← Active
        │  ⚪     │
        │  ⚪     │
        └─────────┘

🛑 STOP!
Wait for the light to change.

────────────────────────────────────────

Try another? (yes/no): yes
```

## What's Next?

Next module: **For Loops** - Repeat code multiple times!

---

## References

- Match-Case Syntax: https://docs.python.org/3/tutorial/controlflow.html#match-statements
- PEP 634 - Match: https://peps.python.org/pep-0634/

