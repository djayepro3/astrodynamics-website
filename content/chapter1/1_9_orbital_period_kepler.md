# Section 9: Orbital Period and Kepler’s Third Law

📂 **File name:** `content/chapter1/1_9_orbital_period_kepler.md`

---

# Orbital Period and Kepler’s Third Law

The **orbital period $T$** is the time it takes for a satellite or celestial body to complete one revolution around its primary. Johannes Kepler, in 1619, formulated his **Third Law of Planetary Motion**, which connects the period of revolution to the size of the orbit.

---

## 1. Orbital Period Definition

The orbital period is directly tied to the **mean motion $n$**:

$$
n = \sqrt{\frac{\mu}{a^3}}, \quad T = \frac{2\pi}{n}
$$

where:

* $T$ = orbital period (s)
* $n$ = mean motion (rad/s)
* $a$ = semi-major axis (m)
* $\mu = GM$ = gravitational parameter (m$^3$/s$^2$)

Thus,

$$
T = 2\pi \sqrt{\frac{a^3}{\mu}}
$$

---

## 2. Kepler’s Third Law

Kepler’s Third Law states:

> *The square of the orbital period of a planet is directly proportional to the cube of the semi-major axis of its orbit.*

In mathematical form (for orbits around the Sun):

$$
\frac{T^2}{a^3} = \text{constant}
$$

* This constant depends only on the **central body’s mass**, not on the orbiting body.
* Remarkably, it applies to **all planets, moons, and artificial satellites**.

---

## 3. Physical Intuition

* If the orbit is **larger**, gravity is weaker → orbital velocity decreases → orbital period increases.
* If the orbit is **smaller**, gravity is stronger → orbital velocity increases → orbital period decreases.

🔎 **Analogy:** Imagine swinging a ball tied to a string. A shorter string → faster swing; a longer string → slower swing.

---

## 4. Practical Applications

* **Low Earth Orbit (LEO):** \~90 minutes per orbit (e.g., ISS).
* **Geostationary Orbit (GEO):** 24 hours per orbit (synchronous with Earth’s rotation).
* **GPS Satellites (MEO):** \~12 hours per orbit.

---

## 5. Example: ISS Orbital Period

For the **International Space Station (ISS):**

* $a \approx 6,780 \, \text{km}$ (Earth’s radius + altitude)
* $\mu_\oplus = 3.986 \times 10^{14} \, \text{m}^3/\text{s}^2$

$$
T = 2\pi \sqrt{\frac{(6.78 \times 10^6)^3}{3.986 \times 10^{14}}}
$$

$$
T \approx 5,556 \, \text{s} \approx 92.6 \, \text{minutes}
$$

✅ Matches observed orbital period of ISS.

---

## 6. Code Example (Python)

```python
import numpy as np

# Gravitational parameter for Earth
mu_earth = 3.986e14  # m^3/s^2

# Semi-major axis of ISS orbit (Earth radius + altitude)
R_earth = 6378e3  # m
altitude = 402e3  # m
a = R_earth + altitude

# Orbital period
T = 2 * np.pi * np.sqrt(a**3 / mu_earth)
T_minutes = T / 60

print(f"Orbital period of ISS: {T_minutes:.2f} minutes")
```

Output:

```
Orbital period of ISS: ~92.6 minutes
```

---

## 7. References

* Johannes Kepler, *Harmonices Mundi* (1619)
* Vallado, *Fundamentals of Astrodynamics and Applications*, Ch. 1.5
* Curtis, *Orbital Mechanics for Engineering Students*, Ch. 2.6
* NASA Fact Sheet: [ISS Orbit](https://www.nasa.gov/mission_pages/station/overview/index.html)

---

📂 **File location:**
`content/chapter1/1_9_orbital_period_kepler.md`

