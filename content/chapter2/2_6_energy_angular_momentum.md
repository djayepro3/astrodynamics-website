# 2.6 Orbital Energy and Angular Momentum

## 1. Why Are These Quantities Important?

In orbital mechanics, **energy** and **angular momentum** are conserved in the ideal two-body problem (no perturbations).
They determine:

* The **shape** of the orbit (ellipse, parabola, hyperbola)
* The **size** of the orbit (semi-major axis)
* The **orientation** of the orbit in space

---

## 2. Specific Mechanical Energy

The **total specific mechanical energy** (energy per unit mass) is the sum of kinetic and potential energy:

$$
\varepsilon = \frac{v^2}{2} - \frac{\mu}{r}
$$

Where:

* $v = \|\mathbf{v}\|$ = speed
* $r = \|\mathbf{r}\|$ = distance from central body
* $\mu = GM$ = standard gravitational parameter

The **sign of $\varepsilon$** tells the orbit type:

* $\varepsilon < 0$ → Elliptical orbit
* $\varepsilon = 0$ → Parabolic escape trajectory
* $\varepsilon > 0$ → Hyperbolic escape trajectory

---

## 3. Angular Momentum

The **specific angular momentum vector** is:

$$
\mathbf{h} = \mathbf{r} \times \mathbf{v}
$$

* $|\mathbf{h}|$ = magnitude, constant for the two-body problem
* $\mathbf{h}$ points **perpendicular to the orbital plane**

Its magnitude relates to orbital size and eccentricity.

---

## 4. Derivation: Energy–Semi-Major Axis Relation

For elliptical orbits:

$$
\varepsilon = -\frac{\mu}{2a}
$$

Where $a$ = semi-major axis.

This shows **orbital energy depends only on semi-major axis** — not eccentricity.
Thus, all ellipses with the same $a$ have the same total energy.

---

## 5. Python Example: Computing Energy & Angular Momentum

```python
import numpy as np

mu = 398600.4418  # km^3/s^2 (Earth)

# Example state vector
r = np.array([7000, 0, 0])   # km
v = np.array([0, 7.5, 1.0])  # km/s

# Energy
r_norm = np.linalg.norm(r)
v_norm = np.linalg.norm(v)
energy = v_norm**2 / 2 - mu / r_norm

# Angular momentum
h_vec = np.cross(r, v)
h_norm = np.linalg.norm(h_vec)

print("Specific Mechanical Energy [km^2/s^2]:", energy)
print("Specific Angular Momentum Vector [km^2/s]:", h_vec)
print("Magnitude of Angular Momentum [km^2/s]:", h_norm)
```

---

## 6. Short Note

* Energy conservation provides insight into **whether a spacecraft is bound or escaping**.
* Angular momentum conservation ensures that **orbital planes remain fixed** (in the two-body case).
* These invariants make the two-body problem solvable analytically.

---

## References

* Curtis, H. D., *Orbital Mechanics for Engineering Students*, Ch. 3
* Vallado, D. A., *Fundamentals of Astrodynamics and Applications*, Ch. 3
* Battin, R. H., *An Introduction to the Mathematics and Methods of Astrodynamics*
