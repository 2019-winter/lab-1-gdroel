---
jupyter:
  jupytext:
    formats: ipynb,md
    text_representation:
      extension: .md
      format_name: markdown
      format_version: '1.1'
      jupytext_version: 1.2.4
  kernelspec:
    display_name: Python 3
    language: python
    name: python3
---

# Name
**Gabe Roeloffs**


**Instructions:** This is an individual assignment, but you may discuss your code with your neighbors.


# Python and NumPy

While other IDEs exist for Python development and for data science related activities, one of the most popular environments is Jupyter Notebooks.

This lab is not intended to teach you everything you will use in this course. Instead, it is designed to give you exposure to some critical components from NumPy that we will rely upon routinely.

## Exercise 0
Please read and reference the following as your progress through this course. 

* [What is the Jupyter Notebook?](https://nbviewer.jupyter.org/github/jupyter/notebook/blob/master/docs/source/examples/Notebook/What%20is%20the%20Jupyter%20Notebook.ipynb#)
* [Notebook Tutorial](https://www.datacamp.com/community/tutorials/tutorial-jupyter-notebook)
* [Notebook Basics](https://nbviewer.jupyter.org/github/jupyter/notebook/blob/master/docs/source/examples/Notebook/Notebook%20Basics.ipynb)

**In the space provided below, what are three things that still remain unclear or need further explanation?**


**YOUR ANSWER HERE**


## Exercises 1-7
For the following exercises please read the Python appendix in the Marsland textbook and answer problems A.1-A.7 in the space provided below.


## Exercise 1

```python
# Make an array a of size 6 × 4 where every element is a 2.
import numpy as np

a = np.full((6,4), 2)
print(a)
```

## Exercise 2

```python
# Make an array b of size 6 × 4 that has 3 on the leading diagonal and 1 everywhere else.
b = np.full((6,4), 1)
np.fill_diagonal(b, 3)
print(b)

```

## Exercise 3

```python
# Can you multiply these two matrices together? Why does a * b work, but not dot(a,b)?
print(a * b)

# dot(a, b) does not work because the number of rows in a is not equivalent to the number
# of columns in b
```

## Exercise 4

```python
# Compute dot(a.transpose(),b) and dot(a,b.transpose()). Why are the results different shapes?

print(np.dot(a.transpose(), b))
print(np.dot(a, b.transpose()))

# Because in the first case, each row of a is multiplied against each column of b.
# Since there are four rows in a because it is transposed, it is multiplied against four columns,
# yielding a 4x4 matrix. The same is true for the second case, except with six rows multiplied against six columns.
```

## Exercise 5

```python
# Write a function that prints some output on the screen and make sure you can run it in the programming environment that you are using.
def hello_there():
    print("hello there")
hello_there()
```

## Exercise 6

```python
# Now write one that makes some random arrays and prints out their sums, the mean value, etc.

def test_func():
    rand1 = np.random.rand(5,5)
    rand2 = np.random.rand(5,5)

    print("sum")
    print(np.sum(rand1))
    print("mean value")
    print(np.mean(rand1))
    
test_func()


```

## Exercise 7

```python
# Write a function that consists of a set of loops that run through an array and count the number of ones in it. Do the same thing using the where() function (use info(where) to find out how to use it).
def num_ones_naive(input_array):
    count = 0
    for i in range(0, input_array.shape[0]):
        for j in range(0, input_array.shape[1]):
            if input_array[i][j] == 1:
                count += 1
                
    return count

def num_ones_fast(input_array):
    return len(np.where(input_array==1)[0])

a = np.full((4,4), 1)
print(num_ones_naive(a))
print(num_ones_fast(a))

```

## Excercises 8-???
While the Marsland book avoids using another popular package called Pandas, we will use it at times throughout this course. Please read and study [10 minutes to Pandas](https://pandas.pydata.org/pandas-docs/stable/getting_started/10min.html) before proceeding to any of the exercises below.


## Exercise 8
Repeat exercise A.1 from Marsland, but create a Pandas DataFrame instead of a NumPy array.

```python
import pandas as pd

# Make an array a of size 6 × 4 where every element is a 2.
dfa = pd.DataFrame(np.full((6,4), 2))
print(dfa)
```

## Exercise 9
Repeat exercise A.2 using a DataFrame instead.

```python
# YOUR SOLUTION HERE
b = np.full((6,4), 1)
np.fill_diagonal(b, 3)
dfb = pd.DataFrame(b)
print(dfb)
```

## Exercise 10
Repeat exercise A.3 using DataFrames instead.

```python
# YOUR SOLUTION HERE
c = pd.DataFrame(dfa.values*dfb.values, columns=dfa.columns, index=dfa.index)
print(c)
```

## Exercise 11
Repeat exercise A.7 using a dataframe.

```python
# Write a function that consists of a set of loops that run through an array and count the number of ones in it. Do the same thing using the where() function (use info(where) to find out how to use it).
def num_ones_naive(input_df):
    count = 0
    for i in range(0, input_df.shape[0]):
        for j in range(0, input_df.shape[1]):
            if input_df.iloc[i][j] == 1:
                count += 1
                
    return count

def num_ones_fast(input_df):
    input_df.where(input_df==1, inplace=True)
    return len(input_df[0]) * len(input_df[1])

a = pd.DataFrame(np.full((4,4), 1))
print(num_ones_naive(a))
print(num_ones_fast(a))

```

## Exercises 12-14
Now let's look at a real dataset, and talk about ``.loc``. For this exercise, we will use the popular Titanic dataset from Kaggle. Here is some sample code to read it into a dataframe.

```python
titanic_df = pd.read_csv(
    "https://raw.githubusercontent.com/dlsun/data-science-book/master/data/titanic.csv"
)
```

Notice how we have nice headers and mixed datatypes? That is one of the reasons we might use Pandas. Please refresh your memory by looking at the 10 minutes to Pandas again, but then answer the following.


## Exercise 12
How do you select the ``name`` column without using .iloc?

```python
## YOUR SOLUTION HERE
titanic_df['pclass']
```

## Exercise 13
After setting the index to ``sex``, how do you select all passengers that are ``female``? And how many female passengers are there?

```python
## YOUR SOLUTION HERE
titanic_df = pd.read_csv(
    "https://raw.githubusercontent.com/dlsun/data-science-book/master/data/titanic.csv"
)
titanic_df.set_index('sex',inplace=True)
print(titanic_df.index.value_counts())

```

## Exercise 14
How do you reset the index?

```python
## YOUR SOLUTION HERE
```

```python
titanic_df.reset_index()
```

```python

```
