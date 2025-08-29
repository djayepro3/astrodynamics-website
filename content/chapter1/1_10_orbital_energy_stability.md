# Section 10: Orbital Energy and Stability

📂 **File name:** `content/chapter1/1_10_orbital_energy_stability.md`

---

# Orbital Energy and Stability

The motion of a satellite or planet is governed not only by forces but also by the **conservation of energy**. By studying orbital energy, we can understand why orbits are stable, why some objects escape, and why others remain bound to their primary.

---

## 1. Total Specific Orbital Energy

For a two-body system, the total **specific orbital energy** (energy per unit mass) is:

$$
\varepsilon = \frac{v^2}{2} - \frac{\mu}{r}
$$

where:

* $v$ = orbital velocity (m/s)
* $r$ = radial distance from the center of the primary (m)
* $\mu = GM$ = standard gravitational parameter (m$^3$/s$^2$)

👉 This is the sum of **kinetic energy** ($\tfrac{v^2}{2}$) and **gravitational potential energy** ($-\mu/r$).

---

## 2. Orbit Classification by Energy

The sign of $\varepsilon$ determines the orbit type:

* $\varepsilon < 0$: **Bound orbit** (elliptical or circular).
* $\varepsilon = 0$: **Parabolic escape** trajectory (just enough energy to escape).
* $\varepsilon > 0$: **Hyperbolic orbit** (object escapes with excess velocity).

This classification is fundamental in astrodynamics and planetary science.

---

## 3. Energy and Semi-Major Axis

For **elliptical or circular orbits**, the orbital energy is related to the semi-major axis:

$$
\varepsilon = -\frac{\mu}{2a}
$$

* Larger $a$ → higher (less negative) energy → longer orbital period.
* Smaller $a$ → lower (more negative) energy → faster orbit.

This connects **energy, geometry, and motion** seamlessly.

---

## 4. Escape Velocity

Escape velocity is derived by setting $\varepsilon = 0$:

$$
v_\text{esc} = \sqrt{\frac{2\mu}{r}}
$$

Example: For Earth at the surface ($r = R_\oplus$):

$$
v_\text{esc} \approx 11.2 \, \text{km/s}
$$

---

## 5. Stability Considerations

* **Circular orbits** are stable in the absence of perturbations, since velocity and gravitational pull perfectly balance.
* **Elliptical orbits** are also stable but vary in speed due to conservation of angular momentum.
* Perturbations (atmospheric drag, non-spherical gravity, third-body effects, radiation pressure) can slowly shift or destabilize orbits.

---

## 6. Example: Energy of ISS

For the **ISS** ($a \approx 6,780 \, \text{km}$):

$$
\varepsilon = -\frac{3.986 \times 10^{14}}{2 \times 6.78 \times 10^6} \approx -2.94 \times 10^7 \, \text{J/kg}
$$

This negative value confirms the ISS is in a **bound orbit**.

---

## 7. Code Example (Python)

```python
import numpy as np

# Constants
mu_earth = 3.986e14   # m^3/s^2
R_earth = 6378e3      # m
altitude = 402e3      # m
a = R_earth + altitude

# Specific orbital energy
epsilon = -mu_earth / (2 * a)
print(f"Specific orbital energy of ISS: {epsilon:.2e} J/kg")
```

Output:

```
Specific orbital energy of ISS: -2.94e+07 J/kg
```

---

## 8. References

* Vallado, *Fundamentals of Astrodynamics and Applications*, Ch. 1.7
* Curtis, *Orbital Mechanics for Engineering Students*, Ch. 2.7
* Wiesel, *Spaceflight Dynamics*, Ch. 2
* Danby, *Fundamentals of Celestial Mechanics*, Ch. 3
* NASA: [Escape Velocity](https://www.nasa.gov/audience/forstudents/5-8/features/nasa-knows/what-is-escape-velocity-58.html)

---

📂 **File location:**
`content/chapter1/1_10_orbital_energy_stability.md`

---

✅ That’s the **final section of Chapter 1**! 🎉

📖 **Chapter 1 Recap:**

* Newton’s Laws
* Universal Gravitation
* Two-Body Problem
* Equation of Motion
* Energy & Stability

