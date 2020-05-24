---
layout: post
title: Abosolute derivative of a vector represented in a rotating frame
excerpt: A vector is defined in a rotating frame. How to find its time derivative relative to an inertial frame?
category: physics
date: 2019-07-29
---
$$XYZ$$ is an inertial frame. $$xyz$$ is a frame that is rotating with an angular
velocity $$\mathbf{\Omega}$$ relative to the inertial frame. $$\mathbf{\hat{I}}$$,
$$\mathbf{\hat{J}}$$, and $$\mathbf{\hat{K}}$$ are unit vectors along $$X$$,
$$Y$$, and $$Z$$ directions respectively. $$\mathbf{\hat{i}}$$,
$$\mathbf{\hat{j}}$$, and $$\mathbf{\hat{k}}$$ are unit vectors along $$x$$,
$$y$$, and $$z$$ axes respectively. The orientation of the two frames are shown
in the figure below.

Our goal is to find the time derivative of a time-dependent vector 
relative to the inertial frame. It's a bit tricky because we know the components
of the vector in the non-inertial frame $$xyz$$. The derivative relative to
an inertial frame is called the **absolute derivative**.

<figure>
<img src="/assets/moving-frames.svg" alt="Rotating frames" width="500" height="500"><br />
<figcaption><em>xyz</em> frame is rotating with a constant angular velocity relative
to <em>XYZ</em> frame</figcaption>
</figure>

<br />
Let $$\mathbf{Q}$$ be an arbitrary time-dependent vector. In the inertial frame,
its components are,

$$
\begin{equation}
\mathbf{Q} = Q_{x}\mathbf{\hat{I}} + Q_{y}\mathbf{\hat{J}} + Q_{z}\mathbf{\hat{K}}
\end{equation}
$$

where $$Q_{x}$$, $$Q_{y}$$, and $$Q_{z}$$ are functions of time. Since $$XYZ$$
is an inertial frame, $$\mathbf{\hat{I}}$$ $$\mathbf{\hat{J}}$$, and 
$$\mathbf{\hat{K}}$$ are fixed. 

Therefore,

$$
\begin{equation}
\frac{d\mathbf{Q}}{dt} = \frac{dQ_{X}}{dt}\mathbf{\hat{I}} +
\frac{dQ_{Y}}{dt}\mathbf{\hat{J}} +
\frac{dQ_{Z}}{dt}\mathbf{\hat{K}}.
\end{equation}
$$

$$\mathbf{Q}$$ can also be resolved into components in the $$xyz$$ frame. Let

$$
\begin{equation}
\mathbf{Q} = Q_{x}\mathbf{\hat{i}} + Q_{y}\mathbf{\hat{j}} + 
Q_{z}\mathbf{\hat{k}}.
\end{equation}
\label{eq:q-xyz}
$$

Since $$xyz$$ frame is rotating relative to the inertial frame, its unit vectors
are not fixed and are constantly changing their direction. However, since they
are unit vectors, their magnitudes remain unchanged.

Therefore, the absolute time derivative of equation \eqref{eq:q-xyz} is given by,

$$
\begin{equation}
\frac{d\mathbf{Q}}{dt} = \frac{dQ_{X}}{dt}\mathbf{\hat{i}} +
\frac{dQ_{Y}}{dt}\mathbf{\hat{j}} +  \frac{dQ_{Z}}{dt}\mathbf{\hat{k}} + 
Q_{x}\frac{d\mathbf{\hat{i}}}{dt} + Q_{y}\frac{d\mathbf{\hat{j}}}{dt} + 
Q_{z}\frac{d\mathbf{\hat{k}}}{dt}  
\end{equation}
\label{eq:dQ}
$$

[The absolute time derivative](https://puttym.github.io/physics/2019/08/01/derivative-of-a-vector.html) 
of a vector with constant magnitude and varying direction is given by,

$$
\begin{equation}
\frac{d\mathbf{\hat{i}}}{dt} = \mathbf{\Omega} \times \mathbf{\hat{i}} \qquad
\frac{d\mathbf{\hat{j}}}{dt} = \mathbf{\Omega} \times \mathbf{\hat{j}} \qquad
\frac{d\mathbf{\hat{k}}}{dt} = \mathbf{\Omega} \times \mathbf{\hat{k}}, \qquad
\end{equation}
\label{eq:di}
$$

where $$\mathbf{\Omega}$$ is the angular velocity of the vector relative to an inertial
frame.

Substituting equation \eqref{eq:di} into equation \eqref{eq:dQ} yields,

$$
\begin{aligned}
\frac{d\mathbf{Q}}{dt} &= \frac{dQ_{x}}{dt}\mathbf{\hat{i}} +
\frac{dQ_{y}}{dt}\mathbf{\hat{j}} +  \frac{dQ_{z}}{dt}\mathbf{\hat{k}} + 
Q_{x}\mathbf{\Omega} \times \mathbf{\hat{i}} +
Q_{y}\mathbf{\Omega} \times \mathbf{\hat{j}} + 
Q_{z}\mathbf{\Omega} \times \mathbf{\hat{k}} \\
&= \frac{dQ_{x}}{dt}\mathbf{\hat{i}} +
\frac{dQ_{y}}{dt}\mathbf{\hat{j}} +  \frac{dQ_{z}}{dt}\mathbf{\hat{k}} + 
(\mathbf{\Omega} \times Q_{x}\mathbf{\hat{i}}) +
(\mathbf{\Omega} \times Q_{y}\mathbf{\hat{j}}) + 
(\mathbf{\Omega} \times Q_{z}\mathbf{\hat{k}}) \\
&= \frac{dQ_{x}}{dt}\mathbf{\hat{i}} +
\frac{dQ_{y}}{dt}\mathbf{\hat{j}} +  \frac{dQ_{z}}{dt}\mathbf{\hat{k}} + 
\mathbf{\Omega} \times (Q_{x}\mathbf{\hat{i}} + Q_{y}\mathbf{\hat{j}} + Q_{z}\mathbf{\hat{k}})
\end{aligned}
$$

$$
\begin{equation}
\boxed{\frac{d\mathbf{Q}}{dt} = \frac{d\mathbf{Q}}{dt}\Bigg)_{\substack{\text{Moving}\\ \text{frame}}} +
\mathbf{\Omega} \times \mathbf{Q}}
\end{equation}
$$

where,

$$
\begin{equation}
\frac{d\mathbf{Q}}{dt}\Bigg)_{\substack{\text{Moving}\\ \text{frame}}}= 
\frac{dQ_{x}}{dt}\mathbf{\hat{i}} +
\frac{dQ_{y}}{dt}\mathbf{\hat{j}} + 
\frac{dQ_{z}}{dt}\mathbf{\hat{k}}
\end{equation}
$$

is the time derivative of $$\mathbf{Q}$$ relative to $$xyz$$ frame. Note that
this is not the absolute time derivative.

The absolute time derivative and the time derivative in $$xyz$$ frame are equal when
$$\mathbf{\Omega} = 0$$. This situation corresponds to pure translation with no
acceleration and the invarience of time derivative is in accordance with the
[special principle of relativity](https://en.wikipedia.org/wiki/Principle_of_relativity).

<br />
*Reference*

Howard Curtis. Orbital Mechanics for Engineering Students. Elsevier 
Butterworth - Heinemann
