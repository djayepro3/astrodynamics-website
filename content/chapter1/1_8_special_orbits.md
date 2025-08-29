# Section 8: Special Orbits

📂 **File name:** `content/chapter1/1_8_special_orbits.md`

---

# Special Orbits: Circular, Elliptical, Parabolic, and Hyperbolic

The **eccentricity $e$** of an orbit determines its **shape** and, therefore, its physical meaning. Each type of orbit corresponds to a different **family of conic sections**:

---

## 1. Circular Orbits ($e=0$)

* **Definition:** Path is a perfect circle, radius is constant.
* **Velocity magnitude is constant** at all points.
* Special case of elliptical orbit.

$$
r = a = \text{constant}
$$

* Common for **GPS satellites**, some **low Earth orbits**, and **geostationary satellites**.

🔎 **Intuition:** The satellite’s kinetic and potential energy remain balanced at all points.

---

## 2. Elliptical Orbits ($0 < e <1$)

* **Definition:** Path is an ellipse with the central body at one focus.
* Velocity varies: **fastest at perigee**, **slowest at apogee**.

$$
r(\nu) = \frac{a(1-e^2)}{1 + e \cos \nu}
$$

* Most practical satellite orbits (Earth observation, communication, Molniya).

🔎 **Intuition:** Like stretching a rubber band — the orbit elongates as eccentricity increases.

---

## 3. Parabolic Trajectories ($e=1$)

* **Definition:** Borderline between bound and unbound motion.
* **Specific orbital energy = 0**.

$$
v = v_\text{esc} = \sqrt{\frac{2\mu}{r}}
$$

* Example: A probe launched with exactly escape velocity from Earth.

🔎 **Analogy:** Throwing a ball just fast enough to escape gravity forever, but without excess speed.

---

## 4. Hyperbolic Trajectories ($e>1$)

* **Definition:** Open orbit, object will not return.
* **Specific orbital energy > 0**.
* Describes flybys and interplanetary missions.

$$
r(\nu) = \frac{a(e^2-1)}{1 + e \cos \nu}, \quad a < 0
$$

* Example: Voyager 1 and 2, interstellar-bound spacecraft.

🔎 **Analogy:** Like a slingshot — the spacecraft “borrows” energy from a planet and escapes.

---

## 5. Visualization of Orbits

We can visualize orbit types by plotting the **radial equation** for different eccentricities.

```python
import numpy as np
import matplotlib.pyplot as plt

# Parameters
a = 1.0  # semi-major axis (AU or normalized)
theta = np.linspace(0, 2*np.pi, 500)

eccentricities = [0, 0.5, 0.9, 1.0, 1.2]
labels = ["Circular (e=0)", "Elliptical (e=0.5)", "Elliptical (e=0.9)", 
          "Parabolic (e=1)", "Hyperbolic (e=1.2)"]

plt.figure(figsize=(8,8))

for e, lbl in zip(eccentricities, labels):
    if e < 1:
        r = (a*(1-e**2)) / (1 + e*np.cos(theta))
    else:
        r = (a*(e**2-1)) / (1 + e*np.cos(theta))
    
    x = r*np.cos(theta)
    y = r*np.sin(theta)
    plt.plot(x, y, label=lbl)

plt.scatter([0], [0], color='orange', s=100, label="Central Body")
plt.xlabel("x")
plt.ylabel("y")
plt.title("Orbit Shapes for Different Eccentricities")
plt.axis("equal")
plt.legend()
plt.grid(True)
plt.show()
```

This produces a **2D plot of orbit shapes** with the central body at the focus.

---

## 6. Applications

* **Circular:** Weather satellites (GOES), GNSS.
* **Elliptical:** Molniya orbits (Russia), eccentric communications.
* **Parabolic:** Theoretical, used in escape trajectory calculations.
* **Hyperbolic:** Interplanetary probes, comets, hyperbolic asteroids.

---

## 7. References

* Curtis, *Orbital Mechanics for Engineering Students*, Ch. 2.5
* Vallado, *Fundamentals of Astrodynamics and Applications*, Ch. 1.4
* Bate, Mueller, White, *Fundamentals of Astrodynamics*, Sections 2–3

---

📂 **File location:**
`content/chapter1/1_8_special_orbits.md`
