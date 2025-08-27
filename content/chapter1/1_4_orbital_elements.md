# Orbital Elements (Keplerian Elements)

So far, we know that any two-body orbit is a **conic section**. But to uniquely describe *which* orbit an object is on, we need **six orbital elements**.

These are called the **classical Keplerian elements (COEs)**.

---

## 1. Why Six Elements?

The motion of a body in 3D requires:

* **3 position components** $(x,y,z)$
* **3 velocity components** $(v_x,v_y,v_z)$

\= 6 independent quantities.
Instead of Cartesian coordinates, orbital mechanics uses six **geometrical + dynamical parameters**.

---

## 2. The Six Classical Orbital Elements

1. **Semi-major axis $a$**

   * Defines the size of the orbit.
   * Related to orbital energy:

     $$
     a = -\frac{\mu}{2\epsilon}, \quad \epsilon = \frac{v^2}{2} - \frac{\mu}{r}
     $$

2. **Eccentricity $e$**

   * Defines the shape (circle, ellipse, parabola, hyperbola).
   * Vector form:

     $$
     \mathbf{e} = \frac{1}{\mu} \left( \mathbf{v} \times \mathbf{h} - \mu \frac{\mathbf{r}}{r} \right)
     $$

     where $\mathbf{h} = \mathbf{r} \times \mathbf{v}$.

3. **Inclination $i$**

   * Tilt of the orbital plane w\.r.t. the equatorial plane.
   * Range: $0^\circ \leq i \leq 180^\circ$.

4. **Right Ascension of the Ascending Node (RAAN, $\Omega$)**

   * Angle in the equatorial plane from the reference direction (vernal equinox) to the **ascending node** (where the orbit crosses northward).

5. **Argument of Periapsis ($\omega$)**

   * Angle within the orbital plane from ascending node to periapsis.

6. **True Anomaly ($\nu$)**

   * Position of the body along its orbit, measured from periapsis at a given time.

---

## 3. Geometry of the Elements

📌 Think of it in **three rotations**:

1. Rotate by $\Omega$ around the z-axis → sets the **line of nodes**.
2. Rotate by $i$ around the node line → tilts the orbital plane.
3. Rotate by $\omega$ inside the plane → places periapsis.
   Then, $\nu$ gives the current location of the spacecraft.

---

## 4. Visual Aid

Here’s a static diagram you can embed:

![Orbital Elements Diagram](https://upload.wikimedia.org/wikipedia/commons/2/27/Orbital_elements.svg)

---

## 5. Python Visualization of Orbital Plane

```python
import numpy as np
import matplotlib.pyplot as plt

# Orbital elements (example)
a = 10000  # km
e = 0.4
i = np.radians(45)  # inclination
Omega = np.radians(60)  # RAAN
omega = np.radians(30)  # argument of periapsis

# True anomaly range
nu = np.linspace(0, 2*np.pi, 500)
r = a*(1-e**2)/(1+e*np.cos(nu))

# Orbit in perifocal coordinates
x_p = r*np.cos(nu)
y_p = r*np.sin(nu)
z_p = np.zeros_like(nu)

# Rotation matrices
R3_Omega = np.array([[np.cos(Omega), -np.sin(Omega), 0],
                     [np.sin(Omega),  np.cos(Omega), 0],
                     [0, 0, 1]])
R1_i = np.array([[1, 0, 0],
                 [0, np.cos(i), -np.sin(i)],
                 [0, np.sin(i),  np.cos(i)]])
R3_omega = np.array([[np.cos(omega), -np.sin(omega), 0],
                     [np.sin(omega),  np.cos(omega), 0],
                     [0, 0, 1]])

Q = R3_Omega @ R1_i @ R3_omega

coords = Q @ np.vstack((x_p, y_p, z_p))

fig = plt.figure(figsize=(7,7))
ax = fig.add_subplot(111, projection='3d')
ax.plot(coords[0], coords[1], coords[2], label="Orbit")
ax.scatter(0,0,0, color="yellow", s=100, label="Earth")
ax.set_xlabel("X (km)")
ax.set_ylabel("Y (km)")
ax.set_zlabel("Z (km)")
ax.legend()
plt.show()
```

This code rotates an ellipse into 3D space based on orbital elements.

---

## 6. Why COEs Matter

* Intuitive geometric meaning.
* Compact representation (6 values vs. 6 Cartesian components).
* Essential for mission design, satellite catalogs, and TLE (Two-Line Elements).

---

## 7. References

* Curtis, *Orbital Mechanics for Engineering Students*, Ch. 4
* Vallado, *Fundamentals of Astrodynamics and Applications*, Ch. 2
* Bate, Mueller, White, *Fundamentals of Astrodynamics*, Ch. 2–3
* NASA Goddard, *Basics of Space Flight*

---

📂 **File name:** `content/chapter1/1_4_orbital_elements.md`

