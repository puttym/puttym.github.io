---
layout: post
title: Sizing Attitude Control Hardware
date: 2019-06-15
category: space 
---
Active control of spacecraft attitude can be achieved by combinations of
* Reaction wheels
* Momentum wheels
* Control moment gyros (CMG)
* Thrusters and
* Magnetic torquers

In this section, we size each of the above hardware (except CMG) for the hypothetical
satellite with the following specifications:

* **Mass:** $$215\, \mathrm{kg}$$ 

* **Moments of inertia:** $$I_{x} \approx I_{z} \approx 90\, \mathrm{kg \cdot
  m^{2}}$$, and $$I_{y} \approx 60\, \mathrm{kg \cdot m^{2}}$$

* **Orbit altitude:** $$700\, \mathrm{km}$$, Circular

* **Lifetime:** 5 years

* **Slew rate:** $$< 0.1^{\circ} \mathrm{/ s}$$ 

* **Pointing accuracy:** $$\approx 0.1^{\circ}$$ 

* **Mission:** Earth-pointing except for one optional $$30^{\circ}$$ maneuver
  per month to a target of opportunity

Note that the same satellite was used for calculating disturbance torques.

<br />
### Sizing of reaction wheels 
Sizing of reaction wheels requires determination of two parameters. They are:

1 **Angular momentum capacity**: Angular momentum capacity is calculated
keeping in mind the cyclic disturbances.  The wheel should have enough capacity
to store angular momentum resulting from cyclic disturbances without the need
for frequent desaturation. The minimum angular momentum capacity required is
determined by the average cyclic disturbance torque in a quarter or a half
orbit. 

In addition to calculating the momentum storage capacity, we shoudld also decide 
how often should the wheels be desaturated. This factor depends more on secular
disturbances because angular momentum resulting from them accumulate over time and
push the wheel towards saturation. Therefore, frequency of wheel desaturation 
depends on the secular torques and the momentum storage capacity of the wheel.

For 3-axis control, at least three wheels are required across each of the axes.
A fourth redundant wheel is highly desirable to continue the mission in the event
of failure of a wheel. Ideally, the wheels are mounted perpendicular to each 
other. Other configurations are also possible, but they come at a cost.

Let $$T_{D}$$ be the worst case cyclic disturbance torque. If it is due to gravity
gradient, then the maximum disturbance accumulates in quarter of an orbit -- like 
a sinusoidal wave. A simplified expression for such a disturbance torque is


$$
\begin{equation}
h_{RW} = (T_{D}) \frac{\text{P}}{4}\,(0.707)
\end{equation}
\label{eq:ang-mom-capacity}
$$

where,

$$h_{RW}$$ is the angular momentum of the wheel

$$T_{D}$$ is the worst case disturbance torque due to gravity gradient

$$0.707$$ is the rms value of a sinusoidal function 

$$P=5925\, \mathrm{s}$$ is the period of the satellite. It is calculated using
the formula $$\frac{2\pi}{\sqrt{\mu}} r^{3/2}$$, where $$\mu = 398,600\,
\mathrm{km^{3}/s^{2}}$$ is the gravitational parameter, and $$r$$ is the radius
of the satellite's orbit as measured from the center of the earth.

The worst case gravity gradient torque is experienced when the satellite is
operating in *target-of-opportunity* mode. The corresponding torque is 
$$4.5 \times 10^{-5} \mathrm{N \cdot m}$$. Plugging in these values into 
\eqref{eq:ang-mom-capacity}, the angular momentum capcity of the wheel is found
to be,

$$
\begin{equation*}
\boxed{h_{RW} = 4.6 \times 10^{-2}\, \mathrm{N \cdot m \cdot s}}
\end{equation*}
$$

We could go with a small reaction wheel with a momentum storage of 
$$0.4\, \mathrm{N \cdot m \cdot s}$$. This would also provide more than
9x margin.


2. **Torque authority**: Torque capacity is mostly driven by slew rate 
requirements. Slew rate and the required torque are related by the expression,

$$
\begin{equation}
\frac{\theta}{2} = \frac{1}{2}\frac{T_{RW}}{I}\left(\frac{t}{2}\right)^{2}
\end{equation}
\label{eq:wheel-torque}
$$

where,

$$\theta = 30^{\circ} = 30 \times \frac{\pi}{180}\, \mathrm{rad}$$ is the slew 
angle

$$T_{RW}$$ is the torque required for the slew 

$$I = 90\, \mathrm{kg \cdot m^{2}}$$ is the moment of inertia of the satellite 
along the slew axis

$$t=600\, \mathrm{s}$$ is the time taken for slew.

Solving for $$T_{RW}$$ in \eqref{eq:wheel-torque}, and substituting the above
values, we get,

$$
\begin{equation*}
\boxed{T_{RW} = 5.24 \times 10^{-4}\, \mathrm{N \cdot m}}
\end{equation*}
$$

