# Data Visualization with Python — A Follow-Along Guide

This guide walks you through Parts 12 and 13 of the workshop notebook at your own pace: data visualization first, then NumPy, the engine underneath it all. Everything here runs in `Python_Zero_to_Hero_Workshop.ipynb`, but the code is also included in full below, so you can copy any block into a fresh notebook and experiment.

Why bother with plots at all? Because nobody in a hospital board meeting wants to see your DataFrame, and nobody at a conference wants your CSV. They want the picture. A good plot is worth a thousand rows — and unlike the thousand rows, people will actually look at it.

## 1. The toolbox: what import actually means

Python itself is deliberately small. Out of the box it can print, do arithmetic, and handle lists — that is about it. The real power lives in libraries: toolboxes of code that other people wrote, tested, and gave away for free.

```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
```

`import` means "go to the shelf, fetch that toolbox, and put it on my bench for this session." When you installed packages with conda, that put the toolbox in the building. `import` brings it to your desk. Install once, import in every notebook.

**Why the short names?** `import pandas as pd` means "fetch pandas, and around here we will call it pd." It is a nickname — an alias. You will type it hundreds of times, and nobody wants to type `pandas.DataFrame` all day.

Here is the important part: `pd`, `plt`, and `sns` are not rules built into Python. They are culture. The whole world uses the same nicknames, so anyone can read anyone's code — like calling a matatu a "mat". Nobody legislated it; everybody understands it. Python will happily accept `import pandas as banana`, and `banana.DataFrame()` will work fine. Your code will run. Your collaborators will never trust you again. Use `pd`.

Two small curiosities in the imports above: we import only the `pyplot` drawer of the big matplotlib toolbox, because that drawer holds the plotting commands. And seaborn's alias `sns` comes from Samuel Norman Seaborn, a character in The West Wing. Programmers are like that.

## 2. Reading Python: dots, parentheses, and brackets

Almost every line in this guide has a dot in it, and the dot always means the same thing: WHO, dot, WHAT. The word before the dot is who owns the tool. The word after is the tool.

- `plt.plot(...)` reads as "matplotlib, draw this."
- `viz_df.head()` reads as "table, show me your first rows."
- `message.upper()` reads as "message, uppercase yourself."

Two more symbols complete the decoder ring:

- Parentheses `()` mean "do it now" — whatever is inside them are the instructions.
- Square brackets `[]` mean "grab this piece" — `viz_df['Age']` is "from the table, grab the Age column."

Doing versus grabbing. That is the whole grammar. Once you can read the dots, no line of Python looks like magic — it reads like a short sentence: somebody, does something, with these details.

## 3. Which tool, and how do you choose?

We use two plotting tools together, and it helps to know who does what.

**Matplotlib** is the grandfather of Python plotting — over twenty years old, controls every pixel, and gives you exactly what you ask for, including the ugly version. It will never stop you from making a terrible chart. It is not a mentor; it is a printer.

**Seaborn** is built on top of matplotlib — matplotlib after someone taught it statistics and fashion sense. One line of seaborn often does what fifteen lines of matplotlib would.

The rule of thumb:

- Quick glance at your own data: pandas has a shortcut, `df.plot()`.
- A statistical figure for a meeting or a paper: seaborn.
- Fine-tuning anything — titles, sizes, annotations: matplotlib commands.

Because seaborn draws on matplotlib's canvas, they mix freely. That is why `plt.title()` works right after `sns.barplot()` — seaborn paints, matplotlib frames. You will see the combination in every example below.

Are there alternatives? Plenty. Plotly makes interactive plots with hover and zoom, and powers dashboards. Bokeh and Altair are similar. If you come from R and miss ggplot2, the plotnine library is literally the ggplot grammar in Python. Learn matplotlib plus seaborn first — they are the standard for static and publication figures, and every alternative borrows their ideas.

## 4. The dataset

