---
layout: post
title: Euler's Equation for Spacecraft Attitude Control
date: 2019-06-10
category: space
---
The rotational motion of a rigid body is explained by the Euler equation,

$$
\begin{equation}
\dot{\mathbf{H}} = \mathbf{T} - \mathbf{\omega \times H},
\end{equation}
\label{eq:euler}
$$

where, \\
$$\mathbf{H}$$ is the angular momentum of the rigid body, $$\omega$$ is the
angular frequency, $$\mathbf{T}$$ is the external torque, and $$\dot{\mathbf{H}}$$
is the rate of change of angular momentum which is nothing but the net torque
on the body.

Euler equation is the fundamental equation of motion for rotational dynamics.
It is also the equation of conservation of angular momentum. In rotational
motion, angular momentum is the quantity that remains unchanged unless and until
an external torque acts on the body. It is the rotational analogue of linear
momentum -- the quantity that remains unchanged in translational motion unless
an external force acts on the body.

Angular momentum is calculated as the product of moment of inertia of the body
and its angular velocity. 

$$
\begin{equation}
\mathbf{H} = [I] \mathbf{\omega}
\end{equation}
\label{eq:ang-mom}
$$

where $$I$$ is a $$3 \times 3$$ symmetric matrix called the *inertia tensor.* 

The elements of the inertia tensor vary according to the frame in which the motion
is described. For every rotational motion, it is possible to find a frame of
reference in which the inertia tensor becomes becomes diagonal. Such a frame is
called the *principal axis frame*. Also, it is desirable to describe the motion
in principal axis frame as it greatly simplifies the inertia matrix.

In equation \eqref{eq:euler}, if $$\mathbf{T}=0$$, then 
$$\dot{\mathbf{H}} = \mathbf{\omega \times H}$$. Since angular momentum is a 
conserved quantity, its magnitude can not change. Also, in general, for 3D rigid
bodies, $$\mathbf{\omega}$$ and $$\mathbf{H}$$ are not parallel vectors and hence
their cross product is not zero. Therefore, in the absence of an external
torque, $$\dot{\mathbf{H}}$$ represents only a *change* in the direction of
$$\mathbf{H}$$. In other words, an external force is necessary to change the 
magnitude of the angular momentum vector. 

By substituting equation \eqref{eq:ang-mom} in equation \eqref{eq:euler},
we get,

$$
\begin{equation}
\dot{\mathbf{H}} = \mathbf{T} - \mathbf{\omega} \times [I] \mathbf{\omega}.
\end{equation}
$$

One might be tempted to conclude that that the cross product vanishes as 
$$\mathbf{\omega}$$ appears in both the vectors. This would have been the case
if $$[I]$$ were a scalar. Since $$[I]$$ is a tensor here, the product
$$[I] \mathbf{\omega}$$ is given by,

$$
\begin{equation}
I \mathbf{\omega} =
\begin{bmatrix}
I_{x} & 0 & 0 \\
0 & I_{y} & 0 \\
0 & 0 & I_{z}
\end{bmatrix}
\begin{bmatrix}
\omega_{x} \\
\omega_{y} \\
\omega_{z}
\end{bmatrix} =
\begin{bmatrix}
\omega_{x}I_{x} \\
\omega_{y}I_{y} \\
\omega_{z}I_{z}
\end{bmatrix}
\end{equation}
$$

Here $$[I]$$ is dioagonal because it is computed in the principal axis frame. Now,
the cross product becomes,

$$
\begin{aligned}
\mathbf{\omega} \times [I] \mathbf{\omega} &= 
\begin{vmatrix}
\hat{i} & \hat{j} & \hat{k} \\
\omega_{x} & \omega_{y} & \omega_{z}\\
\omega_{x}I_{x} & \omega_{y}I_{y} & \omega_{z}I_{z} \\
\end{vmatrix} \\
&= \hat{i}\left(I_{z} -I_{y}\right)\omega_{y}\omega_{z}
+ \hat{j}\left(I_{x} -I_{z}\right)\omega_{x}\omega_{z}
+ \hat{k}\left(I_{y} -I_{x}\right)\omega_{x}\omega_{y}
\end{aligned}
$$

A satellite will have different components like reaction wheels and gyroscopes
spinning inside the housing that contribute to the angular momentum of the
satellite. Therefore, the total angular momentum of the satellite 
$$\mathbf{H}$$ can be written as,

$$
\begin{equation}
\mathbf{H} = [I] \mathbf{\omega} + \mathbf{h},
\end{equation}
\label{eq:ang-mom-sat}
$$

where $$\mathbf{h}$$ is the angular momentum contributed by the rotating objects.

By plugging in equation \eqref{eq:ang-mom-sat} into equation \eqref{eq:euler},
we get,

$$
\begin{aligned}
\frac{\mathrm{d}}{\mathrm{d}t} ([I] \mathbf{\omega} + \mathbf{h}) &= 
\mathbf{T} - \mathbf{\omega \times H} \\
[I] \dot{\mathbf{\omega}} + \dot{[I]} \mathbf{\omega} + \dot{\mathbf{h}} &=
\mathbf{T} - \mathbf{\omega \times H} \\
[I] \dot{\mathbf{\omega}} &= \mathbf{T} - \dot{\mathbf{h}} - \dot{[I]}{\mathbf{\omega}}
- \mathbf{\omega \times H}.
\end{aligned}
$$

In this equation,

$$T$$ is the contribution by the external torque to attitude dynamics of the
satellite. 

$$\dot{\mathbf{h}}$$ provides the relationship between changes in the angular
velocity of rotating objects inside the satellite and the angular velocity
of the satellite itself. The torque provided by these objects are called
internal torques.

$$\dot[I]\mathbf{\omega}$$ shows how changes in mass distribution of the 
satellite can contribute to changes in the attitude of the spacecraft. A typical example is the 
unfolding of solar panels once the satellite is out of the launch vehicle.
This event completely changes the mass distribution of the satellite and hence
its inertia tensor. If there is no change in mass distribution, 
$$\dot[I]\mathbf{\omega} = 0$$.

The term $$\mathbf{\omega} \ times \mathbf{H}$$ is called the gyroscopic torque. 
It changes only the direction of the angular momentum of the satellite, but not 
the magnitude.

In summary, the angular acceleration of a satellite is influenced by,
* The external torques -- can change the total angular momentum of the satellite
* Internal torques -- Torque contribution by onboard objects. Can only
exchange momentum with different rotating parts of the satellite.
* Changes in mass distribution of the satellite and
* Gyroscopic torque.


