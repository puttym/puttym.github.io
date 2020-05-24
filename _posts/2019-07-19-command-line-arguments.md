---
layout: post
title: Undertsanding Command line Arguments in Python
date: 2019-07-20
category: programming
---
Often, passing arguments to a programme through the command line is a useful
option. Python's `argparse` moduel provides the necessary tools for
achieving this.

Passing command line arguments involves the following steps:
<ol>
	<li>Import <code>ArgumentParser</code> class from <code>argparse</code> module</li>
	<li>Create an instance of <code>ArgumentParser</code></li>
	<li>List out the arguments that you pass on through the command line</li>
	<li>Ask the program to inspect the command line for arguments and store them into computer memory.</li>
</ol>
These steps can be implemented as given below:

```python
import argparse
x = argparse.ArgumentParser() # x is an instance of the class ArgumentParser
x.add_argument("p")
x.add_argument("q")
arguments = x.parse_args() # saving command line arguments into computer memory

print(arguments) # print the arguments provided
```

The <code>print()</code> statement at the end confirms that the arguments
provided via command line are indeed stored in the variable
<code>arguments</code>.

Now, let's dig a little deeper and find the datatype of the stored values.

```python
print(type(arguments.p), type(arguments.q))
```

The output of the above command clearly shows that both of them are stored as
strings. In fact, unless specified, <code>argparse</code> treats arguments as
strings. Therefore, if we want to compute something, we need to specifically
ask <code>argparse</code> to consider the parameters as numbers (either integer
or floating point number).

```python
x.add_argument("p", type = int)
x.add_argument("q", type = int)
```

With this, we are in a position to do something useful. As an example, given
below is a programme that takes two numbers from the command line and does some
calculations using them.

```python
def square(x):
    return x*x

def cube(x):
    return x*x*x

def main():
    from argparse import ArgumentParser

    x = ArgumentParser()
    x.add_argument("p", type = int)
    x.add_argument("q", type = int)
    arguments = a.parse_args()
    print(square(arguments.p) + cube(arguments.q))

if __name__ == "__main__":
    main()
```