```python
data = {
    'Patient': ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H'],
    'Age': [25, 34, 28, 45, 31, 52, 29, 38],
    'BMI': [22.5, 24.1, 21.8, 27.3, 23.5, 29.0, 22.0, 25.5],
    'BP': [118, 135, 122, 140, 128, 145, 120, 132],
    'Gender': ['F', 'M', 'F', 'M', 'F', 'M', 'F', 'M']
}

viz_df = pd.DataFrame(data)
viz_df
```

Line by line:

- `data = {...}` is a plain Python dictionary. Read it as a form: each key becomes a column name, each list becomes that column's values. Eight patients, five properties.
- `pd.DataFrame(data)` — decode the dots: "pandas, use your DataFrame tool, on our dictionary, now." Out comes a proper table. We label the box `viz_df`: a DataFrame for visualization. Naming things clearly is a kindness to your future self.
- `viz_df` alone on the last line is a Jupyter trick: a bare variable at the end of a cell gets displayed, no `print()` needed.

The dataset is small on purpose. You can see every row, so when a plot appears you can check it against the raw numbers with your own eyes. That habit — verifying the plot against the data — will save your career someday.

Before you plot anything, try this: just from eyeballing the eight rows, which patient do you predict stands out? Keep your answer in mind. The plots should agree with you — and if they do not, either your reading or the plot is wrong, and finding out which is the whole game.

## 5. The five beats of every plot

Every matplotlib plot follows the same rhythm. Learn this one rhythm and you can play every song.

```python
plt.figure(figsize=(8, 4))
plt.plot(viz_df['Patient'], viz_df['Age'], marker='o')
plt.title('Age by Patient')
plt.xlabel('Patient')
plt.ylabel('Age')
plt.show()
```

- `plt.figure(figsize=(8, 4))` — beat one, the canvas. Every painting starts with a blank canvas of a chosen size: 8 wide, 4 tall, in inches, because matplotlib is American. Do this first, before any paint. Note the parentheses inside parentheses: `figsize` receives one thing, a (width, height) pair.
- `plt.plot(viz_df['Patient'], viz_df['Age'], marker='o')` — beat two, the paint. Square brackets grab the Patient column for the x-axis and the Age column for the y-axis. X first, y second, always, like coordinates on a map. `marker='o'` puts a visible dot at every data point — without it you get only the line, and nobody can see where the actual measurements are.
- `plt.title('Age by Patient')` — beat three, the headline. A plot without a title is a newspaper article without one: technically complete, practically useless.
- `plt.xlabel(...)` and `plt.ylabel(...)` — beat four, the axes introduce themselves. Never make your reader guess what the numbers mean.
- `plt.show()` — beat five, the unveiling. Everything before this was backstage.

Now the uncomfortable question: is a line plot the right choice here? Look again. A line implies that patients A through H are connected in a sequence — but they are unrelated people. Python drew exactly what we asked for, not what we meant. Choosing the right chart is your job, not the computer's. We started with the wrong chart on purpose, so you never trust a default again.

## 6. Bar plot: comparing groups

```python
plt.figure(figsize=(6, 4))
sns.barplot(x='Gender', y='BMI', data=viz_df)
plt.title('Average BMI by Gender')
plt.show()
```

- The canvas is smaller this time — only two categories to show.
- `sns.barplot(x='Gender', y='BMI', data=viz_df)` uses three named instructions: x equals Gender, y equals BMI, data equals our table. These are keyword arguments — labelled slots, like labelled vials. Because each one carries its own name, the order does not matter and nothing gets mixed up.
- The quiet magic: seaborn takes the Gender column, groups the patients, computes the average BMI per group, and draws the bars. One line replaced a group-by, a mean, and a bar call.
- Notice `plt.title()` decorating an sns plot — proof that they share one canvas.

When you run it, look at the small black whisker on each bar. That is a confidence interval — an error bar, included free of charge. And a caution: with four patients per group, how much would you trust this comparison? If you presented an n of 4 at a conference, the statisticians in the audience would need medical attention themselves. Small samples make pretty bars and weak conclusions.

## 7. Histogram: the shape of one variable

