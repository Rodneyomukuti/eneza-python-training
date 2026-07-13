# Post-Session Python Quiz — ENEZA Workshop

Use this quiz at the end of the session or as a take-home review.

## Multiple Choice

**1. What will `print(type(42))` output?**

- A) `<class 'float'>`
- B) `<class 'int'>`
- C) `<class 'str'>`
- D) `<class 'bool'>`

**2. Which of the following correctly creates a variable storing a person’s name?**

- A) `1name = "Amina"`
- B) `name = Amina`
- C) `name = "Amina"`
- D) `name == "Amina"`

**3. What does this code print?**

```python
x = 10
y = 3
print(x // y)
```

- A) `3.333`
- B) `3`
- C) `1`
- D) `30`

**4. What is the value of `result` after this code runs?**

```python
result = 5 > 3 and 2 > 4
```

- A) `True`
- B) `False`
- C) `None`
- D) Error

**5. What does `input()` always return?**

- A) An integer
- B) A float
- C) A string
- D) Whatever the user types, automatically converted

## Fill in the Blanks

**6. Complete the function so it returns the square of a number:**

```python
def square(n):
    return ____________
```

**7. Write a line that appends the value `85` to a list called `scores`:**

```python
____________
```

**8. Write an `if` statement that prints `"Adult"` when `age` is 18 or more:**

```python
____________:
    print("Adult")
```

## Short Coding Challenges

**9. BMI calculator:**

Write a program that:
- Asks the user for their weight in kilograms.
- Asks the user for their height in meters.
- Calculates BMI using the formula: `bmi = weight / (height ** 2)`
- Prints the BMI rounded to 2 decimal places.

**10. Grade checker:**

Write a program that:
- Takes a score as input (as an integer).
- Prints `"A"` if score is 90 or above, `"B"` if 80–89, `"C"` if 70–79, `"D"` if 60–69, and `"F"` if below 60.

**11. Loop practice:**

Write a `for` loop that prints all even numbers from 2 to 10 inclusive.

**12. Dictionary lookup:**

Given this dictionary:

```python
patient = {"name": "Ben", "age": 34, "bp": 130}
```

Write a line to print Ben’s blood pressure.

**13. DataFrame exploration:**

You have a Pandas DataFrame `df`. Write two commands to:
- See the first 5 rows.
- Get summary statistics for numeric columns.

**14. Plotting:**

You have a DataFrame `df` with columns `age` and `bmi`. Write a Seaborn command to make a scatter plot of `age` versus `bmi`.


**15. Truthiness:**

What will this code print?

```python
data = []
if data:
    print("Has data")
else:
    print("Empty")
```

**16. List methods:**

You have a list `numbers = [3, 1, 4]`. What method do you use to add the number `5` to the end of the list?

```python
numbers.________(5)
```

**17. Dictionary methods:**

Given the dictionary:

```python
patient = {"name": "Amina", "age": 25}
```

What method safely returns the value for `"diagnosis"` without raising an error if the key is missing, and returns `"Not recorded"` instead?

```python
patient.________("diagnosis", "Not recorded")
```

**18. Looping with `enumerate()`:**

What does this code print?

```python
fruits = ["apple", "banana"]
for index, fruit in enumerate(fruits):
    print(index, fruit)
```

**19. Functions with default arguments:**

What will this function return when called as `greet("Ben")`?

```python
def greet(name, greeting="Hello"):
    return f"{greeting}, {name}!"
```

- A) `"Hello, Ben!"`
- B) `"Hi, Ben!"`
- C) `Error`
- D) `"Ben, Hello!"`

**20. Scope:**

What is the problem with this code?

```python
def show_city():
    city = "Nairobi"

show_city()
print(city)
```

- A) Nothing, it prints `"Nairobi"`.
- B) `city` is a local variable and cannot be accessed outside the function.
- C) The function should return `city`.
- D) `print(city)` should be inside the function.


**21. File handling:**

Which Python keyword is used to automatically close a file after reading or writing?

- A) `open`
- B) `close`
- C) `with`
- D) `read`

**22. Pandas cleaning:**

Which method removes rows with missing values from a DataFrame?

- A) `df.fillna()`
- B) `df.dropna()`
- C) `df.isnull()`
- D) `df.duplicates()`

**23. Pandas filtering:**

How do you select rows where the `Age` column is greater than 30?

```python
____________
```

**24. Visualization:**

What Seaborn function would you use to create a bar plot of `BP` by `Gender`?

```python
sns.________(x="Gender", y="BP", data=df)
```

**25. NumPy:**

What does `np.array([1, 2, 3]) + 10` return?

- A) `[1, 2, 3, 10]`
- B) `[11, 12, 13]`
- C) `Error`
- D) `[10, 20, 30]`

**26. NumPy indexing:**

Given `arr = np.array([10, 20, 30, 40, 50])`, what does `arr[arr > 25]` return?

- A) `[10, 20]`
- B) `[30, 40, 50]`
- C) `[25]`
- D) `Error`
