---
layout: post
title: Pandas basics
date: 2019-07-20
category: programming
---
DataFrame is the fundamental data structure provided by Pandas. It is a class
with different attributes. In this article, `df` is the name of the
dateframe. 

<br />
### Creating a dataframe from a file
```python
import pandas as pd
df = pd.read_csv("filename.csv")
df = pd.read_csv("ES.txt",delimiter=',') #TXT file
```

<br />
### What columns are there in the dataframe?
```python
df.columns #Output is an Index - a pandas data structure. This doesn't mention all the column headers
df.columns.values #Prints ALL column headers. An Index
list(df.columns.values) #Writes columns headers into a list
```
The output is an 'Index' - a data structure provided by pandas.
```python
df.columns[1] #Accessing a column by its index
df['col_name'] #Accessing a column by its name
```

Individual columns are of type Series - one more data structure provided by
pandas. Printing a Series prints out column values with indices.

```python
col_name = df['col_name']
type(col_name)
col_name[0] #Print first element of column col_name
col_name[col_name] #Slicing. The result is another Series
```

<br />
### Making sense of information in columns 

Suppose `col_name` has five unique values, say 1 to 5. Since each of them can
appear in multiple rows, it makes sense to know that how many times they have
appeared. In other words, We want to know in how many rows 1 has appeared, in
how many rows 2 has appeared etc.  The result is a series.

```python
df.col_name.value_counts() #Counts the occurence of each value 
df.col_name.value_counts()_sort_incex() #Sorts the list based on the values of #col_name
```