```python
plt.figure(figsize=(8, 4))
sns.histplot(viz_df['BMI'], bins=5, kde=True)
plt.title('Distribution of BMI')
plt.xlabel('BMI')
plt.show()
```

The histogram asks a different kind of question — not "which patient" but "what is the shape of this variable." Where do most values cluster? Any stragglers?

- We hand it just one column: grab BMI.
- `bins=5` sorts the values into five buckets and counts each bucket.
- `kde=True` — capital T, a boolean — adds the smooth curve over the bars: a kernel density estimate, the same story with the corners rounded off.

Try changing `bins` to 2, then to 50, and rerun. Too few bins and everything blurs into one lump; too many and you are looking at noise. It is like choosing shelves for a pharmacy: two shelves and everything is just "drugs", fifty and you have a shelf labelled "paracetamol, but Tuesday's batch". Bins are a choice, and choices should be deliberate.

## 8. Box plot: the statistician's x-ray

```python
plt.figure(figsize=(8, 4))
sns.boxplot(x='Gender', y='BP', data=viz_df)
plt.title('Blood Pressure by Gender')
plt.show()
```

Read the seaborn line yourself before continuing — you can, because it is the same labelled-slots pattern as the bar plot. You did not learn one chart earlier; you learned the pattern for all of seaborn. Swap `boxplot` for `violinplot` someday and the line still works.

Anatomy of the box: the line in the middle is the median — the typical patient. The box holds the middle 50 percent. The whiskers show the usual range, and any lonely dot beyond them is an outlier — the patient the ward remembers.

One plot gives you five summary statistics per group at a glance. When you compare BP across wards, shifts, or treatment arms, this is the chart you want. And when you read one, ask about spread as well as center: two groups can share a median while one of them swings far wider — and in medicine, the swing is often the story.

## 9. Scatter plot: four dimensions on a flat screen

```python
plt.figure(figsize=(8, 5))
sns.scatterplot(x='Age', y='BMI', hue='BP', size='BP', data=viz_df)
plt.title('Age vs BMI by Blood Pressure')
plt.show()
```

The scatter plot is the relationship chart. Every dot is one patient.

- Two slots you already know: x is Age, y is BMI.
- Two new slots: `hue='BP'` colors each dot by blood pressure, and `size='BP'` scales each dot by it too.

Count the channels: horizontal position, vertical position, color, size. Four variables in one flat image — smuggling extra dimensions past a two-dimensional screen.

Run it and look for the pattern: older patients trend toward higher BMI, and the big dark dots — high BP — gather in the upper right. Remember the patient you predicted from the raw table? Check the top right corner. The data keeps its promises.

## 10. Correlation heatmap: the relationship hunter

```python
plt.figure(figsize=(6, 4))
sns.heatmap(viz_df[['Age', 'BMI', 'BP']].corr(), annot=True, cmap='coolwarm')
plt.title('Correlation Matrix')
plt.show()
```

This line has the most grammar in the whole guide, so go slowly — it is a beautiful sentence.

- `viz_df[['Age', 'BMI', 'BP']]` — look closely: double square brackets. The outer pair is our old friend "grab". The inner pair is just a list. So this reads "grab this list of columns." One bracket grabs a column; two brackets grab a shopping list of columns. We keep only the numeric three, because you cannot correlate "Male".
- `.corr()` — this dot hangs directly off the result of the grab. Python reads left to right like a sentence: take the table, keep three columns, then compute every pairwise correlation. This chaining works because each step hands its result to the next. It is how fluent Python gets written — short sentences, not paragraphs.
- `sns.heatmap(..., annot=True, cmap='coolwarm')` — the correlation table goes into the heatmap. `annot=True` writes the actual numbers inside each square; a heatmap without annotations is a mood, with them it is evidence. `cmap='coolwarm'` is the color map: warm red for positive, cool blue for negative. Other colormaps exist, including one called `viridis` and one called `inferno`, for when your results feel that way.

