# Module 7.2: External Libraries & pip

**External libraries** (third-party packages) extend Python's functionality beyond the standard library. The **pip** (Python Package Installer) tool downloads and installs packages from PyPI (Python Package Index).

Popular libraries include `numpy` (numerical computing), `pandas` (data analysis), `requests` (HTTP requests), and thousands more. Install with `pip install package_name`.

**Key Technical Properties:**
- **PyPI**: Central repository of packages
- **pip**: Command-line tool for installation
- **Virtual environments**: Isolated package spaces per project
- **requirements.txt**: List dependencies
- **Versioning**: Specify package versions
- **Popular**: Thousands of high-quality packages
- **Community**: Well-maintained by developers

---

## Installing Packages with pip

```bash
# Install a package
pip install requests

# Install specific version
pip install requests==2.28.0

# Install from requirements file
pip install -r requirements.txt

# Upgrade package
pip install --upgrade numpy

# Uninstall package
pip uninstall requests

# List installed packages
pip list

# Show package info
pip show requests
```

---

## Popular Libraries

### Requests (HTTP)

```python
import requests

# Make GET request
response = requests.get('https://api.example.com/data')
print(response.status_code)  # 200
print(response.json())       # Parse JSON response

# Make POST request
data = {"username": "john", "email": "john@example.com"}
response = requests.post('https://api.example.com/users', json=data)

# With headers
headers = {"Authorization": "Bearer token123"}
response = requests.get(url, headers=headers)

# Handle errors
try:
    response = requests.get(url, timeout=5)
    response.raise_for_status()
except requests.exceptions.RequestException as e:
    print(f"Error: {e}")
```

### NumPy (Numerical Computing)

```python
import numpy as np

# Create arrays
arr1 = np.array([1, 2, 3, 4, 5])
arr2 = np.zeros(5)          # [0, 0, 0, 0, 0]
arr3 = np.ones(3)           # [1, 1, 1]
arr4 = np.arange(0, 10, 2)  # [0, 2, 4, 6, 8]

# Array operations
result = arr1 * 2           # Element-wise multiply
mean = np.mean(arr1)        # Average
std = np.std(arr1)          # Standard deviation
max_val = np.max(arr1)      # Maximum

# 2D arrays
matrix = np.array([[1, 2], [3, 4]])
print(matrix.shape)         # (2, 2)

# Practical: Calculate vector norm
vector = np.array([3, 4])
norm = np.linalg.norm(vector)
print(norm)  # 5.0
```

### Pandas (Data Analysis)

```python
import pandas as pd

# Create DataFrame
data = {
    "name": ["Alice", "Bob", "Charlie"],
    "age": [25, 30, 28],
    "salary": [50000, 60000, 55000]
}
df = pd.DataFrame(data)

# Access data
print(df["name"])           # Series
print(df.loc[0])            # First row
print(df.iloc[0, 1])        # Value at row 0, col 1

# Statistics
print(df.describe())        # Summary statistics
print(df.mean())            # Mean of columns

# Filter
high_earners = df[df["salary"] > 55000]

# Group by
grouped = df.groupby("age").mean()

# Save/load
df.to_csv("data.csv")
df2 = pd.read_csv("data.csv")
```

---

## Practical Examples

### Example: Vector Calculations

```python
import numpy as np

def calculate_robot_position(movements):
    """Calculate final robot position"""
    position = np.array([0, 0])
    
    for move in movements:
        direction = np.array(move)
        position += direction
    
    # Calculate distance from origin
    distance = np.linalg.norm(position)
    
    return {
        "position": position.tolist(),
        "distance": float(distance)
    }

# Simulate robot movements
movements = [
    [1, 0],   # Move right
    [0, 1],   # Move up
    [1, 1],   # Move right-up
    [-1, 0]   # Move left
}

result = calculate_robot_position(movements)
print(f"Final position: {result['position']}")
print(f"Distance from origin: {result['distance']:.2f}")
```

---

## Common Libraries by Category

| Category | Package | Use |
|----------|---------|-----|
| **HTTP** | requests | Web API calls |
| **Data** | pandas | Data analysis |
| **Math** | numpy | Numerical computing |
| **Plotting** | matplotlib | Visualizations |
| **Web** | flask | Web applications |
| **Testing** | pytest | Unit testing |
| **ROS2** | rospy | ROS integration |
| **Vision** | opencv-python | Image processing |

---

## What's Next?

Next module: **Creating Your Own Modules** - Package your code!

---

## References

- pip: https://pip.pypa.io/
- PyPI: https://pypi.org/
- Virtual Environments: https://docs.python.org/3/tutorial/venv.html
- Requests: https://requests.readthedocs.io/
- NumPy: https://numpy.org/
- Pandas: https://pandas.pydata.org/

