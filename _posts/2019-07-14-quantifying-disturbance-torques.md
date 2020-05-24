---
layout: post
title: How Strong are the Disturbance Torques?
date: 2019-07-18
category: space
---

In this article, we quantify the disturbance torques that we discussed in the
previous article. For this purpose, we consider a hypothetical satellite with
the following properties. The calculated torque values are given at the end of
the article.

### Properties of the hypothetical satellite

* **Mass:** $$215\, \mathrm{kg}$$ 

* **Moments of inertia:** $$I_{x} \approx I_{z} \approx 90\, \mathrm{kg \cdot
  m^{2}}$$, and $$I_{y} \approx 60\, \mathrm{kg \cdot m^{2}}$$

* **Orbit altitude:** $$700\, \mathrm{km}$$, Circular

* **Lifetime:** 5 years

* **Slew rate:** $$< 0.1^{\circ} \mathrm{/ s}$$ 

* **Pointing accuracy:** $$\approx 0.1^{\circ}$$ 

* **Mission:** Earth-pointing except for one optional $$30^{\circ}$$ maneuver
  per month to a target of opportunity


<br />
### Calculating gravity gradient torque

Gravity gradient torque depends mainly on the orbital radius and the moments of
inertia of the satellite. Between the two, orbital radius has a stronger
effect.  It also depends on slew angle with torque reaching a maximum for a
slew angle of $$45^{\circ}$$.

The magnitude of gravity grdient torque can be estimated using the formula
given below.

$$
\begin{equation}
T_{g} = \frac{3 \mu}{2 R^{3}}\left|I_{z} - I_{y}\right| \sin\, 2\theta
\end{equation}
$$

$$T_{g}$$ -- Torque due to gravity gradient disturbances

$$\mu = 3.986 \times 10^{14}\, \mathrm{m^{3} s^{-2}}$$  is Earth's
gravitational constant

$$R = (6378 + 700) = 7078\, \mathrm{km}$$ is the orbital radius

$$I_{z}$$ and $$I_{y}$$ are moments of inertia of the satellite along row and
pitch axes respectively

$$\theta = 30^{\circ}$$ is the maximum deviation of the z-axis from the local
vertical.  Note that this deviation happens when the satellite is in
target-of-opprtunity mode.

<br />
### Calculating torque due to magnetic field

Magnetic torque increases linearly with both the dipole moment of the residual
magnetic field and earth's magnetic field strength at the orbit.  However, the
orbital radius has the strongest influence on this because earth's magnetic
field strength plummets drastically as one moves farther away from the earth.

A simplified expression for magnetic torque is given below.

$$
\begin{equation}
T_{m} = DB \approx D \frac{2M}{R^{3}}
\end{equation}
$$

$$T_{m}$$ is the torque due to magnetic field

$$D$$ is the dipole moment of spacecraft's residual magnetic field. We assume
it to be $$1 \mathrm{A \cdot m^{2}}$$

$$B$$ is strength of earth's magnetic field; approximated as
$$\frac{2M}{R^{3}}$$ where $$M = 7.95 \times 10^{15}\, \mathrm{Tesla \cdot
m^{3}}$$, is the magnetic moment of the earth, and $$R$$ is the distance from
the center of the dipole (earth) to the spacecraft.

<br />
### Calculating torque due to solar radiation pressure

Torque due to solar radiation pressure depends on a number factors including
the area of surface exposed to the Sun, material properties of the exposed
surface, and angle of incidence of the Sun. It should obviously depend on
distance from the Sun, but this dependence is concealed in solar constant -- a
factor that increases as we move closer to the Sun.

A simplified equation for calculating torque due to solar radiation pressure
is given below.

$$
\begin{equation}
T_{sp} = \frac{F_{s}}{c} A_{s} (1+q) (c_{ps} - c_{g})\, \cos I
\end{equation}
$$

$$T_{sp}$$ is the torque due to solar radiation pressure

$$F_{s} = 1361\, \mathrm{W/m^{2}} $$ is the solar constant. It is the energy
received from the Sun over a unit area in one second

$$c = 3 \times 10^{8} \mathrm{m/s}$$ is the speed of light in vacuum

$$A_{s}$$ is the area of the surface exposed to the Sun. It is assumed to be 
$$2\, \mathrm{m} \times 1.5\, \mathrm{m} = 3\, \mathrm{m^{2}}$$

$$q$$ is the reflectance factor. It is $$0$$ for perfect absorbers and $$1$$
for perfect reflectors. All real materials have their $$q$$ values between
these limits. For our example, we assume $$q = 0.6$$

$$(c_{ps} - c_{g})$$ is center of pressure's offset from the center of gravity.
Assumed to be $$0.3$$ in this example

$$I$$ is the angle of incidence of the Sun. It is assumed to be zero

<br />
### Calculating torque due to atmospheric drag

Atmospheric drag is proportional to the square of the speed of the satellite.
However, the effect of satellite speed is balanced by very low atmospheric
densities that are common in outer space. Speed will have a greater influence
in very low earth orbits where the atmospheric density is not really low.
That's why atmospheric drag torque is strongest in those orbits and practically
vanishes at MEO.

$$
\begin{equation}
T_{a} = \frac{1}{2} \rho C_{d} A V^{2} \left(c_{pa} - c_{g}\right)
\end{equation}
$$

$$\rho = 10^{-13}\, \mathrm{kg/m^{3}}$$ is the atmospheric density at the 
orbit altitude. For comparison, density at sea level is a little more than 
$$1\, \mathrm{kg/m^{3}}$$ 

$$C_{d}$$ is the drag coefficient of the spacecraft which is assumed to be
$$2.0$$. For comparison, an aerodynamically designed Mercedes Benz A-Class has
a drag coefficient of $$0.22$$ and a typical bus' drag coefficient is in the
range of $$0.6 - 0.8$$. Lower the drag coefficient, better the aerodynamic
efficieny

$$A$$ is the surface area. Assumed to be $$3\, \mathrm{m^{2}}$$

$$V$$ is the spacecraft velocity. In a $$700\, \mathrm{km}$$ orbit, it is about
$$7,504\, \mathrm{m/s}$$

$$\left(c_{pa} - c_{g}\right)$$ is center of pressure's offset from the center
of gravity. Assumed to be $$0.2$$ in this example

<br />
### Calculated torque values

All values in $$\mathrm{N \cdot m}$$

$$
\begin{aligned}
T_{g} = 4.4 \times 10^{-5} \\
T_{m} = 4.5 \times 10^{-5} \\
T_{s} = 6.6 \times 10^{-6} \\
T_{a} = 3.4 \times 10^{-6}
\end{aligned}
$$

<br />
*References*
1. W J Larson et al. Space Mission Analysis and Design. 3rd Edition. Published
jointly by Microcosm Press and Kluwer Academic Publishers 

2. Firstpost. Mercedes-Benz A-Class sedan has lowest drag-coefficient of any
   production car.
https://www.firstpost.com/tech/auto/mercedes-benz-a-class-sedan-has-lowest-drag-coefficient-of-any-production-car-4822801.html
Accessed on July 18, 2019

3. The Engineering Toolbox. Drag Coefficient.
   https://www.engineeringtoolbox.com/drag-coefficient-d_627.html Accessed on
July 18, 2019