How to read it: +1 means two variables move together perfectly, -1 means perfectly opposite, 0 means no linear relationship. The diagonal is always exactly 1, because everything correlates perfectly with itself — the least surprising result in statistics.

And the sentence every data person must be able to recite in their sleep: correlation is not causation. Age and BMI moving together does not mean birthdays cause weight gain. Ice cream sales correlate with drowning incidents, and ice cream does not drown people — summer causes both. Whenever two variables move together, always ask what the "summer" might be.

## 11. Making your plots look professional

How do you make a plot clean, smooth, and ready for a supervisor or a journal? Six habits, and none of them is talent.

1. Set the canvas first: `plt.figure(figsize=(8, 4))` before you draw, not after.
2. Every plot gets a title and axis labels, every time. An unlabeled plot is a rumor. A plot with no labels is like a prescription with no dosage — impressive handwriting, clinically useless.
3. One plot, one message. If you catch yourself saying "and also notice...", that is a second plot.
4. Run `plt.tight_layout()` before showing, so labels never get chopped off at the edges.
5. Instant beauty: run `sns.set_theme()` once at the top of your notebook and every plot after it gets restyled. Try it, then rerun the scatter plot — the before-and-after speaks for itself.
6. When you export: `plt.savefig('figure.png', dpi=300)` — and call it before `plt.show()`, or you will save a beautiful blank image. Everyone does that exactly once.

A bonus habit: use `palette='colorblind'` in seaborn plots. Roughly one in twelve men cannot tell your red from your green, and some of them will be reviewing your paper.

## 12. Practice

Using `viz_df` from section 4:

1. Create a histogram of the `BP` values. Choose your bins deliberately.
2. Create a scatter plot of `BMI` versus `BP`. Give it a proper title and labels.
3. Interpret your scatter plot in one written sentence. In real work, the interpretation is the deliverable — the code is just how you got there.

Both tasks are copy-and-adapt jobs from sections 7 and 9. Change more than the variable names: retitle, relabel, make the plot yours.

## 13. NumPy: the engine under the hood

One more toolbox — the last one, and the deepest. Under Pandas, under Seaborn, under half of scientific Python, sits NumPy. It does one thing supremely well: arrays of numbers, fast. If Pandas is the ward, NumPy is the plumbing and electricity. This corresponds to Part 13 of the workshop notebook.

```python
import numpy as np

a = np.array([1, 2, 3, 4, 5])
b = np.zeros(5)
c = np.ones((2, 3))
d = np.arange(0, 10, 2)

print('a:', a)
print('b:', b)
print('c:', c)
print('d:', d)
```

Four ways to make an array:

- `np.array([1, 2, 3, 4, 5])` — decode the dots: "numpy, use your array tool, on this ordinary list." Out comes an array: looks like a list, behaves like a rocket.
- `np.zeros(5)` — five zeros. Why would anyone want zeros? Placeholders. You build the empty container first and fill it with results later, like labelling tubes before the samples arrive.
- `np.ones((2, 3))` — ones, but look: double parentheses again. We hand it one instruction, the pair (2, 3) — two rows, three columns. Your first two-dimensional array; a tiny spreadsheet of ones.
- `np.arange(0, 10, 2)` — start at 0, stop before 10, step by 2. Like the `range()` you met with loops, but it makes an array. And as always in Python, the stop value is excluded: 0, 2, 4, 6, 8 — no 10.

## 14. Vectorized operations: no loop needed

Before running this, make a prediction: what does `a + 10` do — an error, or something else?

```python
a = np.array([1, 2, 3, 4, 5])

print('a + 10:', a + 10)
print('a * 2:', a * 2)
print('a squared:', a ** 2)
print('a > 3:', a > 3)
```

Every element, one operation, no loop. This is called vectorization, and it is NumPy's party trick: most of the numeric loops you would otherwise write simply become unnecessary.

Look closely at the last line. `a > 3` did not give one answer — it asked all five elements "are you greater than 3?" and returned an array of True and False. Hold that thought; it pays off in the next section.

