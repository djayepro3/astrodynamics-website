# 2.5 Differential Equations in Astrodynamics

## Why Differential Equations?

In astrodynamics, motion is governed by **Newton’s Second Law**:

$$
\mathbf{F} = m \mathbf{a} = m \frac{d^2 \mathbf{r}}{dt^2}
$$

* **Position** $\mathbf{r}(t)$ is a function of time
* **Velocity** $\mathbf{v}(t)$ is the derivative of position
* **Acceleration** $\mathbf{a}(t)$ is the derivative of velocity

Thus, orbital mechanics problems naturally lead to **differential equations**.

---

## 1. The Two-Body Problem

For a spacecraft orbiting a central body of mass $M$:

$$
\frac{d^2 \mathbf{r}}{dt^2} = - \frac{\mu}{r^3} \mathbf{r}
$$

Where:

* $\mathbf{r}$ = position vector
* $r = \|\mathbf{r}\|$ = distance to the central body
* $\mu = GM$ = gravitational parameter

This is a **second-order ordinary differential equation (ODE)**.

---

## 2. Converting to First-Order ODEs

Numerical solvers work best with first-order systems. Introduce velocity:

$$
\mathbf{v} = \frac{d\mathbf{r}}{dt}
$$

Then:

$$
\frac{d\mathbf{r}}{dt} = \mathbf{v}, \qquad \frac{d\mathbf{v}}{dt} = -\frac{\mu}{r^3}\mathbf{r}
$$

This formulation is what we implement in code.

---

## 3. Numerical Integration with Python

```python
import numpy as np
from scipy.integrate import solve_ivp
import matplotlib.pyplot as plt

mu = 398600.4418  # Earth's mu in km^3/s^2

def two_body(t, state):
    r = state[:3]
    v = state[3:]
    r_norm = np.linalg.norm(r)
    a = -mu * r / r_norm**3
    return np.hstack((v, a))

# Initial position (km) and velocity (km/s)
r0 = np.array([7000, 0, 0])
v0 = np.array([0, 7.5, 1.0])
state0 = np.hstack((r0, v0))

# Time span (seconds)
t_span = (0, 5400)
t_eval = np.linspace(*t_span, 1000)

# Integrate
sol = solve_ivp(two_body, t_span, state0, t_eval=t_eval, rtol=1e-9)

# Plot trajectory
fig = plt.figure()
ax = fig.add_subplot(111, projection='3d')
ax.plot(sol.y[0], sol.y[1], sol.y[2])
ax.set_xlabel("x [km]")
ax.set_ylabel("y [km]")
ax.set_zlabel("z [km]")
ax.set_title("Two-Body Orbit Propagation")
plt.show()
```

👉 This numerically integrates the orbit and plots it in 3D.

---

## 4. Short Note

* The **two-body ODE** is the cornerstone of orbital mechanics.
* Advanced topics (perturbations, three-body, n-body) are extensions of this framework.
* Numerical integration is the bridge from **theory to real-world trajectories**.

---

## References

* Curtis, H. D., *Orbital Mechanics for Engineering Students*, Ch. 3–4
* Vallado, D. A., *Fundamentals of Astrodynamics and Applications*, Ch. 3
* Wiesel, W. E., *Spaceflight Dynamics*, Ch. 3–4
* Hairer, E., Nørsett, S., & Wanner, G., *Solving Ordinary Differential Equations I*, Springer

