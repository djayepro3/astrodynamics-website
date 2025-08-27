# Newton’s Laws and Universal Gravitation

Astrodynamics begins with **first principles**: how forces cause motion. In this section, we’ll build from Newton’s laws to the law of universal gravitation — the foundation of orbital mechanics.

---

## 1. Newton’s Laws of Motion

**First Law (Law of Inertia):**
An object remains at rest, or moves in a straight line at constant speed, unless acted upon by a net external force.

$$
\mathbf{F}_{\text{net}} = 0 \quad \Rightarrow \quad \mathbf{a} = 0
$$

**Second Law (Force and Acceleration):**
The acceleration of a body is proportional to the net force acting on it and inversely proportional to its mass.

$$
\mathbf{F} = m \mathbf{a}
$$

This is the *engine* of dynamics: forces cause accelerations.

**Third Law (Action–Reaction):**
For every action, there is an equal and opposite reaction.

$$
\mathbf{F}_{12} = - \mathbf{F}_{21}
$$

This reciprocity ensures conservation of momentum in isolated systems.

---

## 2. Newton’s Law of Universal Gravitation

In 1687, Newton proposed that the same force that pulls apples to the ground also governs the motion of the Moon and planets:

$$
\mathbf{F}_{12} = -G \frac{m_1 m_2}{r^2} \hat{\mathbf{r}}
$$

where:

* $G$ is the universal gravitational constant $(6.67430 \times 10^{-11}\, \text{N·m}^2/\text{kg}^2)$
* $m_1, m_2$ are the two masses
* $r$ is the distance between them
* $\hat{\mathbf{r}}$ is the unit vector from one mass to the other

This central, attractive force is the cornerstone of **orbital motion**.

---

## 3. Combining Newton’s Laws

Applying Newton’s 2nd law to the gravitational force gives the **equation of motion** for two bodies:

$$
m \mathbf{a} = - G \frac{M m}{r^2} \hat{\mathbf{r}}
$$

Cancel $m$ (the test body’s mass):

$$
\mathbf{a} = - G \frac{M}{r^2} \hat{\mathbf{r}}
$$

👉 This tells us: **all objects, regardless of their mass, experience the same gravitational acceleration** — as Galileo suspected, and Newton proved.

---

## 4. Visualization: Earth–Moon Gravitational Interaction

Below is a simple Python/Plotly snippet (linked in your code repo) that visualizes the gravitational attraction between Earth and Moon:

```python
import plotly.graph_objects as go
import numpy as np

# Earth and Moon positions
earth = np.array([0,0,0])
moon = np.array([384400,0,0])  # km

# Create 3D scatter
fig = go.Figure()

fig.add_trace(go.Scatter3d(x=[earth[0]], y=[earth[1]], z=[earth[2]],
                           mode='markers+text',
                           text=['Earth'], textposition="top center",
                           marker=dict(size=10, color='blue')))

fig.add_trace(go.Scatter3d(x=[moon[0]], y=[moon[1]], z=[moon[2]],
                           mode='markers+text',
                           text=['Moon'], textposition="top center",
                           marker=dict(size=5, color='gray')))

# Add vector arrow Earth->Moon
fig.add_trace(go.Cone(x=[moon[0]], y=[moon[1]], z=[moon[2]],
                      u=[-1], v=[0], w=[0],
                      sizemode="absolute", sizeref=20000,
                      colorscale="Viridis"))

fig.update_layout(scene=dict(
    xaxis_title="x (km)",
    yaxis_title="y (km)",
    zaxis_title="z (km)"),
    title="Earth–Moon Gravitational Force Vector")

fig.show()
```

* The arrow points from Moon to Earth, showing the **force vector**.
* Users can rotate the 3D view interactively when run in Binder/Colab.
* On your site, you can embed the **static preview** (e.g., PNG or GIF) while linking to interactive code.

---

## 5. References

* Newton, I. *Philosophiæ Naturalis Principia Mathematica* (1687).
* Curtis, H. D. *Orbital Mechanics for Engineering Students* (4th ed., 2020).
* Vallado, D. A. *Fundamentals of Astrodynamics and Applications* (4th ed., 2013).
* Wiesel, W. E. *Spaceflight Dynamics* (2nd ed., 1997).
* NASA. *Basics of Space Flight: Orbital Mechanics* (JPL Publication).

---

📂 **File name:** `content/chapter1/1_1_newtons_laws.md`

---


