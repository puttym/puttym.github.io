---
layout: post
title: Introduction to attitude coordinates
date: 2019-09-29
category: space
---

Attitude coordinates are the set of coordinates that describe the orientation
of a rigid body. Technically, these coordinates describe the orientation of a
frame of reference attached to the rigid body relative to a reference frame.
For example, the attitude of a spacecraft relative to a ground station is
actually the orientation of the frame attached to the spacecraft relative to
the frame attached to the ground station. Similalry, the attitude of a
spacecraft relative to a distant star is the orientation of a frame attached to
the spacecraft relative to a frame attached to the star. In this case, the star
frame is assumed to be inertial and this arrangement is used to determine
spacecraft attitude using a star sensor.

A single spacecraft will have multiple frames defined in its flight dynamics
software. For example, there will be a spacecraft frame to describe the
attitude of the spacecraft relative to an inertial frame. However, the camera
of the spacecraft might have a frame attached to it. This frame will describe
the orientation of the camera frame relative to the spacecraft frame. 

A set of three parameters can completely define the attitude of an object. 
However, in practice we use sets that have more than three parameters. Some of
the attitude coordinate sets are:

* Direction Cosine Matrix
* Euler angles
* Principle rotation parameters
* Euler parameters (quaternions)
* Classical Rodrigues parameters 
* Modified Rodrigues parameters
* Stereographic orientation parameters

### Difference between position and attitude coordinates
There is a fundamental difference between position coordinates and attitude
coordinates. While the error in position between two frames can grow infinitely
large, the error in attitude can never be more than $$180^\circ$$.

### Four truths about attitude coordinates
1. A minimum of three coordinates is required to describe the relative angular
displacement between two reference frames.

2. Any minimal set of three coordinates will contain at least one geometrical
orientation where the coordinates are singular, namely at least two coordinates
are **undefined** or not unique.

3. At or near such a geometric singularity, the corresponding kinematic
differential equations are also singular.

4. The geometric singularities and associated numerical difficulties can be 
avoided altogether through regularisation. Redundant sets of four or more
coordinates exist that are universally valid.

Redundant sets avoid singularities at the cost of additional coordinates.
However, just having more than three coordinates doesn't guarantee that the set
will be non-singular. 

<br />
*References*

1. H Schaub and J Junkins. Analytical Mechanics of Space Systems. Published by
American Institute of Aeronautics and Astronautics, Inc


