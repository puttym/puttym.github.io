---
layout: post
title: Solving the vibration ODE numerically - I
date: 2021-01-03
category: mathematics
permalink: vibration-ode-mesh
---

The simplest model of a vibrating mechancal system is of the form:

$$
\begin{equation}
\frac{d^{2}u}{dt^{2}} + \omega^{2} u = 0, \quad u(0) = I, u'(0) = 0, t \in (0,T].
\end{equation}
\label{eq:vib-ode}
$$

$$t \in (0, T]$$ means that Eq. \eqref{eq:vib-ode} is not valid at $$t = 0$$. This
makes sense because at $$t = 0$$, $$u = I$$, as given by the initial condition.

The analytical solution of Eq. \eqref{eq:vib-ode} is given by,

$$
\begin{equation}
u(t) = I \cos\, \omega t.
\end{equation}
$$

That is, $$u$$ oscillates with an angular frequency $$\omega$$ and amplitude
$$I$$. The initial condition determines the amplitude of the vidration. In
Eq. \eqref{eq:vib-ode}, $$t$$ varies continuously from $$0$$ to $$T$$. Since
there is an $$u(t)$$ for each $$t$$, there are infinitely many values of
$$t$$ and $$u(t)$$ in the continuous solution. However, when we intend to
find a numerical solution, we no longer deal with the continuous problem
stated above.

## Discretizing the Domain
The first step in finding the numerical solution is to discretise the domain.
We change the problem domain from $$(0, T]$$ to $$[0, T]$$, and let it be
represented by,

$$
\begin{equation}
0 = t_{0} < \underbrace{t_{1} < t_{2} < \cdots < t_{N_{t} - 1} < t_{N_{t}} = T}_{N_{t} \text{ points}}.
\end{equation}
\label{eq:num-domain}
$$

The collection of these points makes a *mesh* or a *grid*. Since there are
$$N_{t}$$ points from $$t_{1}$$ to $$t_{N_{t}}$$ (both included), there are
$$N_{t}+1$$ points in the mesh. The mesh points are often uniformly spaced,
but this is not a strict requirement. In our mesh, we denote the spacing,
$$t_{n+1} - t_{n}$$, between two consecutive points by $$\Delta t$$. It can
be easily proved that $$t_{n} = n\Delta t$$.

$$
\begin{align*}
t_{n+1} - t_{n} &= \Delta t \\
t_{n+1} &= t_{n} + \Delta t \\
&= (t_{n-1} + \Delta t) + \Delta t \\
&= (t_{n-2} + \Delta t)  + 2 \Delta t \\
&= \vdots \\
&= t_{0} + n \Delta t \\
&= n \Delta t \quad (\text{because } t_{0} = 0)
\end{align*}
$$

Our goal is to find $$u^{n}$$ ($$0 < n < N_{t}$$) - the *numerical approximation* to
the exact solution $$u(t_{n})$$ at $$t = t_{n}$$. The collection of all
$$u^{n}$$ values constitutes the mesh function. Unlike the exact solution, the 
mesh function is not continuous and is defined only at certain discrete points.

## Fulfilling the equation at mesh points

To compute the numerical solution, it is sufficient if Eq. \eqref{eq:vib-ode} is
valid at the mesh points. Hence, Eq. \eqref{eq:vib-ode} now reduces to 
a set of $$N_{t}+1$$ differential equations.

$$
\begin{align*}
u''(t_{0}) + \omega^{2}\,u(t_{0}) &= 0, \quad u(0) = I \\
u''(t_{1}) + \omega^{2}\,u(t_{1}) &= 0, \quad u(0) = I \\
& \vdots \\
u''(t_{N_{t}-1}) + \omega^{2}\,u(t_{N_{t}-1}) &= 0, \quad u(0) = I \\
u''(t_{N_{t}}) + \omega^{2}\,u(t_{N_{t}}) &= 0, \quad u(0) = I \\
\end{align*}
$$

Or, more succintly,

$$
\begin{equation}
u''(t_{n}) + \omega^{2}\, u(t_{n}) = 0, \quad n = 0, 1, 2, \cdots N_{t}, \quad u(0) = I, \
\quad u'(0) = 0
\end{equation}
\label{eq:vib-dis}
$$