<br />
### Sizing of momentum wheels
Momentum wheel spins almost at constant speed about the pitch axis. Unlike 
reaction wheels, momentum wheels do not change the attitude of the satellite,
but only maintain the current attitude. 

Since the momentum wheel spins along the pitch axis, it can influence both
roll and yaw accuracies. Yaw accuracy, disturbance torque, and the wheel 
momentum are related by the expression,

$$
\begin{equation}
T_{D} \times \frac{P}{4} = h_{MW} \theta_{a}
\end{equation}
\label{eq:mom-wheel}
$$

where $$\theta_{a}$$ is the yaw accuracy in radian.

Solving \eqref{eq:mom-wheel} for $$h_{MW}$$, and substituting the values, we get,

$$
\begin{equation}
\boxed{h_{MW} = 37.36\, \mathrm{N \cdot m \cdot s}}
\end{equation}
$$

<br />
### Sizing magnetic torquers
Let $$\mathbf{D}$$ be the dipole moment of the residual magnetic field inside
the spacecraft. If $$\mathbf{B}$$ is the strength of the earth's magnetic field,
then the maximum torque experienced by the dipole is given by $$T = D \cdot B$$, 
where $$D$$ and $$B$$ are the magnitudes of the corresponding vector quantities.

Since $$T = 4.5 \times 10^{-5}\, \mathrm{N \cdot m}$$ and 
$$B = 4.5 \times 10^{-5}\, \mathrm{Tesla}$$, the required dipole moment turns 
out to be

$$
\begin{equation}
\boxed{D = 1\, \mathrm{A \cdot m^{2}}}
\end{equation}
$$

I am not able to understand this because exactly the same equation was used
to calculate the torque due to magnetic field with an assumed dipole moment
of $$1\, \mathrm{A \cdot m^{2}}$$ !

<br />
### Sizing thrusters
Thrusters provide control torque to the satellite. Unlike reaction wheels, they
can change the total angular momentum of the satellite. They can also be used to
desaturate the wheels.

The torque provided by a thruster is given by,

$$
\begin{equation}
\mathbf{T} = \mathbf{F \times L}.
\end{equation}
$$

The torque is maximum when the direction of the force and the moment arm are
perpendicular to each other. Therefore, to counteract the worst-case disturbance
torque, the force required is,

$$
\begin{align*}
F &= \frac{T_{D}}{L} \\
  &= \frac{4.5 \times 10^{-5}}{0.5} \\
  &= 9 \times 10^{-5}\, \mathrm{N}.
\end{align*}
$$

where $$F$$, $$T_{D}$$, and $$L$$ are the magnitudes of the vector quantities
force, worst-case disturbance torque, and thruster moment arm respectively.

The required force for counteracting worst-case disturbance torque is very small.
This indicates that the thruster sizing is more likely to be determined by
slew rate requirements.

#### **Sizing force level to meet slew rates**
A thruster can change the angular momentum of the spacecraft by providing control
torque. In our example spacecraft, the slew rate requirement is given to be
$$30^{\circ}$$ in less than 10 minutes. We take the highest slew rate to be 
$$30^{\circ}$$ in 1 min. The required angular velocity for this maneuver is,

$$
\begin{equation*}
\dot{\theta} = \frac{30^{\circ}}{60\, \mathrm{s}} = 0.5^{\circ}\, \mathrm{s^{-1}}.
\end{equation*}
$$

The entire slewing maneuver can be divided into three parts:
1. The spacecraft accelerates angularly until its velocity reaches the target
value $$0.5^{\circ}\, \mathrm{s^{-1}}$$
2. The spacecraft maintains the angular velocity until the maneuvering operation
is over
3. The spacecraft decelerates angularly until its angular velocity reaches
zero.

Let's assume that the acceleration and deceleration each will take 5% of the 
total maneuver time (1 min). The corresponding angular acceleration is,

$$
\begin{align*}
\ddot{\theta} &= \frac{\dot{\theta}}{t} \\
              &= \frac{0.5^{\circ}\, \mathrm{s^{-1}}}{3\, \mathrm{s}} \\
              &= 0.169^{\circ}\, \mathrm{s^{-2}} \\
              &= 2.91 \times 10^{-3}\, \mathrm{rad \cdot s^{-2}} 
\end{align*}
$$  

To find the corresponding force, we use the relation $$T=F_{slew}L=I\ddot{\theta}$$,
where $$I = 90\, \mathrm{kg \cdot m^{2}}$$ is the moment of inertia across the 
roll (x) axis.

Solving for $$F$$, and substituting the values, we get,

$$
\begin{equation*}
\boxed{F_{slew} = 0.52\, \mathrm{N}}.
\end{equation*}
$$

A force of same magnitude, but applied in opposite direction, will be required
for deceleration.

