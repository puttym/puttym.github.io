---
layout: post
title: Disturbance Environment for Earth Orbiting Satellites
date: 2019-07-18
category: space
---

Satellites orbiting the earth, experience the following disturbance torques:

1. Gravity gradient torque
2. Magnetic field torque
3. Torque due to solar radiation pressure
4. Torque due to aerodynamic drag

The strength of these torques varies with the altitude. For example, gravity
gradient and magnetic field torques are strong in the Low Earth Orbit (LEO).
On the other hand, the torque due to aerodynamic drag is practically
non-existent in LEO and beyond, but it is the most dominant torque in the
very low earth orbits. Torque due to solar radiation pressure is constant 
across orbits but increases as one moves closer to the Sun.

The disturbance torques can not only change the attitude of the satellite but
also influence the choice of sensors and actuators. For example, in the
Low Earth Orbits (LEO), where the magnetic field is quite strong, we can use
magnetic torquer rods to apply control torques. However, the torquer rods may not
be the ideal choice in a geostationary orbit where the magnetic field is not
strong enough to produce a decent amount of control torque. Star sensors -- devices
that provide high accuracy attitude measurements -- are not  preferred in the 
*Van Allen Belts*. This is because the charge coupled devices (CCD) used in the
star sensors are highly sensitive to the extreme radiation that is characterises
Val Allen belts. Inner Van Allen belts extend from 1,600 km to 13,000, and the 
outer belts from 19,000 km to 40,000 km.

### Gravity gradient torques
The gravitational force on a satellite in orbit varies along the length of
the satellite. As a result of this, for elongated objects in orbit, the Center
of Gravity (CG) may be offset from the Center of Mass (CM). This creates a 
torque called the *Gravity gradient tortue*. This is hard for us to imagine
becaue, gravity, as we experience on earth is fairly constant -- the force we
experience on top of a two-storied building is not different from the force
we experience on the street!

It is worth noting that the location of CG is a function not only of the mass
configuration of the satellite, but also its current attitude.

### Magnetic Torque

Satellite carry a number of electronic equipment that generate a residual
magnetic field inside the vehicle. The dipole moment of these fields is of the
order of $$0.1 - 20\, \mathrm{A \cdot m^{2}}$$ and is a function of the spacecraft
size. In addition to this, the satellite also moves in a region that is inside
the spehere of influence of earth's magnetic field. If the magnetic dipole 
corresponding to the residual field is not aligned with the earth's field, then
the dipole experiences a torque given by $$\mathbf{D \times B}$$, where 
$$\mathbf{D}$$ is the dipole moment corresponding to the residual field, and
$$\mathbf{B}$$ is the strength of earth's magnetic field. Clearly, the torque
vanishes when $$\mathbf{D}$$ is aligned with $$\mathbf{B}$$. We see this torque
in action when the earth's magnetic field pulls a compass needle until the needle
is aligned with earth's magnetic field.

For calculating the torque experienced by the satellite dur to earth's magnetic
field, it is sufficient to consider the earth's magnetic field to be eminating
from a giant bar magnet hiding inside the earth. However, we must remember that
it is just an approximation and earth's magnetic behaviour is much more complex.

### Torque due to solar radiation pressure

Sunlight is a stream of photons. When an object is lit by sunlight, the photons
strike the object and transfer their momentum due to which the object experiences
some pressure. The actual pressure experienced by the object is a function of the
material properties of the object. Materials with good reflectivity experience
more pressure than those with good abosorbitivity. For example, a perfect
reflector, like an ideal mirror, will experience a pressure that is twice the
pressure experienced by a perfect absorber. 

Solar radiation pressure torque results from an offset from the center of
gravity of the satellite. Radiation pressure on a satellite can be thought to
be acting on a single point called the *center of pressure*.  A torque results
whenever the center of pressure is offset from the center of gravity of the
satellite (or any surface that is exposed to the Sun).

To understand how solar radiation pressure affects dynamic of a satellite, imagine
a flat surface on the satellite that is exposed to the Sun. Also imagine that
half of the plate us painted black and has higher absorbtivity than the other 
half. When sun rays awash the surface, the two halfs experience different pressures
because of their different material properties. This creates an offset between
center of pressure and center of gravity of the surface which results in torque.

In general, a satellite will have surfaces with different material properties
simultaneously exposed to the Sun. For example, solar arrays absorb more radiation
than a polished mettalic surface. Moreover, different surfaces surfaces are at 
different angles to the Sun. Surfaces that are directly facing the Sun receive
more radiation and experience more pressure than those that are at an angle. 

While solar radiation pressure can really influence the dynamics of a spacecraft,
the magnitude of the torque gets stronger as the spacecraft gets closer to the 
Sun. As we see in the next article, torque due to radiation pressure is not
the strongest disturbance torque experienced by a satellite.

### Torque due to atmospheic drag

Atmospheric drag results in a torque when the center of atmospheric pressure is
not aligned with the center of gravity of the spacecraft. 

Atmospheric drag is a significant force on earth. If you are wondering why I am
calling it significant, try cycling against the wind on a windy day! Drag is a 
lesser evil in space because the atmospheric density plummets exponentially
with altitude. Spacecraft in very low orbits, like the International
Space Station, do encounter enough number of particles to cause a noticeable
effect. In fact, in these orbits, drag is stronger than all other disturbances.
However, it fades in strength as one moves to higher orbits in LEO, and
practically disappears at Medium Earth Orbits (MEO).

 

 



<br />
*References*
1. NASA. *NASA's Van Allen Probes Spot an Impenetrable Barrier in Space*. 
https://www.nasa.gov/content/goddard/van-allen-probes-spot-impenetrable-barrier-in-space
Accessed on July 19, 2019

2. S R Starin and J Eterno. 19.1 Attitude Determination and Control System
