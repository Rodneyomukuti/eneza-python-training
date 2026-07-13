# Python Cheat Sheet — ENEZA Python Workshop

A one-page reference for the basics covered in the session.

## 1. Variables and Data Types

```python
name = "Amina"          # str (text)
age = 25                # int (whole number)
height = 1.65           # float (decimal)
is_student = True       # bool (True or False)

# Check the type
type(name)              # <class 'str'>
```

| Type | Example | Description |
|------|---------|-------------|
| `int` | `42`, `-7` | Whole numbers |
| `float` | `3.14`, `-0.5` | Decimal numbers |
| `str` | `"hello"`, `'hello'` | Text |
| `bool` | `True`, `False` | Logical values |

## 2. Basic Output and Input

```python
print("Hello, World!")

name = input("Enter your name: ")   # always returns a string
age = int(input("Enter your age: "))  # convert to int
```

## 3. Comments

```python
# This is a single-line comment

"""
This is a multi-line comment
or a docstring.
"""
```

## 4. Strings

```python
greeting = "Hello"
name = "Amina"
message = greeting + " " + name       # Hello Amina
message = f"{greeting}, {name}!"        # Hello, Amina!

name.upper()      # "AMINA"
name.lower()      # "amina"
name.strip()      # remove extra spaces
name.replace("A", "E")  # "Emina"
```

## 5. Numbers and Arithmetic

```python
a = 10
b = 3

a + b     # 13
a - b     # 7
a * b     # 30
a / b     # 3.333... (always float)
a // b    # 3 (floor division)
a % b     # 1 (remainder)
a ** b    # 1000 (power)
```

## 6. Comparison and Logical Operators

```python
a == b    # equal
a != b    # not equal
a > b     # greater than
a < b     # less than
a >= b    # greater or equal
a <= b    # less or equal

x > 0 and x < 10   # both must be True
x < 0 or x > 10    # at least one must be True
not (x == 0)       # opposite
```

## 7. Conditionals

```python
score = 85

if score >= 90:
    grade = "A"
elif score >= 80:
    grade = "B"
elif score >= 70:
    grade = "C"
elif score >= 60:
    grade = "D"
else:
    grade = "F"
```

### Truthiness

| Value | Treated as |
|-------|-----------|
| `0`, `0.0`, `""`, `[]`, `{}`, `None` | `False` |
| Non-zero numbers, non-empty collections | `True` |

```python
name = "Amina"
if name:
    print("Name provided")
```

### Nested Conditions

```python
if has_fever:
    if cough_days >= 3:
        print("See a doctor")
    else:
        print("Rest at home")
```

## 8. Data Structures

### Lists (ordered, mutable)

```python
fruits = ["apple", "banana", "cherry"]
fruits[0]               # "apple"
fruits[-1]              # last item: "cherry"
fruits[0:2]             # slice: ["apple", "banana"]
fruits.append("date")   # add at end
fruits.insert(1, "kiwi") # insert at index
fruits.remove("banana") # remove first match
fruits.pop()            # remove and return last item
fruits.sort()           # sort in place
fruits.reverse()        # reverse in place
len(fruits)             # number of items
fruits.index("apple")   # find position
fruits.count("apple")   # count occurrences
```

### Dictionaries (key-value pairs)

```python
patient = {
    "name": "Amina",
    "age": 25,
    "bp": 120
}
patient["age"]              # 25
patient["bmi"] = 22.5       # add new key
patient.get("diagnosis", "Not recorded")  # safe lookup
patient.keys()              # all keys
patient.values()            # all values
patient.items()             # key-value pairs
patient.update({"bp": 118, "bmi": 22.5})  # update multiple
del patient["bp"]           # remove key
```

### Tuples (ordered, immutable)

```python
coordinates = (10, 20)
x, y = coordinates          # tuple unpacking
```

### Sets (unique items)

```python
tags = {"python", "data", "python"}  # {"data", "python"}

# Set operations
a = {1, 2, 3}
b = {3, 4, 5}
a | b   # union: {1, 2, 3, 4, 5}
a & b   # intersection: {3}
a - b   # difference: {1, 2}
```

### Which Structure to Use?

| Use | When you need... |
|-----|------------------|
| **List** | Ordered collection that may change |
| **Tuple** | Fixed data that should not change |
| **Dictionary** | Labeled data with key-value pairs |
| **Set** | Unique items only, order does not matter |

## 9. Loops