#### **Sizing force levels for momentum dumping**
Secular disturbances push reaction wheels towards their saturation speeds.
Hence, wheels must be slowed down and desaturated regularly. The force required
to desaturate a wheel depends on the momentum storage capacity of the wheel
and the time it takes to desaturate the wheel.

The force level for desaturation of one wheel can be calculated by the formula,

$$
\begin{equation*}
F_{desat} = \frac{h}{Lt}
\end{equation*}
$$

Here, $$h$$ is the is the momentum storage of the wheel calculated earlier in
this article. Assuming that we want to desaturate one wheel in 1 sec, we get,

$$
\begin{equation*}
\boxed{F_{desat} = 0.8\, \mathrm{N}}
\end{equation*}
$$


#### **How many times should the thruster fire?**
Assume that the thruster fires only for
1. The $$30^{\circ}$$ slew maneuver
2. Desaturation of reaction wheels

Mission requirements state that the $$30^{\circ}$$ maneuvers are needed only
once in a month. Each maneuver has an acceleration pulse and a decelaration pulse.
Also, controlling movement of spacecraft's yaw axis requires rotation of the
spacecraft along pitch and roll axes, each of which require a separate pulse.
Therefore, each maneuver needs,

$$
\begin{equation*}
\text{2 pulses (for accn. and decn.)} \times \text{2 axes} = \text{4 pulses}.
\end{equation*}
$$

Since $$30^{\circ}$$ slew maneuver is a monthly event, there are $$4 \times 12
= 48$$ pulses in a year. 

Now, let's look at desaturation of wheels. Assume that there are 3 wheels and
each of them must be desaturated once every day. In one year, desaturation results
in,

$$
\begin{equation*}
\text{1 pulse} \times \text{3 wheels} \times \text{365 days} = \text{1095 pulses}.
\end{equation*}
$$

Therefore, total number of pulses per year is $$48 + 1095 = 1143$$. Since the 
design life of the satellite is 5 years, the thruster has to fire 
$$1143 \times 5 = 5715$$ pulses. 

Pulse ratings for small thrusters typically varies between 20,000 and 50,000.
Therefore, finding the thruster that meets our requirement won't be a problem.

#### **Estimating propellant mass**
Propollant mass consumed is a function of the force required and the duration
for which that force must be applied. It also depends on the specific impulse,
$$I_{sp}$$, of the fuel -- larger the value of $$I_{sp}$$ lower the fuel 
required.

The first step in estimating propellant mass is the calculation of total impulse.
Impulse is the product of force and the duration of application of the force.
The total impulse is the sum of slew maneuver impulse and the wheel desaturation
impulse.

$$
\begin{equation*}
\text{Impulse}_{tot} = \text{Impulse}_{slew} + \text{Impulse}_{desat}
\end{equation*}
$$

1. **Calculatinng slew maneuver impulse**: The slew maneuver has an acceleration
and a deceleration pulse each lasting $$3\, \mathrm{s}$$. The corresponding total
pulse duration over satellite's design life is 

$$
\begin{equation*}
48\, \text{per year} \times 5 \text{years} \times (3+3) \text{second} = 
1200\, \mathrm{s}
\end{equation*}
$$

As calculated before, the force required for slew maneuver is $$0.52\, \mathrm{N}$$.
The corresponding impulse is,

$$
\begin{equation*}
\text{Impulse}_{slew} = 0.52 \times 1200 = 624\, \mathrm{N \cdot s}
\end{equation*}
$$

2. **Calculating desaturation impulse:** The thruster has to fire 5475 pulses
in 5 years to desaturate the wheels. 

Since each pulse lasts $$1\, \mathrm{s}$$, the total desaturation pulse duration
for one wheel is $$365\, \mathrm{s} \times 5\, \text{years} = 1825\, \mathrm{s}$$. 
The corresponding impulse is $$0.8 \times 1825 = 1460\, \mathrm{N \cdot s}$$.
Therefore, for a three-wheel system, 

$$
\begin{equation*}
\text{Impulse}_{desat} = 3 \times 1460 = 4380\, \mathrm{N \cdot s}
\end{equation*}
$$

Total impulse due to both slew maneuver and desaturation is 
$$624 + 4380 = 5004\, \mathrm{N \cdot s}$$.

Propellant mass can now be estimated using the equation,

$$
\begin{equation*}
M_{p} = \frac{\text{Impulse}_{tot}}{I_{sp}\,g}
\end{equation*}
$$

Assuming that the thruster runs on hydrazine for which $$I_{sp}=200\, \mathrm{s}$$
is a conservative estimate, and taking $$g = 9.8\, \mathrm{m/s^{2}}$$, we get,

$$
\begin{equation}
\boxed{M_{p} = 2.55\, \mathrm{kg}}.  
\end{equation}
$$

<br />
*Reference*

1. W J Larson et al. Space Mission Analysis and Design. 3rd Edition. Published
jointly by Microcosm Press and Kluwer Academic Publishers 


