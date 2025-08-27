# The Two-Body Problem

The **two-body problem** asks:

> *How do two masses move under their mutual gravitational attraction, when no other forces act on them?*

This is the foundation of **orbital mechanics**. Solving it gives us the shape of orbits, their properties, and how spacecraft move around planets.

---

## 1. Setting Up the Problem

We have two masses, $m_1$ and $m_2$, separated by a distance $r = \|\mathbf{r}\|$.
Newton’s law of gravitation gives the force on $m_2$ due to $m_1$:

$$
\mathbf{F}_{12} = - G \frac{m_1 m_2}{r^2} \hat{\mathbf{r}}
$$

By Newton’s 2nd law:

$$
m_1 \ddot{\mathbf{r}}_1 = \mathbf{F}_{21}, \quad m_2 \ddot{\mathbf{r}}_2 = \mathbf{F}_{12}
$$

---

## 2. Relative Motion

Define the **relative position vector**:

$$
\mathbf{r} = \mathbf{r}_2 - \mathbf{r}_1
$$

Differentiating twice:

$$
\ddot{\mathbf{r}} = \ddot{\mathbf{r}}_2 - \ddot{\mathbf{r}}_1
$$

Substitute forces:

$$
\ddot{\mathbf{r}} = - G (m_1 + m_2) \frac{\mathbf{r}}{r^3}
$$

This is the **equation of motion** of the two-body problem. It depends only on the total mass $(m_1 + m_2)$ and the relative vector $\mathbf{r}$.

---

## 3. Reduced Mass and Center of Mass

To simplify, we often use the **reduced mass**:

$$
\mu = \frac{m_1 m_2}{m_1 + m_2}
$$

and the **center of mass (barycenter)**:

$$
\mathbf{R} = \frac{m_1 \mathbf{r}_1 + m_2 \mathbf{r}_2}{m_1 + m_2}
$$

* The barycenter moves in a straight line (or is stationary in an inertial frame).
* The relative motion $\mathbf{r}$ contains all the orbital dynamics.

---

## 4. Conservation Laws

From symmetry, two key conservation laws follow:

* **Conservation of Angular Momentum**

  $$
  \mathbf{h} = \mathbf{r} \times \dot{\mathbf{r}} = \text{constant}
  $$

* **Conservation of Energy**

  $$
  \epsilon = \frac{1}{2} \|\dot{\mathbf{r}}\|^2 - \frac{G (m_1+m_2)}{r} = \text{constant}
  $$

These lead to the conic-section orbits.

---

## 5. Visualizing the Two-Body System

Here’s a minimal interactive Plotly code to illustrate barycenter motion for Earth–Moon:

```python
import plotly.graph_objects as go
import numpy as np

# Parameters
earth_mass = 5.972e24
moon_mass = 7.348e22
distance = 384400  # km

# Barycenter location (from Earth's center)
barycenter = distance * moon_mass / (earth_mass + moon_mass)

fig = go.Figure()

# Earth, Moon, Barycenter
fig.add_trace(go.Scatter(x=[0], y=[0], mode="markers+text",
                         text=["Earth"], textposition="bottom center",
                         marker=dict(size=12, color="blue")))
fig.add_trace(go.Scatter(x=[distance], y=[0], mode="markers+text",
                         text=["Moon"], textposition="bottom center",
                         marker=dict(size=8, color="gray")))
fig.add_trace(go.Scatter(x=[barycenter], y=[0], mode="markers+text",
                         text=["Barycenter"], textposition="top center",
                         marker=dict(size=6, color="red")))

fig.update_layout(title="Earth–Moon Two-Body System",
                  xaxis_title="x (km)", yaxis_title="y (km)",
                  yaxis=dict(scaleanchor="x", scaleratio=1))
fig.show()
```

👉 You can embed a static image of this figure in your `.md` file and link the interactive code in the GitHub repo.

---

## 6. References

* Curtis, H. D. *Orbital Mechanics for Engineering Students*, Ch. 2
* Vallado, D. A. *Fundamentals of Astrodynamics and Applications*, Ch. 2
* Wiesel, W. E. *Spaceflight Dynamics*, Ch. 2
* Goldstein, H. *Classical Mechanics* (3rd ed.), Sec. 3.4 – Two-body problem
* Danby, J. M. A. *Fundamentals of Celestial Mechanics* (2nd ed.)
* Szebehely, V. *Theory of Orbits: The Restricted Problem of Three Bodies* (1967)

---

📂 **File name suggestion:** `content/chapter1/1_2_two_body_problem.md`

