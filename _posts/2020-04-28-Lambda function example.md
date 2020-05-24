---
layout: post
title: Lambda function example
date: 2020-04-28
category: programming
---

```python
import pandas as pd
import numpy as np
```


```python
df = pd.read_excel("../Data/Monthly_CO2_Concentrations.xlsx", 
                   converters={'Year':np.int32, 'Month':np.int32})
df = df.dropna()
df = df.reset_index(drop=True) 
```

`dropna()` -- Removes rows with `NaN` values. But the indices remain the same. That is, if row 8 is removed, then index 8 disappears and we see 9 after 7. This discontinuity in indexing is not an issue and we don't have to correct it. 

I seem to have OCD towards this, and hence I will correct it.

`reset_index(drop=True)` -- Removes the discontinuity in indexing. `drop=True` is necessary.
Otherwise you get a new index while retaining the old discontinuous index.


```python
year1 = df['Year'].astype(str)
month1 = df['Month'].astype(str)
month1 = month1.map(lambda x: '0'+x if len(x) == 1 else x)
df.index = year1 + '-' + month1 
```

This data set has monthly average of CO2 concentration for a number of years. Non-negative integers are used as indices, but a more intuitive index would be a 'year-month' combination. Something like '2020-04'. In other words, the year and month values must be concatenated with a hyphen separating the two values.

Creating this seemingly simple index involves many steps. 

1. Year and Month values are of type `int32`. Convert them to type `str`. Without this conversion, it would be impssoble to include a hypen because we would be asking the computer  to add (not concatenate) an integer to a string.

2. Note that the month value has a zero. While it's not mentioned anywhere, we know that a zero is prefixed only if the month value is less than 10. Again, the month value must be converted to `str` type before a zero is prefixed.

3. Concatenate year and month value with a hyphen (a string) in between. 

`astype(str)` -- Converts the values of the column to type `str`

lambda function -- This provides the logic for prefixing zero to the month value in string format. If the lenght of the string is 1, then 0 is prefixed. Else, month value is retained as it is.

`map()` -- Applies the lamba function to all month values. lambda function is passed as a parameter to the `map` method

New indices can also be obtained in a single line code, as shown below. It is same as above, but written in one line. With this, we don't have to create new variables for the string values of year and month. However, this reduces the readability.

Here the index values are assigned to a different variable to avoid confusion.


```python
n1 = df['Year'].astype(str) + '-' + df['Month'].astype(str).map(lambda x: '0'+x if len(x) == 1 else x)
```

## Lambda functions: What they are and what they are not

1. They have simple syntax. Easy to use with other functions like `map`, `filter`, etc

2. Use them for simple logics only

3. They are not a replacement normal functions defined with keyword `def`

4. Lambda functions are nameless. Because of this, TraceBack will not be able able specify
   the name if a lambda function has a problem
