---
layout: post
title: Random pandas notes
date: 2020-05-12
category: machine learning
---

*A dump of pandas functions which I have found useful. Use with discretion.*

* **Plotting code example**

```python
import matplotlib.pyplot as plt
import pandas a pd

fig = plt.figure(figsize=(6,6)) # Create a Figure object
ax = fig.subplots() # Create an AxesSubplot object
#Both Figure and AxesSubplot are classes defined in matplotlib

#Plot CO2 on y-axis and index along x-axis.
df['CO2'].plot(kind='line', color='b', ax=ax)

#If two columns are being plotted, then we should speficy both of them
df.plot(x='x-column', y='y-column', kind='line', color='b', ax=ax)

ax.set(title='Title', xlabel='XLabel', ylabel='Ylabel')
ax.legend().set_visible(False) #Remove legend
ax.legend(loc="upper left")

#Rotate x-tick labels. For datetime objects see below
for tick in ax.get_xticklabels():
	tick.set_rotation(45)

#Formatting datetime tick labels
fig.autofmt_xdate()

fig.savefig('file.png', transparent=False, dpi=300, bbox_inches='tight')
plt.show()
```

* **Change datatype of selected columns while creating a dataframe**
  - Use the `converters` parameter
```python
df = pd.read_excel("datafile.xlxs", converters={'Year':np.int32, 'Month':np.int32})
```
  In the above example, the datatype of columns 'Year' and 'Month' are
  changed to `numpy.int32`.

* **Changing indices in a dataframe**
```python
df.index=df['Year'] # Indices changed to Year column
df.reset_index(drop=True) # Indices changed to default values
df.reset_index('Year') # Indices changed to Year column
```
  In the above example, the indices are first changed to 'Year' values.
  `reset_index` with parameter `drop` switches the indices back to
  default values

* **Print entire dataframe/series/column**
```python
print(df.to_string()) # Print entire dataframe
print(df['Year'].to_string()) # Print all values of the column Year
```

* **Sorting a data frame by column/s**
```python
df = df.sort_values(['Year', 'Month'])
df.sort_values(['Year', 'Month'], inplace=True) # Same as above
```
  Year values are sorted first, and then Month values are sorted without
  without affecteing the order of Year values.

  Suppose there are 5 year values which are not sorted. Each each year
  has 12 month values which again are not sorted. The above command
  first sorts the year values, and then sorts the month values for each year
  value.

  `sort_values` has the following parameters. (Refer to documentation
  for a complete list)
    - `ascending`: boolean. Default is `True` 
    - `inplace`: boolean. Default is `False`. Returns a sorted object
	if `False`, and returns nothing if `True`.
    - `axis`: 0 or `index` to sort rows. 1 or `columns` to sort columns
    - `na_position`: `first` or `last`. Sets the position of `Nan` values.
	Default: `last`
    - `kind`: Algorithm used for sorting. 
       Accepted values: 
       1. `quicksort` 
       2. `mergesort` 
       3. `heapsort`.

        	Default is `quicksort`.

<br>
* **Dealing with NaN values**
```python
df.dropna() # Drop rows with NaN values
df.isnull().sum() # Find number of NaN values
```

* **Selection by row number**
```python
df.iloc[2:60] #selects rows from 2 to 59
```

* **Number of rows and columns in a dataframe**
```python
df.shape #Returns the tuple (rows, cols)
df.shape[0] #Returns the first entry in the tuple. This is the no. of rows
df.shape[1] #Returns the second entry in the tuple. This is the no. of cols
```

* **Reading date and time from a file** 
To read string objects as datetime objects, set the `parse_date` parameter.

You can either set it to `True` or the column whose values muct be interpreted
as datetime objects.

By default it is set to `False`.
```python
df = pd.read_csv("filename.csv", parse_dates=["Column"])
df = pd.read_csv("filename.csv", parse_dates=True)
```
