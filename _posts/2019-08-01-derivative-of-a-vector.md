---
layout: post
title: Time derivative of a vector of fixed magnitude
date: 2019-08-01
category: Physics
---

This post is about finding the derivative of a vector whose magnitude is fixed
but the direction is changing. For simplicity, we consider unit vectors of a
frame that is rotating with respect to an inertial frame. The result is applicable
to any arbitrary vector.

Let $$XYZ$$ be an inertial frame. Let $$\mathbf{\hat{I}}$$,
$$\mathbf{\hat{J}}$$, and $$\mathbf{\hat{K}}$$ be the unit vectors along $$X$$,
$$Y$$, and $$Z$$ axes respectively. Let $$xyz$$ be another frame that is
rotating at a constant angular velocity with respect to the $$Z-$$ axis of the
inertial frame. Let $$\mathbf{\hat{i}}$$, $$\mathbf{\hat{j}}$$, and
$$\mathbf{\hat{k}}$$ be the unit vectors along $$x$$, $$y$$, and $$z$$
directions.  Let the origins and axes of both the frames conincide at $$t=0$$
and let the $$xyz$$ frame rotate at an angular velocity $$\mathbf{\Omega}$$.
After time $$t$$, the $$x$$ and $$y-$$ axes make an angle $$\mathbf{\Omega}\, t
= \theta(t)$$ with $$X$$ and $$Y$$ axes respectively.  The orientation of the
$$xyz$$ frame relative to the inertial frame at time $$t$$ is shown in figure
below.

<figure> <img src="/assets/frames2.svg" alt="Rotating frames" width="500"
height="500"><br /> <figcaption><em>xyz</em> frame is rotating about the Z-axis
of the <em>XYZ</em> frame with a constant angular velocity</figcaption>
</figure>

<br />
We want to find the time derivative of $$\mathbf{\hat{i}}$$.

At the instant shown in figure, let $$(x_{i}, y_{i}, z_{i})$$ be the coordinates of
$$\mathbf{\hat{i}}$$. From firgure, we can write,

$$
\begin{equation}
\cos \theta = \frac{x}{\mathbf{\hat{||i||}}} \qquad 
\sin \theta = \frac{y}{\mathbf{\hat{||j||}}}
\end{equation}
$$

Since $$\mathbf{\hat{i}}$$ and $$\mathbf{\hat{j}}$$ are unit vectors, 
$$\mathbf{\hat{||i||}} = \mathbf{\hat{||j||}} = 1$$. Therefore, the coordiantes
of $$\mathbf{\hat{i}}$$ at any time $$t$$ are given by,

$$
\begin{equation}
(x_{i}, y_{i}, z_{i}) = (\cos \theta (t),\, \sin \theta (t),\, 0)
\end{equation}
$$

$$z-$$ coordinate is zero because $$\mathbf{\hat{i}}$$ lies in the $$xy-$$ plane.

Similarly, the coordinates of $$\mathbf{\hat{j}}$$ are given by,

$$
\begin{align}
(x_{j}, y_{j}, z_{j}) &= (\cos\, (90 + \theta (t)),\, \sin\, (90 + \theta (t)),\, 0) \nonumber \\
          &= (-\sin\, \theta (t), \cos\, \theta (t), 0)
\end{align}
$$

Since we want to find the time derivatives of unit vectors, let's differentiate
$$\mathbf{\hat{i}}$$ with respect to $$t$$.

$$
\begin{align}
\frac{d\mathbf{\hat{i}}}{dt} &= (-\sin \theta(t)\, \dot{\theta},\, \cos\, \theta(t)\, \dot{\theta},\, 0) \nonumber \\
&= \dot{\theta}\, (-\sin \theta(t),\, \cos \theta(t),\, 0) \nonumber \\
&= \mathbf{\Omega}\, \mathbf{\hat{j}} \label{eq:didt}
\end{align}
$$

Now, let's take the cross product of $$\mathbf{\Omega}$$ with
$$\mathbf{\hat{i}}$$ and observe something interesting.  Since
$$\mathbf{\Omega}$$ is along the $$Z-$$ axis, $$\mathbf{\Omega} = (0, 0,
\Omega)$$.

$$
\begin{equation}
\mathbf{\Omega} \times \mathbf{\hat{i}} = 
\begin{vmatrix}
\mathbf{\hat{i}} & \mathbf{\hat{j}} & \mathbf{\hat{k}} \\
0 & 0 & \Omega \\
1 & 0 & 0
\end{vmatrix} = 
\mathbf{\Omega}\, \mathbf{\hat{j}}
\end{equation}
\label{eq:cross-product}
$$

From equations \eqref{eq:didt} and \eqref{eq:cross-product}, we can write,

$$
\begin{equation}
\frac{d\mathbf{\hat{i}}}{dt} = \mathbf{\Omega} \times \mathbf{\hat{i}}
\end{equation}
$$

In general, for an arbitrary vector $$A$$ of fixed magnitude and changing
direction, the time derivative is given by,

$$
\begin{equation}
\boxed{
\frac{d\mathbf{A}}{dt} = \mathbf{\Omega} \times \mathbf{A}
}
\end{equation}
$$

<br />
*Reference*

Wikipedia. Rotating reference frame.
<https://en.wikipedia.org/wiki/Rotating_reference_frame>. Accessed on August 1,
2019.
