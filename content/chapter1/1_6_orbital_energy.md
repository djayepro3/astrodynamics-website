# Orbital Energy and the Vis-Viva Equation

Orbital energy is a **fundamental conserved quantity** in astrodynamics. By understanding it, we can predict velocities at different points in an orbit and design maneuvers such as **transfers** and **injections**.

---

## 1. Total Mechanical Energy of an Orbit

A satellite’s motion is governed by the balance between:

* **Kinetic energy**:

  $$
  T = \frac{1}{2}mv^2
  $$
* **Potential energy** (gravitational):

  $$
  U = -\frac{GMm}{r}
  $$

Thus, the **total orbital energy** is:

$$
E = T + U = \frac{1}{2}mv^2 - \frac{GMm}{r}
$$

---

## 2. Specific Orbital Energy (per unit mass)

To make the expression independent of the satellite’s mass $m$, we define **specific orbital energy**:

$$
\epsilon = \frac{v^2}{2} - \frac{\mu}{r}, \quad \mu = GM
$$

### Important property:

* $\epsilon$ is **constant for a two-body system**.
* This means energy does not change along the orbit (neglecting perturbations).

---

## 3. Energy of Different Orbits

Depending on the orbit shape:

* **Elliptical orbit ($e < 1$)**:
  $\epsilon < 0$
* **Parabolic orbit ($e = 1$)**:
  $\epsilon = 0$
* **Hyperbolic orbit ($e > 1$)**:
  $\epsilon > 0$

This classification shows how energy dictates whether an object is **bound** (satellite), at **escape velocity**, or on a **flyby trajectory**.

---

## 4. The Vis-Viva Equation

By combining conservation of energy with orbital geometry, we obtain the **vis-viva equation** (“living force” in Latin):

$$
v^2 = \mu \left( \frac{2}{r} - \frac{1}{a} \right)
$$

where:

* $v$ = orbital velocity at distance $r$
* $\mu = GM$ (gravitational parameter)
* $a$ = semi-major axis of the orbit

### Key points:

* At **perigee** ($r = r_p$): velocity is **maximum**.
* At **apogee** ($r = r_a$): velocity is **minimum**.
* In circular orbits ($r = a$):

  $$
  v = \sqrt{\frac{\mu}{a}}
  $$

---

## 5. Example: Low Earth Orbit (LEO)

For Earth ($\mu = 398600 \, \text{km}^3/\text{s}^2$):

* $a = 6678 \, \text{km}$ (Earth radius + 300 km altitude)

$$
v = \sqrt{\frac{398600}{6678}} \approx 7.73 \, \text{km/s}
$$

This matches the orbital speed of the **International Space Station (ISS)**.

---

## 6. Python Visualization: Velocity Along Orbit

```python
import numpy as np
import matplotlib.pyplot as plt

mu = 398600  # km^3/s^2
a = 10000  # km
e = 0.5  # eccentricity

# True anomaly
theta = np.linspace(0, 2*np.pi, 500)

# Radius at each point
r = a*(1 - e**2) / (1 + e*np.cos(theta))

# Velocity from vis-viva
v = np.sqrt(mu * (2/r - 1/a))

plt.figure(figsize=(8,5))
plt.plot(theta*180/np.pi, v)
plt.xlabel("True Anomaly (degrees)")
plt.ylabel("Velocity (km/s)")
plt.title("Velocity Variation Along an Elliptical Orbit")
plt.grid()
plt.show()
```

✅ This plot shows how orbital velocity changes — fastest near **perigee**, slowest near **apogee**.

---

## 7. Why the Vis-Viva Equation Matters

* Used in mission design (e.g., **Hohmann transfers**).
* Allows calculation of required **delta-v** for maneuvers.
* Links geometry (orbit shape) with dynamics (velocity, energy).

---

## 8. References

* Curtis, *Orbital Mechanics for Engineering Students*, Ch. 2–3
* Vallado, *Fundamentals of Astrodynamics and Applications*, Ch. 2
* Bate, Mueller, White, *Fundamentals of Astrodynamics*
* NASA Technical Reports on orbital mechanics (e.g., NASA SP-8021)

---

📂 **File location:**
`content/chapter1/1_6_orbital_energy.md`