Arrays also work element by element with each other — first with first, second with second:

```python
b = np.array([10, 20, 30, 40, 50])
print('a + b:', a + b)
print('a * b:', a * b)
```

## 15. Grabbing pieces: indexing, slicing, and the boolean mask

```python
arr = np.array([10, 20, 30, 40, 50, 60])

print('First element:', arr[0])
print('Last element:', arr[-1])
print('Slice [1:4]:', arr[1:4])
print('Elements > 30:', arr[arr > 30])
```

- Square brackets mean "grab", as ever. Position 0 is the first element — Python counts from zero. Minus 1 counts from the end.
- The slice `1:4` grabs positions 1, 2, and 3 — stop excluded, same rule as `arange`, same rule as everywhere.
- The last line is the payoff from the previous section. Read it inside out: `arr > 30` asks every element "are you over 30?" and gets back True/False. Feed that back into the grab brackets, and only the Trues survive. One readable line: "give me the elements over 30."

This is called a boolean mask, and it is the same filter whatever your field: all patients with BP above 140, all sequencing reads with quality above 30, all observations beyond the threshold. One pattern, every discipline.

## 16. Statistics, and why the median earns its salary

Before running this, look at the numbers: 12, 15, 18, 21, 24 — and then 100. Predict: will the mean be bigger or smaller than the median?

```python
nums = np.array([12, 15, 18, 21, 24, 100])

print('Mean:', np.mean(nums))
print('Median:', np.median(nums))
print('Standard deviation:', np.std(nums))
print('Min:', np.min(nums))
print('Max:', np.max(nums))
```

The mean comes out around 31.7 — higher than five of the six actual values. The median sits at 19.5 and barely noticed the intruder. One outlier dragged the mean far from the typical value, the way the average salary in a room jumps the moment a billionaire walks in: technically correct, describes nobody.

This is why skewed data — income, hospital length-of-stay, gene expression — is usually reported with medians. Whenever you report a mean, ask yourself who the billionaire in your data might be.

## 17. The race: why everyone builds on NumPy

One final experiment. A million numbers, multiply each by 2. Contestant one: a Python list with a loop. Contestant two: a NumPy array. Before you run it, place a bet — how many times faster is NumPy?

```python
import time

py_list = list(range(1000000))
np_arr = np.arange(1000000)

start = time.time()
result = [x * 2 for x in py_list]
print('Python list time:', time.time() - start)

start = time.time()
result = np_arr * 2
print('NumPy array time:', time.time() - start)
```

On most machines NumPy wins by a factor of ten to a hundred. The Python list is a matatu making every stop; NumPy is the express — same route, no stops.

This is not a party trick. On a genome with three billion bases, or a national health dataset, this is the difference between a coffee break and come-back-tomorrow. It is also why Pandas, Seaborn, scikit-learn, and most of scientific Python are built on NumPy underneath.

## 18. Practice

1. Create a NumPy array of the numbers 1 to 10 (hint: `np.arange` — mind the excluded stop).
2. Multiply every element by 3.
3. Keep only the elements greater than 15, using a boolean mask.
4. Compute the mean of what remains.

You are chaining the three skills from this half of the guide: vectorized math, a boolean mask, and a statistic. If your final answer is 24, everything worked.

## 19. Where to go next

- More Seaborn: facet grids, regression plots, pair plots — [seaborn.pydata.org](https://seaborn.pydata.org/)
- Interactive plots and dashboards: Plotly and Streamlit
- For R converts: plotnine, the ggplot grammar in Python
- NumPy in depth: [numpy.org/doc](https://numpy.org/doc/stable/)
- The gallery method: browse the [matplotlib gallery](https://matplotlib.org/stable/gallery/) or [seaborn gallery](https://seaborn.pydata.org/examples/), find a plot you like, copy its code, and bend it to your data. This is how everyone actually learns visualization.

You now have the decoder ring: owner, dot, action. Grab with brackets, do with parentheses. You can read Python. Happy plotting.
