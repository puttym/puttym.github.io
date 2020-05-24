---
layout: post
title: Object Oriented Concepts - I
date: 2020-02-05
category: programming
---

# Classes and objects
Classes are the templates used to create objects. They don’t occupy any
storage. Defining class creates a class object.


```python
class Point():
    """Represents a point in 2D space"""
```

An **instance** of a class is an object that can be used for computing. An
instance of a class occupies storage. When you print instance, Python tells you
which class it belongs to and where it is stored.

The syntax for creating an instance of a class is similar to that of calling a
function.


```python
>>> Point()
>>> <__main__.Point at 0x7fc46c490f98>
```
As seen above, `Point()` creates an instance of the class `Point()`. Passing
the object to the `print` statement provides the follwing information:
    1. The class to which the object belongs
    2. The location at which the object is stored

```python
>>> print(Point())
>>> <__main__.Point object at 0x7fc46c490b00>
```
However, we generally want to assign the object to a varible name for
convenience. This is done via the assignment operator `=`. In the following
example, the object `Point()` is assigned to the variable `blank`.

```python
blank = Point()
```
The memory address of this object can be obtained by passing the variable name
to the `print` statement.

```python
>>> print(blank)
>>> <__main__.Point object at 0x7fc46c490d68>
```

An object can have named elements called **attributes**. For a `Point()`
object, the attributes can be `x` and `y` coordinates. The syntax for assigning
values to attributes is shown below.


```python
blank.x = 3.0
blank.y = 4.0
``` 
Here `blank` refers to a `Point()` object which contains two attributes. Each
attribute refers to a floating point number. 

The value of an attribute can be read by using the same syntax.


```python
>>> blank.x
>>> 3.0
```
Meaning of this expression is: "Go to the object `blank` refers to and get the
value of `x`".

Objects can be passed as an argument to a function, as shown below.

```python
import math
def print_point(p):
    print("(%g, %g)" %(p.x, p.y))
    
def distance_between_points(p1, p2):
    dx = p1.x - p2.x
    dy = p1.y - p2.y
    distance = math.sqrt(dx**2 + dy**2)
    return distance
    
blank1 = Point()
blank1.x = 6.0
blank1.y = 8.0
    
print_point(blank)
distance_between_points(blank, blank1)
```

    (3, 4)
    5.0



### Another example: Rectangle

In the case of the point, the attributes of the object were quite obvious. But,
this may not be the case always. For example, consider a class representing
rectangles. The attributes of an instance of a rectangle class object
can be thought of in the following ways:
  1. Specify one corner (or the center), the width, and the height
  2. Specify two end points of a diameter
  
Let's implement the first one.

```python
class Rectangle:
    """Represents a rectangle.
    Attributes: width, height, and corner"""
```

```python
box = Rectangle()
box.width = 100.0
box.height = 200.0
box.corner = Point()
box.corner.x = 0.0
box.corner.y = 0.0
```

The `Point()` object is assigned to the `corner` attribute of a `Rectangle()`
object. Since `Point()` has two attributes, will also become the attributes of
the `corner` attribute (??).

An onject that is an attribute of another object is **embedded**. 

The expression `box.corner.x` means: "Go to the object `box` refers to and
select the attribute named `corner`; then go to `Point()` object and pick the
attribute `x`".

### Instances as return values

Given below is a function that takes an instance of `Rectangle` as an argument
and returns an instance of `Point`. The attributes of the returned object
contain the `x` and `y` coordinates of the center of the rectangle represented
by the attributes of the `Rectangle` object.

```python
def find_center(rect):
    p = Point()
    p.x = rect.corner.x + rect.width/2
    p.y = rect.corner.y + rect.height/2
    return p
```

We will be tempted to print the result of this function by a simple `print()`
statement. However, it doesn't work because the object itself doesn't have the
coordinates of the center. They are infact stored as attributes to the `Point`
object. Therefore, we have to print the attributes.

Passing `box` as an argument and printing the attributes of the resulting
`point` object gives the rerquired result, but it's messy.


```python
>>> print(find_center(box).x, find_center(box).y)
>>> 50.0 100.0
```
A better way would be to format the output of the print statement.

```python
>>> print("(%g, %g)" %(find_center(box).x, find_center(box).y))
>>> (50, 100)
```

But the smart way is to use the `print_point(p)` functions we wrote earlier,
which was exactly written for the purpose of nicely printing out the attributes
of a `Point` object.

```python
>>> center = find_center(box)
>>> print_point(center)
>>> (50, 100)
```

### Attributes can be changed

If you remember, our `Rectangle` object has a widht of 100 units and a height
of 200 units. If you want a rectangle with different dimensions, you can either
change the existing `Rectangle` class object or create another object itself. 

```python
box.width = box.width + 50
box.height = box.height + 100
```

You can also write a function to do this. The function takes three arguments: a
`Rectangle` object, and the *change* in attributes.


```python
def grow_rectangle(rect, dwidth, dheight):
    rect.width += dwidth
    rect.height += dheight
```

Here is how we can use the `grow_rectangle(rect, dwidth, dheight)` function to
change the dimensions of a `Rectangle` object.