For $$n = 0$$, the value of the mesh function is identical to the value of
$$u$$ as given by the initial condition.

Did you notice that, in Eq. \eqref{eq:num-domain}, we made a subtle change in
the problem domain specification? This is because, we require Eq.
\eqref{eq:vib-dis} to be valid at every mesh point, including $$t_{0} = 0$$,
even though Eq. \eqref{eq:vib-ode} is not valid at that point (it *is* valid
as close to $$t_{0}=0$$ as we like, but not *at* $$t_{0}=0$$). 

## Formulating the recursive algorithm

The next step is to replace the derivatives in Eq. \eqref{eq:vib-dis} with
finite difference equations. There are two derivatives: one in the
ODE itself, and the other in the form of an initial condition. Let's replace
both of them with the following second-order accurate finite difference
approximations:

$$
\begin{equation}
u''(t_{n}) \approx \frac{u^{n+1} - 2u^{n} + u^{n-1}}{\Delta t^{2}} 
\end{equation}
\label{eq:second-derivative}
$$

and

$$
\begin{equation}
u'(t_{n}) \approx \frac{u^{n+1} - u^{n-1}}{2\Delta t}.
\label{eq:first-derivative}
\end{equation}
$$

Since $$u'(0) = 0$$ (initial condition),

$$
\begin{equation*}
u'(0) \approx \frac{u^{1} - u^{-1}}{2 \Delta t} = 0,
\end{equation*}
$$

and hence,

$$
\begin{equation}
u^{1} = u^{-1}. 
\end{equation}
$$

Inserting Eq.\eqref{eq:second-derivative} into Eq. \eqref{eq:vib-dis}, we get,

$$
\begin{equation}
\frac{u^{n+1} - 2u^{n} + u^{n-1}}{\Delta t^{2}} = - \omega^{2}u^{n}.
\end{equation}
$$

Rearranging the terms, we get the recursive equation:

$$
\begin{equation}
\boxed{
u^{n+1} = 2u^{n} - u^{n-1} -\omega^{2}u^{n}\Delta t^{2}, \\
\text{where }n = 0, 1, \ldots, N_{t} - 1, \quad u(0) = I, \quad u'(0) = 0.
}
\end{equation}
\label{eq:vib-recursive}
$$

If we know the values of $$u^{n-1}$$ and $$u^{n}$$, then we can find $$u^{n+1}$$
using Eq. \eqref{eq:vib-recursive}.

The following observations can be made about Eq. \eqref{eq:vib-recursive}:

1. It is an algebraic equation that can be solved on a computer.

2. The value of mesh function $$u^{n+1}$$ at a point $$t_{n+1}$$ depends on the 
values of the mesh function at two previous points $$t_{n-1}$$ and $$t_{n}$$.
Hence the name *recursive equation.*

3. $$n$$ varies from $$0$$ to $$N_{t}$$, while it varies from $$0$$ to $$N_{t} - 1$$
in Eq. \eqref{eq:vib-dis}. This is because, for $$n = N_{t}$$, LHS in
Eq. \eqref{eq:vib-recursive} would be out of problem domain.

## The computational algorithm

We are now in a position compute the value of the mesh function at each of the 
mesh points.

1. $$u^{0}$$ is straightforward as it is given as an intitial condition.

2. We can compute $$u^{1}$$ by substituting $$n=0$$ into Eq. \eqref{eq:vib-recursive}.
    However, this introduces the term $$u^{-1}$$ which lies outside the problem domain.
    We can deal with this situation by substituting $$u^{-1} = u^{1}$$ (See
    Eq. \eqref{eq:first-derivative}). With this, we get, 
    $$u^{1} = u^{0} - \frac{1}{2}\Delta t^{2} \omega^{2} u^{0}$$

3. Calculate $$u^{2}, u^{3}, \ldots, u^{N_{t}}$$ using Eq. \eqref{eq:vib-recursive}.

**Reference**
1. Hans Petter Langtangen and Svein Linge. *Finite Difference Computing with PDEs - 
A Modern Software Approach*
