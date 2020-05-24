---
layout: post
title: Random Python notes
date: 2020-04-29
category: programming
---

+ `=` and `==` are operators. `=` is used to asign a value to a variable.
`==` is used to check if two values are equal. The result of the `==` operator
is a boolean and this can be used write crisp code.

```python
def is_divisible(x, y):
  return x % y == 0

# A more explicit version of the same function
def is_divisible(x, y):
  if x % y == 0:
    return True
  else:
    return False
```

+ **Void functions** are functions do not return any value. More precisely
their return value is `None`. A function can also return `None` if the 
program execution ends without hitting a return statement. The following
function returns `None` when `x = 0`. This function is incorrect because
it can not find the absolute value of `0`.

```python
def absolute(x):
  if x < 0:
    return -x
  if x > 0:
    return x 
```


+ **Types of Division:** Three types of division can be performed in Python.
  - *Conventional Division*: Returns a floating point number, always. Operator:
    `/`
  - *Floor division*: Returns the integer part of the division leaving out the
    decimal. The value returned is of either `int` or `float`. Operator: `//`
  - *Modulus operation*: Returns the reminder. The value returned is of either
    `int` or `float` type. Operator: `%` 

<br />
+ **User input** received via `input()` function is of type of `str`, by
  default. If required, it can be converted into an integer or a float by
  using the function `int()` or `float()`, respectively.

+ **Global variables** can be accessed from any function. They belong to a
special scope called `__main__`. They are not destropyed after the execution 
of the function.

+ **Local variables** are created when the function is called and disappear
after the function is executed. They are not accessible from outside of the
function in which they are first used.

+ **Parameters and Arguments**: Parameters are the variables names used in the
function definition. Arguments are the actual values passed on to the parameters
while executing the function.

In the example giveb below, `x` is the parameter, and 2 is the argument passed on
to it.

```python
def foo(x):
  return x**2

print(foo(x=6))
```

+ **if-else statement**
If more than one condition is true, then only the first true branch is run.
The following code returns `x is divisible by 9` even though the the last
condition is also true. This is because, once a condition is met, the remaining
conditions are not checked.

```python
x = 999

if (x % 2 == 0):
  print("x is even")
elif (x % 9 == 0):
  print("x is divisible by 9")
elif (x % 3 == 0):
  print("x is divisible by 3")
```

+ **Recursive Function:** A function that calls itself.
Example:
```python
def countdown(n):
  if n <= 0:
    print("Blastofff")
  else:
    print(n)
    countdown(n-1)
```

+ **Infinite Recursion** This happens when it becomes impossible to hit the 
return statement. In the example given below, for n = 2.5 (or any number 
with decimal part), the program doesn't meet the base case `n == 0` and
recurses forever. Apparently, the factorials of such numbers can be computed
using Gamma functions, and I don't know how.

```python
def factorial(n):
  if n == 0:
    return 1
  else:
    recurse = factorial(n-1)
    result = n * recurse
    return result 
```

+ **isinstance() function** takes two arguments: a value and a type and tells
us if the given value is of the given type or not. The result of `isinstance()`
is a boolean, meaning that the function returns either `True` or `False`.

```python
isinstance(4, int) #returns True
isinstance(4.0, int) #returns False
isinstance('4.0', float) #returns False
```
The infinite resursion seen in the `factorial(n)` function can be handled
better by using the `isinstance()` function.

```python
def factorial(n):
  if not isinstance(n, int):
    print("Factorial is defined only for integers")
    return None
  elif n < 0:
    print("Factorial is not defined for negative integers")
    return None
  elif n == 0:
    return 1
  else:
    recurse = factorial(n-1)
    result = n * recurse
    return result
```

+ **Return stament** exits the function.
  1. It need not always be at the end of the function
  2. It need not be followed by a variable name. 
```python
def print_n(text, n):
	if n <= 0:
		return
	else:
		print(text)
		print(text, n-1)
```
  3. A function can have more than one return statement.
```python
def compare(x, y):
	if x < y:
		return 1
	if x == y:
		return 0
	else:
		return -1
```

+ **Boolean expression**: An expression that is either true or false.
Example: `5 == 5` returns `True`, `5 == 6` returns `False`.

+ `True` and `False` are special values that belong to the type `bool`. They
are not strings. Try `type(True)` and `type(False)`

+ `int()` takes any value and returns an integer. 
  - If a decimal number is passed as an argument, the decimal part is chopped
    off and only the integer part is retained.
  - If a whole number is passed as a string, then the number will be converted
    into an integer. 
  - If a decimal number is passed as a string, an error message appears.
  - If a word is passed, an error message appears.

  Examples:
    - `int(3.14)` returns 3 
    - `int("3")` returns 3
    - `int("3.14")` returns an error message
    - `int("Hi")` returns an error message

<br />
* `float()` takes any value and returns a decimal number.
  - If an integer is passed as an argument, the decimal part will be added.
  - If a number (both integer and decimal) is passed as a string, then the
    corresponding floating point number is returned.
  - If a word is passed, an error message is returned.

  Examples:
    - `float(3)` returns 3.0
    - `float("3")` returns 3.0
    - `float("3.14")` returns 3.14
    - `float("Hi")` returns an error message

<br>
* **Split a number into integer and decimal parts**

```python
from math import modf

d, i = modf(123.456) #modf() returns a tuple
print(d) # Decimal part
print(i) # Integer part
```

* **Printing an enumerated list of array elements**
```python
for i in range(len(indicators)):
	print(str(i+1)+". "+indicators[i])
```
The trick is to convert the number (i+1) into a string so that it can be
concatenated with the text present in the array `indicators`.

<br />
*Reference*
1. Allen Downey. *Think Python. How to Think Like a Computer Scientist*. Green
   Tea Press, Needham, Massachusetts