```python
>>> box.width, box.height #current dimensions (or values assigned to attributes)
>>> (150.0, 300.0)
```
```python
>>> grow_rectangle(rect=box, dwidth=50, dheight=100)
>>> box.width, box.height
>>> (200.0, 400.0)
```
Now, let's write a function to move the rectangle. It will have three
parameters: the `Rectangle` object that must be moved, movement along `x`
direction, and movement along `y` direction.


```python
def move_ractangle(rect, dx, dy):
    rect.corner.x += dx
    rect.corner.y += dy
```

The current coordinates of the corner of the `Rectangle` object referred by the
variable `box` are:


```python
>>> box.corner.x, box.corner.y
>>> (0.0, 0.0)
```
Let's invoke the `move_rectangle(rect, dx, dy)` function to move the corner of
the `Rectangle` object referred to by the variable `box`.

```python
>>> move_ractangle(rect=box, dx=3.0, dy=4.5)
>>> box.corner.x, box.corner.y
>>> (3.0, 4.5)
```

### Copying

In all the functions defined till now, `rect` is an alias for a `Rectangle`
object -- more specifically, the object referred to by the variable `box`.
Copying an object is often an alternative to aliasing.


```python
import copy
p1 = Point()
p1.x = 3.0
p1.y = 4.0
p2 = copy.copy(p1)
```

Variable `p2` refers to a copy of the `Point` object referred to by the
variable `p1`. However, variables `p1` and `p2` refer to two different
instances of the `Point` class object which have the same attribute values. The
fact that `p1` and `p2` are different can be verified by using the boolean
expression `is`.

```python
print(p1 is p2)
print(p1 == p2)
print(p1.x == p2.x)
print(p1.x is p2.x)
```

    False
    False
    True
    False


`p1 == p2` also resturns `False`. This is because `p1` and `p2` do not have any
values assigned to them and the compiler doesn't know what to compare. In fact,
while comparing objects, the `==` operator behaves same as `is` operator.

The comparison of `p1.x` and `p2.x` is straightforward because the attributes
of `p1` and `p2` are assigned same values. However, `is` operator shows that
they are two different entities with the same value assigned to them.

Now, let's copy an instance of the `Rectangle` class objects. It is different
from the `Point` object in the sense that it has another object embedded in it.


```python
box2 = copy.copy(box)
print(box2 is box)
print(box2.corner is box.corner)
print(box2.corner, box.corner)
```

    False
    True
    <__main__.Point object at 0x7fc456b78160> <__main__.Point object at 0x7fc456b78160>


Both `box` and `box2` have the same corner attribute. This is because, the
`corner` attribute is actually an instance of a `Point` class object which is
*not* copied by the `copy` command. The `corner` attribute of `box2` is
referring to the `corner` attribute of `box`, and hence `is` expression returns
`True`. Note that the `print()` function is referring to the same memory
location.

> The `copy` command does not copy the embedded objects, and hence it is called
> **shallow copy**.

A better way of copying objects is to use `deepcopy` -- a method provided by
the `copy` module that copies the embdded objects as well. `deepcopy` copies
everything: even the objects that are embedded in an embedded object.


```python
box3 = copy.deepcopy(box)
print(box3 is box)
print(box3.corner is box.corner)
print(box3.corner, box.corner)
```

    False
    False
    <__main__.Point object at 0x7fc456ccac50> <__main__.Point object at 0x7fc456b78160>


Clearly, `box3` and `box` are two different objects. The attribute `corner` is
also different for both the objects (see different memory locations).

Given below is a slightly modified version of the `move_rectangle()` function
we wrote earlier. The previous version changed the values of the attribute
`corner` and assigned them to an existing instance of the `Rectangle` class.
The version given below does the following:
  1. Create a new instance of the `Rectangle` class
  2. Modify the `corner` attributes
  3. Assign the modified `corner` attributes to the newly ceated instance of the `Rectangle` class


```python
def move_rectangle1(rect, dx, dy):
    rect = copy.deepcopy(box)
    rect.corner.x += dx
    rect.corner.y += dy

move_rectangle1(rect=box4, dx=3.0, dy=4.0)
print(box4.corner.x, box.corner.x)
print(box4.corner.y, box.corner.y) 
```

    6.0 3.0
    8.5 4.5


### Debugging

You get an `AttributeError` when you try to access an attribute that doesn't
exist. An example is given below.


```python
p = Point()
p.x = 3.0
p.y = 3.87
p.z
```


    AttributeError: 'Point' object has no attribute 'z'


Pyhton's built-in function `hasattr()` can be used to check before hand if an
object has a particular attribute.


```python
print(hasattr(p, 'x'))
print(hasattr(p, 'z'))
```

    True
    False


The syntax for the `hasattr` function is `hasattr(object, 'attribute')`.


<br />
Reference:

Allen Downey. *Think Python*. Green Tea Press.


Permission is granted to copy, distribute, and/or modify this document under
the terms of the Creative Commons Attribution-NonCommercial 3.0 Unported
License, which is available at <http://creativecommons.org/licenses/by-nc/3.0/>.
