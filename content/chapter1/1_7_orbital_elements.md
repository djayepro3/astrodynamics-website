# Section 7: Orbital Elements

📂 **File name:** `content/chapter1/1_7_orbital_elements.md`

---

# Orbital Elements (Classical Orbital Elements)

To fully describe the position and motion of a satellite in space, we use a set of **six parameters** called the **Classical Orbital Elements (COEs)**. These elements uniquely define an orbit in 3D space relative to a central body.

---

## 1. Why Orbital Elements?

* Position vector $\vec{r}$ and velocity vector $\vec{v}$ at a single instant describe a satellite’s **state**.
* However, orbital elements give us a more **intuitive, geometrical description** of the orbit: shape, size, and orientation.
* Used widely in **astronomy**, **mission planning**, and **satellite tracking**.

---

## 2. The Six Classical Orbital Elements

1. **Semi-major axis ($a$)**

   * Defines the **size** of the orbit.
   * For elliptical orbits: half the longest diameter.
   * Linked to orbital energy.

2. **Eccentricity ($e$)**

   * Defines the **shape** of the orbit.
   * $e=0$: circle, $0<e<1$: ellipse, $e=1$: parabola, $e>1$: hyperbola.

3. **Inclination ($i$)**

   * Tilt of the orbit relative to the equatorial plane of the central body.
   * $i=0^\circ$: equatorial orbit, $i=90^\circ$: polar orbit.

4. **Right Ascension of the Ascending Node (RAAN, $\Omega$)**

   * Defines where the orbit crosses the equatorial plane going north.
   * Measured from the **vernal equinox direction**.

5. **Argument of Perigee ($\omega$)**

   * Defines the orientation of the ellipse within the orbital plane.
   * Angle from ascending node to perigee.

6. **True Anomaly ($\nu$)**

   * Position of the satellite along the orbit at a given time.
   * Angle from perigee to satellite’s position vector.

---

## 3. Visualization of Orbital Elements

🖼️ (We should include a **diagram** here: a 3D sketch of an orbit showing inclination, RAAN, argument of perigee, and true anomaly.)

👉 I suggest we use **Plotly** or **Matplotlib + mpl\_toolkits** for a **3D orbit visualization** that can be embedded interactively.

---

## 4. Example: ISS Orbit

* Semi-major axis: \~6780 km
* Eccentricity: \~0.0007 (almost circular)
* Inclination: \~51.6°
* RAAN: varies due to precession
* Argument of perigee: not meaningful (for circular orbit)
* True anomaly: varies with time

---

## 5. Python Example: Convert State Vectors to Orbital Elements

```python
import numpy as np

mu = 398600  # km^3/s^2 (Earth)

def state_to_coe(r_vec, v_vec, mu):
    r = np.linalg.norm(r_vec)
    v = np.linalg.norm(v_vec)

    # Specific angular momentum
    h_vec = np.cross(r_vec, v_vec)
    h = np.linalg.norm(h_vec)

    # Eccentricity vector
    e_vec = (1/mu)*((v**2 - mu/r)*r_vec - np.dot(r_vec, v_vec)*v_vec)
    e = np.linalg.norm(e_vec)

    # Semi-major axis
    a = 1 / (2/r - v**2/mu)

    return a, e

# Example: satellite position and velocity
r_vec = np.array([7000, 0, 0])  # km
v_vec = np.array([0, 7.5, 1])   # km/s

a, e = state_to_coe(r_vec, v_vec, mu)
print(f"Semi-major axis: {a:.2f} km, Eccentricity: {e:.4f}")
```

---

## 6. Why Orbital Elements Matter

* Used to track and predict satellite positions.
* Keplerian elements published by agencies (e.g., NASA TLEs) follow this framework.
* Provides intuitive understanding of orbit orientation and shape.

---

## 7. References

* Curtis, *Orbital Mechanics for Engineering Students*, Ch. 4
* Vallado, *Fundamentals of Astrodynamics and Applications*, Ch. 2
* NASA JPL HORIZONS Ephemeris System
* Bate, Mueller, White, *Fundamentals of Astrodynamics*

---

📂 **File location:**
`content/chapter1/1_7_orbital_elements.md`
