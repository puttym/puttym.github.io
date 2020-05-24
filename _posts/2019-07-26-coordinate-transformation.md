---
layout: post
title: Coordinate transformation matrix
category: physcis
date: 2019-07-26
---
$$XYZ$$ and $$xyz$$ define two frames of reference with a common origin. The
$$x-$$ axis of the $$xyz$$ frame coincides with the $$Y-$$ axis of the $$XYZ$$
frame. The orientations of $$y$$ and $$z$$ axes with respect to $$Y$$ and $$Z$$
axes are as shown in the figure. $$\mathbf{I}$$, $$\mathbf{J}$$, and $$\mathbf{K}$$
are the unit vectors along $$X$$, $$Y$$, and $$Z$$ directions respectively. 
Similarly, $$\mathbf{i}$$, $$\mathbf{j}$$, and $$\mathbf{k}$$ are the unit vectors 
along $$x$$, $$y$$, and $$z$$ directions respectively. 

<figure>
<img src="/assets/frames.svg" alt="Coordinate frames" width="500" height="500"><br />
<figcaption>Relative orientation of <em>XYZ</em> and <em>xyz</em> frames</figcaption>
</figure>


<br />
Any vector in the $$XYZ$$ frame can be represented in the $$xyz$$ frame and
vice versa. The two representations will of course have different components.
In this article, let's derive the matrix of transformation from $$xyz$$ to $$XYZ$$
frame. For the sake of simplicity, let's use unit vectors for this exercise.
However, the resulting transformation matrix works for any matrix.

In $$xyz$$ frame, $$\mathbf{I}$$, $$\mathbf{J}$$, and $$\mathbf{K}$$ can be represented as,

$$
\begin{align}
\mathbf{I} &= Q_{11}\,\mathbf{i} + Q_{12}\,\mathbf{j} + Q_{12}\,\mathbf{k} \nonumber \\
\mathbf{J} &= Q_{21}\,\mathbf{i} + Q_{22}\,\mathbf{j} + Q_{23}\,\mathbf{k} \label{eq:one}\\
\mathbf{K} &= Q_{31}\,\mathbf{i} + Q_{23}\,\mathbf{j} + Q_{33}\,\mathbf{k} \nonumber
\end{align}
$$

where $$Q_{ij} (i,j = 1, 2, 3)$$ are the direction cosines. They are the
cosines of the angles between the vector and the three coordinate axes. They
can be calculated by taking the dot product of the vector with the unit vector
along each axis. For example, the direction cosines of the vector $$\mathbf{v}
= v_{x}\,\mathbf{p}+v_{y}\,\mathbf{q}+v_{z}\,\mathbf{r}$$, are given by,

$$
\begin{equation}
\cos\, {a} = \frac{\mathbf{v} \cdot \mathbf{p}}{||\mathbf{v}||} \qquad 
\cos\, {b} = \frac{\mathbf{v} \cdot \mathbf{q}}{||\mathbf{v}||} \qquad 
\cos\, {c} = \frac{\mathbf{v} \cdot \mathbf{r}}{||\mathbf{v}||}
\end{equation},
$$
 
where $$a$$, $$b$$, and $$c$$ are the angles between $$\mathbf{v}$$ and $$\mathbf{p}$$,
$$\mathbf{q}$$, and $$\mathbf{r}$$ directions respectively. 

Let's say $$\mathbf{I}$$ makes angles $$\alpha$$, $$\beta$$, and $$\gamma$$ 
with $$\mathbf{i}$$, $$\mathbf{j}$$, and $$\mathbf{k}$$ directions respectively. Then,

$$
\begin{equation*}
Q_{11} = cos\, \alpha = \mathbf{I} \cdot \mathbf{i} \qquad 
Q_{12} = cos\, \beta = \mathbf{I} \cdot \mathbf{j} \qquad 
Q_{13} = cos\, \gamma = \mathbf{I} \cdot \mathbf{k}.
\end{equation*}
$$

In the figure, we can observe that $$\alpha = 90^\circ$$, $$\beta = -[90+(90-\theta)]$$,
and $$\gamma = -(90-\theta)$$. The cooresponding direction cosines are,

$$
\begin{align}
Q_{11} &= cos\, \alpha = \cos\, 90^{\circ} = 0  \nonumber \\
Q_{12} &= cos\, \beta = \cos\, [-(180 - \theta)] = \cos\, (180-\theta) = -\cos\, \theta \label{eq:dcos-I} \\
Q_{13} &= cos\, \gamma = \cos\, [-(90-\theta)] = \cos\, (90-\theta) = \sin\, \theta. \nonumber
\end{align}
$$
 
Similarly, the direction cosines of $$\mathbf{J}$$ and $$\mathbf{K}$$ are found to be, 

$$
\begin{align}
Q_{21} &= 1 \qquad Q_{22} =& 0 \qquad Q_{23} &= 0 \label{eq:dcos-J}\\ 
Q_{31} &= 0 \qquad Q_{31} =& \sin\, \theta \qquad Q_{33} &= \cos\, \theta \nonumber
\end{align}
$$
 
Substituting equations \eqref{eq:dcos-J} and \eqref{eq:dcos-I} into \eqref{eq:one}
yields,

$$
\begin{align*}
\mathbf{I} &= -\cos\, \theta\, \mathbf{j} + \sin\, \theta\, \mathbf{k} \\
\mathbf{J} &= \mathbf{i} \\
\mathbf{K} &= \sin\, \theta\, \mathbf{j} + \cos\, \theta\, \mathbf{k}.
\end{align*}
$$

In matrix form, the above equation can be written as,

$$
\begin{equation}
\begin{pmatrix}
\mathbf{I} \\
\mathbf{J} \\
\mathbf{K} 
\end{pmatrix} = 
%
\begin{bmatrix}
0 & -\cos\, \theta & \sin\, \theta \\
1 & 0 & 0 \\
0 & \sin\,\theta & \cos\, \theta
\end{bmatrix}
%
\begin{pmatrix}
\mathbf{i} \\
\mathbf{j} \\
\mathbf{k}
\end{pmatrix}.
\end{equation}
\label{eq:transformation}
$$

For an arbitrary vector 
$$\mathbf{v} = v_{x}\, \mathbf{i} + v_{j}\, \mathbf{y} + v_{k}\, \mathbf{z}$$,
equation \eqref{eq:transformation} becomes,

$$
\begin{equation}
\begin{pmatrix}
\mathbf{v_{X}} \\
\mathbf{v_{Y}} \\
\mathbf{v_{Z}} 
\end{pmatrix} = 
%
\begin{bmatrix}
0 & -\cos\, \theta & \sin\, \theta \\
1 & 0 & 0 \\
0 & \sin\,\theta & \cos\, \theta
\end{bmatrix}
%
\begin{pmatrix}
\mathbf{v_{x}} \\
\mathbf{v_{y}} \\
\mathbf{v_{z}}
\end{pmatrix}.
\end{equation}
$$

*Reference*
Howard Curtis. Orbital Mechanics for Engineering Students. Elsevier Butterworth-Heinemann
