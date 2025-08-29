# 📖 Chapter 2.1 — Vectors and Coordinate Systems

## 🌍 Why Vectors in Astrodynamics?

Astrodynamics is the science of motion in three-dimensional space. To describe the **position, velocity, and acceleration** of spacecraft or celestial bodies, we rely on **vectors**.

A vector is simply a **quantity with both magnitude and direction**. While scalars (like mass, time, or temperature) only tell us "how much," vectors also tell us "which way."

---

## 🧮 Basic Definitions

* **Vector Notation:**
  A vector **r** can be written as:

  $$
  \mathbf{r} = x \hat{\mathbf{i}} + y \hat{\mathbf{j}} + z \hat{\mathbf{k}}
  $$

  where:

  * $x, y, z$ are components in the Cartesian coordinate system
  * $\hat{\mathbf{i}}, \hat{\mathbf{j}}, \hat{\mathbf{k}}$ are unit vectors along the axes

* **Magnitude of a Vector:**

  $$
  |\mathbf{r}| = \sqrt{x^2 + y^2 + z^2}
  $$

* **Unit Vector (Direction only):**

  $$
  \hat{\mathbf{r}} = \frac{\mathbf{r}}{|\mathbf{r}|}
  $$

---

## ⚙️ Vector Operations

1. **Dot Product (Scalar Product):**

   $$
   \mathbf{a} \cdot \mathbf{b} = |\mathbf{a}| |\mathbf{b}| \cos\theta
   $$

   Physical meaning: Projection of one vector onto another.

   * Example: Work = Force $\cdot$ displacement

2. **Cross Product (Vector Product):**

   $$
   \mathbf{a} \times \mathbf{b} = |\mathbf{a}| |\mathbf{b}| \sin\theta \, \hat{\mathbf{n}}
   $$

   * Direction given by the **right-hand rule**
   * Example in astrodynamics: Angular momentum vector $\mathbf{h} = \mathbf{r} \times \mathbf{v}$

---

## 📐 Coordinate Systems

In astrodynamics, we often switch between coordinate systems.

1. **Cartesian (x, y, z):**

   * Useful for numerical computations
   * Natural for Newton’s laws

2. **Polar (r, θ) in 2D / Spherical (r, θ, φ) in 3D:**

   * More natural for orbits
   * Position in 3D:

   $$
   \mathbf{r} = r \sin\theta \cos\phi \, \hat{\mathbf{i}} + r \sin\theta \sin\phi \, \hat{\mathbf{j}} + r \cos\theta \, \hat{\mathbf{k}}
   $$

3. **Inertial vs Rotating Frames:**

   * **Inertial frame:** Fixed relative to the stars (non-accelerating).
   * **Rotating frame:** Earth-centered rotating with Earth (useful for launch problems, satellite ground tracks).

---

## 🎨 Visualization (3D Interactive Plot)

Let’s make an **interactive 3D vector visualization** in Python (using Plotly):

```python
import plotly.graph_objects as go
import numpy as np

# Define vectors
r = np.array([2, 3, 1])   # position vector
v = np.array([-1, 2, 0])  # velocity vector

# Create 3D figure
fig = go.Figure()

# Add position vector
fig.add_trace(go.Cone(
    x=[0], y=[0], z=[0],
    u=[r[0]], v=[r[1]], w=[r[2]],
    colorscale="Blues", sizemode="absolute", sizeref=0.5, name="r"
))

# Add velocity vector
fig.add_trace(go.Cone(
    x=[0], y=[0], z=[0],
    u=[v[0]], v=[v[1]], w=[v[2]],
    colorscale="Reds", sizemode="absolute", sizeref=0.5, name="v"
))

# Layout
fig.update_layout(
    scene=dict(
        xaxis=dict(range=[-3, 3]),
        yaxis=dict(range=[-3, 3]),
        zaxis=dict(range=[-3, 3])
    ),
    title="3D Vectors: Position (blue) & Velocity (red)"
)

fig.show()
```

This plot shows the **position vector** $\mathbf{r}$ (blue) and **velocity vector** $\mathbf{v}$ (red) in 3D space.
Users can rotate with their mouse to build intuition.

---

## ✅ Practical Exercise

* Define three different position vectors for a satellite.
* Compute:

  1. Their magnitudes.
  2. The angle between two vectors using the **dot product**.
  3. The orbital angular momentum $\mathbf{h} = \mathbf{r} \times \mathbf{v}$.

Try coding this in Python!

---

## 📚 References

* Curtis, H. D. *Orbital Mechanics for Engineering Students* (Ch. 1.3–1.4)
* Vallado, D. A. *Fundamentals of Astrodynamics and Applications* (Ch. 1.2)
* Wiesel, W. E. *Spaceflight Dynamics* (Ch. 3)
* Goldstein, H. *Classical Mechanics* (for vector calculus background)

