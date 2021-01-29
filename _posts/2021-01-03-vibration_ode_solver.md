---
layout: post
title: Solving the vibration ODE numerically - II
date: 2021-01-03
permalink: vibration-ode-code
---

A function to compute the mesh function should do the following:

1. Create a mesh. In the programming lingo, this is an array to store all the
mesh points.

2. Create another array to store the values of the mesh function calculated
at each mesh point.

3. Calculate the mesh funtion $$u^{n}$$ at each mesh point by executing the 
computational algorithm.


## Creating the arrays

Arrays to store mesh points and the mesh function are of length $$N_{t} +
1$$. But, how do we find $$N_{t}$$? $$N_{t} = T/\Delta t$$, where $$T$$ is
the simulation time and $$\Delta t$$ is the time step size. However, there is
slightly more to it than this simple ratio. For computational purposes, we
require $$N_{t}$$ to be an integer. That means, when $$N_{t}$$ becomes a
decimal, we should round it off to the nearest integer.

As an example, let $$T=8\, \text{s}$$ and $$\Delta t = 3\,\textrm{s}$$. Then,

$$
\begin{equation*}
N_{t} = \frac{T}{\Delta t} = \frac{8}{3} = 2.67.
\end{equation*}
$$

Rounding $$N_{t}$$ off to the nearest integer gives $$N_{t} = 3$$. But, this
changes the values of $$T$$ to 
$$N_{t} \times \Delta t = 3 \times 3\,\text{s} = 9\,\text{s}$$. Therefore, to
accommodate an integer value of $$N_{t}$$, we will reset $$T$$ to 
$$N_{t} \times \Delta t$$, where is $$N_{t}$$ is the integer value
we will be using for computation. Python code to accomplish this is given
below.

```python
T = 8, dt = 3
Nt = T/dt
Nt = round(Nt) # Returns an integer
T = Nt * dt # Resetting T

for n in range(1, Nt): # Runs from 1 to Nt-1 
    u[n+1] = 2*u[n] - u[n-1] - w**2*u[n]*dt**2 # Computes from u[2] to u[Nt]. Nt-1 values
```
In the 'for' loop, the variable `n` ranges from $$0$$ to $$N_{t}$$. However,
in the algorithm, it goes only till $$N_{t}-1$$. This difference between the
math and the code exists because of the way Python executes `for` loops.
While executing statements inside the `for` loop, the upper end of the range
is not considered. For example, if the given range is from $$n = 1$$ to $$n =
5$$, then the execution stops when the value of $$n$$ reaches $$4$$.
Similarly, in our algorithm, the execution stops at $$n = N_{t} - 1$$, which
is exactly what we want.


