---
layout: post
title: Understanding __init__ and __str__ methods
date: 2020-02-17
category: programming
---

## The `__init__()` method

The `__init__()` method makes it easier to instantiate an object. 

Let's understand it through a simple example.


```python
class Time:
    """Represents time of the day"""
    
    def __init__(self, hour = 0, minute = 0, second = 0):
        self.hour = hour
        self.minute = minute
        self.second = second
        
    def __str__(self):
        return '%.2d:%.2d:%.2d' % (self.hour, self.minute, self.second)
```
The code above defines `Time` - a class for representing time of the day. 
The attributes of the class are `hour`, `minute`, and `second`.  By definition,
they are also the attributes of the instance `self`. 

The class also has two methods defined, nameley, `__init__()` and `__str__()`.
The `__init__()` method has four parameters:

  1. `self` - an instance of the class `Time`
  2. `hour` - an integer
  3. `minute` - an integer
  4. `second` - an integer.

It is tempting to conclude that the class attributes are passed as parameters
to the `__init__()` method. However, the fact is that, the parameters of
`__init__()` method are delibertely given the same names as the attributes. 
Also, the parameters of the `__init__()` method are initialised to zero.  

In the function body, the class attributes are assigned the values of the
method parameters.  As a result, the attributes are also initialised to zero.
When instantiating a new object, the attributes take the values assigned to
method parameters. With `__init__()` method in place, objects can be
instantiated from a single command.


```python
t1 = Time(1, 2, 3)
t2 = Time1(4, 5, 6)
```

Technically, it is not necessary to have same names for class attributes and
method parameters. However, they are given common names for the sake of 
convenience.

For example, in the code snippet shown below, the class atrributes and method
parameters are given different names. While the code is logically correct,
the choice of variable names makes it less intuitive to understand and hence 
more difficult to maintain in the long term.


```python
class Time1:
    """Represents time of the day"""
    
    def __init__(self, car = 0, bus = 0, cycle = 0):
        self.hour = car
        self.minute = bus
        self.second = cycle
```
### What's in a name?  
Now comes the interesting part. We know that the function name
doesn't influence what a function does. It is like any other
variable name - just a label to identify and use a particular piece of code.

Things *appear* to become a bit different when you are dealing with methods
like `__init__()` and `__str__()`. For example, if you change the name from
`__init__()` to `foo()`, without changing the body, the functionality provided
by `__init__()` is lost. This is interesting because we have changed only the
function name but not the body.


```python
class Time2:
    """Represents time of the day"""
    
    def foo(self, hour = 0, minute = 0, second = 0):
        self.hour = hour
        self.minute = minute
        self.second = second
```


```python
t3 = Time2(10, 23, 45)
```
Output: 


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-22-8184df36575a> in <module>()
    ----> 1 t3 = Time2(10, 23, 45)
          2 print(t3)


    TypeError: object() takes no parameters

How can this happen? What's going on? 

Let's dig a bit deeper to understand to understand this better.

When we create an instance, the following steps are carried out under the hood.

  1. The interpreter invokes the method `__call__()`.
  2. `__call__()` method invokes `__new__()` method, which creates a new
     instance.
  3. `__call__()` method then calls `__init__()` method which initialises the
     instance created by `__new__()`.
  
`__init__()` is a predefined function in Python. But, there is also a provision
to define it the way we want it to be and make it part of the class definition.
Our definition, obviously, will be a new method and it doesn't change the
original function. 

While invoking `__init__()` method, the `__call__()` method first looks at the
class definition. If `__init__()` is available there itself, then that version
is invoked. If not, the pre-defined version is invoked.

When you change the name from `__init__()` to `foo()` in the class definition,
`__call__()` concludes that `__init__()` is not defined in the class and uses
the pre-defined version of `__init__()`. Obviously, this is not going to give
you the functionality that you implemented in the method `foo()`. Figure 1
shows a flowchart for choosing the `__init__()` method.

Of course, it is possible to instantiate an object without including the
`__init__()` method in the class definition. But, this takes more effort.


```python
t3 = Time2()
t3.hour = 10
t3.minute = 23
t3.second = 45
``` 

If you observe closely, our `__init__()` method is just a function-form of this
syntax!

<figure>
<img src="/assets/init.png" alt="init method flowchart" width="595" height="452"><br />
<figcaption>Figure 1. Flowchart for choosing the __init__() method</figcaption> 
</figure>

<br />

In summary,

> + `__init__()` method enables you to instantiate objects with a single command. 
> + It provides a function-like syntax for instantiating objects and setting
>   their attribute values.

## The `__str__()` method

`__str__()` function makes it easier to display objects using `print()`
function. If `__str__()` is not included in the class definition, `print()`
displays some meta data concerning the object.

As an example, let us print the `t2` - an instance of the class `Time1`. I am
particulalrly considering `Time1` because the class definition doesn't include
`__str__()` method.

```python
print(t2)
```
Output:

    <__main__.Time1 object at 0x7f09a8496d30>


There is no error message, but we are not getting what wanted to see.

However, printing an instance of `Time` gives no surprises because it has a
`__str__()` method defined.


```python
print(t1)
```
Output:


    01:02:03


So, what's happening here? 

Like `__init__()` method, `__str__()` is also a pre-defined function. As in the
case of `__init__()`, you can define your own version of `__str__()`, and
include it in the class definition.

When you try to print an object, the `print()` function calls `__str__()`
method and prints the value that is returned by it. If the class definition
contains a `__str__()` method, then the value returned by that function is
printed. Otherwise, the value returned by the pre-defined `__str__()` is
printed. Figure 2 shows a flowchart for choosing the `__str__()` method.

<br />

<figure>
<img src="/assets/str.png" alt="__str__() flowchart" width="522" height="472"><br />
<figcaption>Figure 2. Flowchart for choosing the __str__() method</figcaption>
</figure>

<br />

Scroll up and look at the body of `__str__()` method in the definition of `Time`
class. It converts the attribute values from integers to string, and returns
one string value in a particular format. When called, the `print()` function
simply displays the formatted string value.

## Conclusion

+ `__init__()` methods makes it easy to instantiate objects. `__str__()` makes
  it easy to print objects.

+ Including `__init__()` and `__str__()` methods in the class definition is
  useful but not necessary. 

+ Both of them are pre-defined functions. But they can also be defined by users
  to be included in their classes.

+ The scope of user-defined `__init__()` and `__str__()` methods is limited to
  the class in which they are defined.

+ When dealing with `__init__()` and `__str__()`, the method names are as
  important as the method body. This is because there are other methods that
are programmed to look for functions with names `__init__()` and `__str__()`.

+ `__call__()` method invokes the `__init__()` to initialise an object with a
  given set of attribute values. Similarly, `print()` calls `__str__()` method
to display the string representation of the object.

+ In both the cases, the pre-defined versions are called only when the
  user-defined versions are not available.  


***References***
  1. Allen Downey. *Think Python. How to Think Like a Computer Scientist*.
     Green Tea Press, Needham, Massachusetts
  2. John Sturtz. *Python Metaclasses*. https://realpython.com/python-metaclasses/
     Accessed on 2020-02-17.
