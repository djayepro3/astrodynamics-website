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

📂 **File name:** `content/chapter1/1_2_two_body_problem.md`