---

Do you want me to continue the flow with **Section 3: Conic Orbits (Ellipses, Parabolas, Hyperbolas)**, which naturally follows from conservation of energy & angular momentum?


Perfect 👍 — the next natural step is indeed **Section 3: Conic Orbits (Ellipses, Parabolas, Hyperbolas)**.

I’ll draft it as `content/chapter1/1_3_conic_orbits.md`.

---

# Conic Orbits: Ellipses, Parabolas, Hyperbolas

From Newton’s laws, the two-body problem admits a beautiful result:

> The path of one body relative to the other is always a **conic section** — an ellipse, parabola, or hyperbola — with the more massive body at one focus.

---

## 1. Conservation Principles → Orbit Shape

* **Angular momentum conservation** makes the orbit **planar** (motion lies in a fixed plane).
* **Energy conservation** determines the *type* of conic section.

The **specific orbital energy** is:

$$
\epsilon = \frac{v^2}{2} - \frac{\mu}{r}, \quad \mu = G (m_1 + m_2)
$$

| Orbit Type | Energy $\epsilon$ | Eccentricity $e$ | Shape                   |
| ---------- | ----------------- | ---------------- | ----------------------- |
| Ellipse    | $\epsilon < 0$    | $0 \leq e < 1$   | Closed, bound orbit     |
| Parabola   | $\epsilon = 0$    | $e = 1$          | Open, escape trajectory |
| Hyperbola  | $\epsilon > 0$    | $e > 1$          | Open, flyby trajectory  |

---

## 2. Polar Equation of a Conic

In the orbital plane, using polar coordinates $(r, \theta)$:

$$
r(\theta) = \frac{h^2 / \mu}{1 + e \cos \theta}
$$

where:

* $h = \|\mathbf{r} \times \mathbf{v}\|$ = specific angular momentum
* $e$ = eccentricity
* $\theta$ = true anomaly (angle from periapsis)

👉 This is the **orbit equation** in closed form.

---

## 3. Elliptical Orbits (Bound Motion)

* $0 \leq e < 1$
* Periapsis (closest point):

  $$
  r_p = a(1-e)
  $$
* Apoapsis (farthest point):

  $$
  r_a = a(1+e)
  $$
* Semi-major axis:

  $$
  a = \frac{r_p + r_a}{2}
  $$

The orbital period follows **Kepler’s 3rd Law**:

$$
T = 2\pi \sqrt{\frac{a^3}{\mu}}
$$

---

## 4. Parabolic Orbits (Escape)

* $e = 1$, $\epsilon = 0$
* Just enough energy to escape the central body.
* Useful as an idealization for **minimum-energy escape trajectories**.

---

## 5. Hyperbolic Orbits (Flybys)

* $e > 1$, $\epsilon > 0$
* Spacecraft entering planetary systems on **interplanetary transfers** follow hyperbolas.
* Characterized by the **hyperbolic excess velocity**:

  $$
  v_\infty = \lim_{r \to \infty} v(r)
  $$

---

## 6. Visualization: Conics in Python

```python
import numpy as np
import matplotlib.pyplot as plt

mu = 398600  # km^3/s^2 (Earth)
h = 60000    # specific angular momentum

# Different eccentricities
eccs = [0.3, 1.0, 1.5]
labels = ["Ellipse (e=0.3)", "Parabola (e=1)", "Hyperbola (e=1.5)"]

theta = np.linspace(-np.pi, np.pi, 1000)

plt.figure(figsize=(6,6))
for e, label in zip(eccs, labels):
    r = h**2/mu/(1 + e*np.cos(theta))
    plt.plot(r*np.cos(theta), r*np.sin(theta), label=label)

plt.scatter(0,0,color="red",label="Focus (Earth)")
plt.xlabel("x (km)")
plt.ylabel("y (km)")
plt.axis("equal")
plt.legend()
plt.title("Conic Section Orbits")
plt.show()
```

* Produces ellipse, parabola, and hyperbola in one plot.
* The red dot = central body at the focus.

---

## 7. References

* Curtis, *Orbital Mechanics for Engineering Students*, Ch. 2–3
* Vallado, *Fundamentals of Astrodynamics and Applications*, Ch. 2
* Bate, Mueller, White, *Fundamentals of Astrodynamics*, Ch. 2
* Roy, *Orbital Motion*, Ch. 2
* NASA JPL, *Basics of Space Flight*

---

📂 **File name:** `content/chapter1/1_3_conic_orbits.md`


