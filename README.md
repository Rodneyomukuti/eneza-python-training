# Eneza_Data_Science_Python_tutorial

Welcome! This repository contains the teaching materials, notebooks, and reference guides for the **Python Basics for Data Science** session (ENEZA Training Program Curriculum, Section 6).

It is designed for instructors and learners who want a complete, hands-on introduction to Python for data science, from fundamentals to Pandas, NumPy, and visualization.

## Repository Contents

| File | Purpose |
|------|----------|
| `Python_Zero_to_Hero_Workshop.ipynb` | Main interactive notebook for teaching and hands-on practice |
| `python_cheat_sheet.md` | One-page reference for participants |
| `post_session_quiz.md` | Review quiz |
| `environment.yml` | Conda environment specification (installs Python, Jupyter, Pandas, Seaborn, etc.) |
| `environment_miniforge.yml` | Same environment, optimized for Miniforge (conda-forge only) |
| `python_tutorial_notebook.ipynb` | Original reference notebook (kept as archive) |

## Quick Start

### 1. Clone this repository

```bash
git clone https://github.com/Rodneyomukuti/eneza-python-training.git
cd eneza-python-training
```

### 2. Create the environment

**If you use Anaconda or Miniconda:**

```bash
conda env create -f environment.yml
conda activate eneza-python
```

**If you use Miniforge:**

Miniforge works the same way as conda, but it uses the `conda-forge` channel by default. You can use either file, but `environment_miniforge.yml` is optimized for Miniforge.

```bash
conda env create -f environment_miniforge.yml
conda activate eneza-python
```

> **Note:** If `conda` is not found on WSL, make sure Miniforge was initialized for your shell. You may need to run `source ~/.bashrc` or restart your terminal after installing Miniforge.

### 3. Start Jupyter

**Linux:**
```bash
jupyter notebook
```

**WSL on Windows:**
```bash
jupyter notebook --no-browser
```
Then copy the URL (with token) into Chrome/Edge on Windows.

### 4. Open the notebook

In Jupyter, open `Python_Zero_to_Hero_Workshop.ipynb` and follow the instructions.

## Workshop Flow

1. Setup and orientation
2. Hello Python, variables, and data types
3. Strings and f-strings
4. Numbers, user input, and BMI calculator
5. `if/elif/else` decisions, truthiness, and nested conditions
6. Lists, dictionaries, tuples, sets — including common methods and when to use each
7. `for` and `while` loops, `enumerate()`, `zip()`, and list comprehensions
8. Functions, parameters, defaults, scope, and docstrings
9. Pandas + Seaborn mini-project
10. **File handling**: text files, CSV, JSON
11. **Data cleaning with Pandas**: missing values, duplicates, filtering, sorting
12. **Data visualization**: line, bar, histogram, box, scatter, and heatmap plots
13. **Numerical computing with NumPy**: arrays, operations, indexing, statistics
14. Wrap-up and quiz

## Notes

- The main notebook was designed for a **mixed-experience audience**.
- WSL-specific tips are included for Windows users.
- The session covers the full **Python fundamentals-to-data-science pipeline** taught in the curriculum.
- More advanced topics (machine learning, interactive dashboards, databases) are left for follow-up sessions.

## Recommended Session Length

**Two full days** is ideal for this expanded coverage:

- Day 1: Parts 1–9 (Python fundamentals + first Pandas/Seaborn project)
- Day 2: Parts 10–13 (file handling, data cleaning, visualization, NumPy) + wrap-up/quiz

If you must fit everything into one day, focus on the essentials and treat the later parts as demonstrations.

---

Good luck!
