---
layout: post
title: Meaning of if __name__ == "__main__" in Python
date: 2019-07-20
category: programming
---

Simple answer: `if __name__ == "__main__"` helps a programme to choose and pick
chunks of code from other programmes. 

Without this, the called programme will be executed fully, even if only one
function is required by the calling programme.

Let's look at an example. Assume that we already have a programme that has
separate functions to find square and cube of a number. Such a programme could
be as given given below. Let's also assume that the programme is stored in the
file `test.py`.

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
    arguments = x.parse_args()
    print(square(arguments.p) + cube(arguments.q))

if __name__ == "__main__":
    main()
```

Let's say we just want to write a programme to compute the cube of a number.
Since this functionality is already available in `test.py`, as smart
programmers, we simply want to call that particular chunk of code and use it.
Such a programme, say `test1.py` could be as given below.

```python
import test

def main():
    from argparse import ArgumentParser

    x = ArgumentParser()
    x.add_argument("a", type = int)
    y = x.parse_args()
    print(test.cube(y.a))

if __name__ == "__main__":
    main()
```

Now, if you run `test1.py`, you will notice that only the function `cube` from
`test.py` is executed, but not the entire programme. Without `if __name__ ==
"__main__"`: condition, running `test1.py` results in completely running
`test.py` (this actually gives an error msg).

<br />
### What's happening?

When executing a programme, the Python interpreter creates the special variable
`__name__` and assigns a string value to it. In the case of a stand-alone
programme, the value assigned is `__main__`. This is the case when `test.py` is
run. 

However, when the programme is executed as module, then the module name is
assigned to the `__name__` variable. This is what happens when `test1.py`,
which calls a function from `test.py`, is run. Here, `test.py` is used as a
module and the value `test` is assigned to the variable `__name__` in
`test.py`. Note that this is happening in `test.py`, but not in `test1.py`.

The statement `if __name__ == "__main__":` simply checks if the value assigned
to `__name__` is `__main__`. When running `test.py`, this check yields a
positive result and the subsequent statement is executed.

While running `test1.py`, `__name__` has the value `test`. Therefore, 
`if __name__ == "__main__":` returns a negative result, and the subsequent
statement is not executed.
