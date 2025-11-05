# Module 4.2: While Loops
## What is a While Loop?

In simple a while loop keeps running code **as long as a condition is True**. The moment the condition becomes False, the loop stops.

A **while loop** is a control flow statement that **repeatedly executes a block of code as long as a given condition remains True**. Unlike `for` loops, while loops continue until their condition becomes False. This makes them ideal when you don't know how many iterations you need beforehand.

**Key Difference from For Loops:**
- **For loop**: "Repeat this code N times" (known iterations)
- **While loop**: "Keep repeating until condition is false" (unknown iterations)

**Syntax:**
```
while condition:
    code block (executes if condition is True)
    UPDATE the condition (otherwise infinite loop!)
code after loop (executes after condition becomes False)
```

**Why This Matters:** While loops are essential for interactive programs where you don't know when the user will stop, or when processing continues until data runs out.

---

## Simple while loop
```python
count = 0
while count < 5:
    print(count)
    count += 1               # IMPORTANT: Must update the condition!

# Output: 0, 1, 2, 3, 4
```

**Critical Rule**: You MUST change the condition inside the loop, or it runs forever (infinite loop)!


```python
# For loop - we know it's 5 times
for i in range(5):
    print(i)

# While loop - we don't know when user stops
while True:
    choice = input("Play again? (yes/no): ")
    if choice == "no":
        break  # Exit the loop
    # Otherwise loop continues
```

---

## Common While Loop Patterns

### Pattern 1: Counter-Based (Similar to For Loop)

```python
# This is what for loop does internally
count = 0
while count < 5:
    print(f"Iteration {count}")
    count += 1  # DON'T FORGET THIS!

# Better to use for loop for this pattern
for count in range(5):
    print(f"Iteration {count}")
```

### Pattern 2: User Input Loop (Repeat Until Valid)

```python
# Keep asking until user enters valid data
while True:
    age = input("Enter age (0-120): ")
    try:
        age = int(age)
        if 0 <= age <= 120:
            print(f"Valid age: {age}")
            break  # Exit loop when valid
    except ValueError:
        print("That's not a valid number!")

print("Age accepted!")
```

**Note about try-except**: You'll learn about error handling (try-except blocks) in Module 9.1. For now, think of it as "try this, but if it fails, do something else."

### Pattern 3: Sentinel Value (Stop When Condition Met)

```python
# Ask user for numbers, stop when they enter 0
total = 0
while True:
    num = int(input("Enter number (0 to quit): "))
    if num == 0:
        break  # Exit loop when user enters 0
    total += num

print(f"Total: {total}")
```



---

## Practical Examples

### Example 1: Password Validator

```python
correct_password = "python123"
attempts = 0
max_attempts = 3

while attempts < max_attempts:
    password = input("Enter password: ")
    
    if password == correct_password:
        print("Access granted!")
        break  # Exit loop on success
    else:
        attempts += 1
        remaining = max_attempts - attempts
        if remaining > 0:
            print(f"Wrong! {remaining} attempts remaining")

if attempts >= max_attempts:
    print("Account locked!")
```

### Example 2: Bank ATM Simulation

```python
balance = 1000
menu_active = True

while menu_active:
    print("\n" + "=" * 30)
    print("ATM MENU")
    print("=" * 30)
    print(f"Current Balance: ${balance}")
    print("1. Withdraw")
    print("2. Deposit")
    print("3. Check Balance")
    print("4. Exit")
    
    choice = input("Choose (1-4): ")
    
    if choice == "1":
        amount = int(input("Withdraw amount: $"))
        if amount <= balance:
            balance -= amount
            print(f"Withdrew ${amount}")
        else:
            print("Insufficient balance!")
    elif choice == "2":
        amount = int(input("Deposit amount: $"))
        balance += amount
        print(f"Deposited ${amount}")
    elif choice == "3":
        print(f"Balance: ${balance}")
    elif choice == "4":
        print("Thank you for using ATM!")
        menu_active = False
    else:
        print("Invalid choice!")
```

---

## Common Mistakes

### ❌ Mistake 1: Infinite Loop (Forgot to Update Condition)

```python
# INFINITE LOOP! Runs forever
count = 0
while count < 5:
    print("Help! I'm stuck!")
    # Forgot to do count += 1
    # Condition never becomes False

# FIX: Update the condition
count = 0
while count < 5:
    print("This will end")
    count += 1
```

### ❌ Mistake 2: Condition Never True

```python
# Never enters loop
count = 10
while count < 5:
    print("This never runs")
    count += 1

# FIX: Start with condition that's True
count = 0
while count < 5:
    print("This runs!")
    count += 1
```

---

## When to Use While vs For

### Use FOR Loop When:
- You know exactly how many times to loop
- You're iterating through a range of numbers
- You're working with `range()`

```python
for i in range(10):
    print(i)
```

### Use WHILE Loop When:
- You don't know how many iterations needed
- Loop continues based on a condition
- You're getting user input repeatedly
- You're simulating a process that ends when condition is met

```python
while user_wants_to_continue:
    # do something
    user_wants_to_continue = ask_user()
```

---

## Milestone Task: Number Guessing Game

Create an interactive number guessing game!

### Requirements:
- Computer "thinks" of a random number (1-100)
- User tries to guess
- Give hints: "Too high", "Too low", "Correct!"
- Count attempts
- Play again option
- Use while loops for game loop and play-again loop

### Example Output:

```
🎮 Number Guessing Game!
I'm thinking of a number 1-100
Your guess: 50
📈 Too low! Try higher
Your guess: 75
📉 Too high! Try lower
Your guess: 60
📈 Too low! Try higher
Your guess: 65
📉 Too high! Try lower
Your guess: 62
🎉 Correct! You got it in 5 attempts!

Play again? (yes/no): yes

🎮 Number Guessing Game!
I'm thinking of a number 1-100
Your guess: 50
📉 Too high! Try lower
...
```

---

## What's Next?

Next module: **Break, Continue & Pass** - Control how loops behave!

---

## References

- While Loops: https://docs.python.org/3/tutorial/controlflow.html#while-statements
- Loop Control: https://docs.python.org/3/tutorial/controlflow.html#break-and-continue-statements-and-else-clauses-on-loops