```python
# For loop with range
for i in range(5):
    print(i)          # 0, 1, 2, 3, 4

for i in range(2, 11, 2):
    print(i)          # 2, 4, 6, 8, 10

# Loop through a list
for fruit in fruits:
    print(fruit)

# Loop through a dictionary
for key, value in patient.items():
    print(f"{key}: {value}")

# enumerate: index and value
for index, fruit in enumerate(fruits):
    print(f"{index}: {fruit}")

# zip: two lists together
names = ["Amina", "Ben"]
ages = [25, 34]
for name, age in zip(names, ages):
    print(f"{name} is {age}")

# While loop
count = 0
while count < 5:
    print(count)
    count += 1

# List comprehension (shortcut)
squares = [n ** 2 for n in range(1, 6)]  # [1, 4, 9, 16, 25]
```

## 10. Functions

```python
def greet(name):
    """Return a greeting message."""
    return f"Hello, {name}!"

message = greet("Amina")
print(message)
```

### Default Arguments

```python
def greet(name, greeting="Hello"):
    return f"{greeting}, {name}!"

greet("Amina")                  # "Hello, Amina!"
greet("Ben", "Good morning")    # "Good morning, Ben!"
```

### Local vs Global Scope

```python
country = "Kenya"  # global

def show_city():
    city = "Nairobi"  # local
    print(f"{city} is in {country}")

show_city()
# print(city)  # Error! city is local
```

### Multiple Return Values

```python
def analyze(a, b):
    return a + b, a * b

s, p = analyze(4, 5)
```

## 11. Importing Libraries

```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
import numpy as np
```

## 12. Quick Pandas and Seaborn

```python
# Create a DataFrame
data = {
    "name": ["Amina", "Ben", "Carla"],
    "age": [25, 30, 28],
    "bmi": [22.5, 24.1, 21.8]
}
df = pd.DataFrame(data)

# Explore
df.head()           # first 5 rows
df.tail()           # last 5 rows
df.info()           # structure and types
df.describe()       # summary statistics

# Select data
df["age"]                       # one column
df[["name", "age"]]             # multiple columns
df[df["age"] > 26]              # filter rows

# Plot
sns.scatterplot(x="age", y="bmi", data=df)
plt.show()
```

## 13. File Handling

```python
# Write a text file
with open('file.txt', 'w') as f:
    f.write('Hello\n')

# Read a text file
with open('file.txt', 'r') as f:
    content = f.read()

# Read CSV with Pandas
import pandas as pd
df = pd.read_csv('data.csv')

# Read and write JSON
import json
with open('data.json', 'w') as f:
    json.dump({'name': 'Amina'}, f)

with open('data.json', 'r') as f:
    data = json.load(f)
```

## 14. Pandas Data Cleaning

```python
# Check missing values
df.isnull().sum()

# Drop missing values
df.dropna()

# Fill missing values
df['Age'].fillna(df['Age'].mean())

# Remove duplicates
df.drop_duplicates()

# Rename columns
df.rename(columns={'OldName': 'NewName'})

# Filter and sort
df[df['Age'] > 30]
df.sort_values('Age', ascending=False)
```

## 15. Data Visualization (Seaborn/Matplotlib)

```python
import seaborn as sns
import matplotlib.pyplot as plt

# Bar plot
sns.barplot(x='Category', y='Value', data=df)

# Histogram
sns.histplot(df['Value'], kde=True)

# Box plot
sns.boxplot(x='Group', y='Value', data=df)

# Scatter plot
sns.scatterplot(x='Age', y='BMI', hue='Gender', data=df)

# Heatmap of correlations
sns.heatmap(df.corr(), annot=True)

plt.show()
```

## 16. NumPy Basics

```python
import numpy as np

# Create arrays
arr = np.array([1, 2, 3, 4, 5])
zeros = np.zeros(5)
ones = np.ones((2, 3))
sequence = np.arange(0, 10, 2)

# Operations
arr + 10
arr * 2
arr ** 2
arr > 3

# Indexing
arr[0]
arr[-1]
arr[1:4]
arr[arr > 3]

# Statistics
np.mean(arr)
np.median(arr)
np.std(arr)
np.min(arr)
np.max(arr)
```

## 17. Common Errors

| Error | Likely Cause |
|-------|--------------|
| `NameError` | Variable not defined |
| `SyntaxError` | Typo or missing colon/parenthesis |
| `TypeError` | Wrong type used (e.g., adding string + int) |
| `IndexError` | List index out of range |
| `KeyError` | Dictionary key does not exist |
| `ModuleNotFoundError` | Library not installed |

---

**Keep this sheet handy while coding!**
