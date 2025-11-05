# Module 7.3: Creating Your Own Modules

A **module** is a Python file (`.py`) containing functions, classes, and variables that you can reuse in other programs.

**Packages** are directories containing modules and a special `__init__.py` file. Creating modules promotes code organization, reusability, and maintainability.

```python
import my_module

# or

from my_module import my_function
```

**Key Technical Properties:**
- **Module**: Single `.py` file
- **Package**: Directory with `__init__.py`
- **Import**: Load module with `import`
- **Namespace**: Module functions accessed via `module.function()`
- **Reusable**: Use code across projects
- **Organized**: Group related functionality
- **Testable**: Test modules independently

**Note**: It is highly recommended to learn the Object-Oriented Programming (OOP) section before diving deeper into creating packages.
Understanding classes and objects will help you organize modules more effectively, especially in larger applications.

---
rest : TODO