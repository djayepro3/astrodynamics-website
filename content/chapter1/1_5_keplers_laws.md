# Kepler’s Laws of Planetary Motion

Kepler’s three laws, derived from **empirical observations of Tycho Brahe** and later explained by **Newton’s Law of Gravitation**, are the foundation of orbital mechanics.

We will not only state the laws but also **derive them mathematically** from Newton’s framework.

---

## 1. Kepler’s First Law: Orbits Are Conic Sections

**Statement**:
A planet moves around the Sun in an **ellipse**, with the Sun at one focus.

### Derivation (from Newton’s Laws)

1. Start with **Newton’s Law of Gravitation**:

   $$
   \mathbf{F} = -\frac{GMm}{r^2} \hat{\mathbf{r}}
   $$

2. Apply **Newton’s 2nd Law**:

   $$
   m \ddot{\mathbf{r}} = -\frac{GMm}{r^2} \hat{\mathbf{r}}
   $$

   Cancelling $m$:

   $$
   \ddot{\mathbf{r}} = -\frac{\mu}{r^2} \hat{\mathbf{r}}, \quad \mu = GM
   $$

3. Solve using conservation of angular momentum $\mathbf{h} = \mathbf{r} \times \mathbf{v}$.

   * This confines the orbit to a plane.
   * Introduce polar coordinates $(r, \theta)$.

4. After substitution and rearrangement (Curtis §2.4), we obtain the **orbit equation**:

   $$
   r(\theta) = \frac{p}{1 + e \cos(\theta)}
   $$

   where $p = \frac{h^2}{\mu}$.
   This is the general equation of a **conic section** (ellipse, parabola, hyperbola).

✅ This proves Kepler’s **First Law**.

---

## 2. Kepler’s Second Law: Equal Areas in Equal Times

**Statement**:
A line joining a planet and the Sun sweeps out **equal areas in equal times**.

### Derivation

1. Area swept in a small time $dt$:

   $$
   dA = \frac{1}{2} r^2 d\theta
   $$

2. Divide by $dt$:

   $$
   \frac{dA}{dt} = \frac{1}{2} r^2 \dot{\theta}
   $$

3. But recall from angular momentum:

   $$
   h = r^2 \dot{\theta}
   $$

4. Substituting:

   $$
   \frac{dA}{dt} = \frac{h}{2}
   $$

Since $h$ is **constant**, the **areal velocity is constant**.

✅ This proves Kepler’s **Second Law**.

---

## 3. Kepler’s Third Law: Period–Size Relationship

**Statement**:
The square of the orbital period is proportional to the cube of the semi-major axis:

$$
T^2 \propto a^3
$$

### Derivation

1. For an elliptical orbit, semi-major axis is $a$.
2. The **specific orbital energy** is:

   $$
   \epsilon = -\frac{\mu}{2a}
   $$
3. Relating energy to orbital motion:

   $$
   T = 2\pi \sqrt{\frac{a^3}{\mu}}
   $$

✅ This proves Kepler’s **Third Law**.

---

## 4. Python Visualization: Kepler’s Second Law

We can illustrate **equal areas in equal times**.

```python
import numpy as np
import matplotlib.pyplot as plt

mu = 398600  # km^3/s^2, Earth
a = 10000  # km
e = 0.5  # eccentricity

# Time steps
M = np.linspace(0, 2*np.pi, 200)  # mean anomaly
E = np.zeros_like(M)  # eccentric anomaly

# Solve Kepler's equation iteratively
for i, M_i in enumerate(M):
    E_i = M_i
    for _ in range(10):  # Newton-Raphson
        E_i = E_i - (E_i - e*np.sin(E_i) - M_i) / (1 - e*np.cos(E_i))
    E[i] = E_i

# True anomaly and radius
nu = 2*np.arctan2(np.sqrt(1+e)*np.sin(E/2), np.sqrt(1-e)*np.cos(E/2))
r = a*(1 - e*np.cos(E))

# Cartesian coordinates
x = r*np.cos(nu)
y = r*np.sin(nu)

plt.figure(figsize=(6,6))
plt.plot(x, y, label="Orbit")
plt.scatter([0], [0], color="yellow", s=200, label="Earth")
plt.fill(x[:20], y[:20], alpha=0.3, label="Area swept in equal time")
plt.axis("equal")
plt.legend()
plt.xlabel("X (km)")
plt.ylabel("Y (km)")
plt.title("Kepler's Second Law: Equal Areas in Equal Times")
plt.show()
```

This plot shows the area swept by the planet over equal time intervals.

---

## 5. Why Kepler’s Laws Still Matter

* Foundation for modern orbital mechanics.
* Used in trajectory design (e.g., Mars transfer).
* Basis for **orbital resonance, perturbation analysis, and mission planning**.

---

## 6. References

* Johannes Kepler, *Astronomia Nova* (1609)
* Curtis, *Orbital Mechanics for Engineering Students*, Ch. 2
* Vallado, *Fundamentals of Astrodynamics and Applications*, Ch. 2–3
* NASA, *Basics of Space Flight*

---

📂 **File location:**
`content/chapter1/1_5_keplers_laws.md`

