Awesome — here are the **exercise solutions for 2.1** first, then we jump into **Section 2.2**.

---

# ✅ Chapter 2.1 — Exercise Solutions

📂 **File:** `content/chapter2/2_1_exercises.md`

## Goal

Practice vector basics used throughout astrodynamics: magnitudes, angles, projections, and angular momentum $\mathbf{h} = \mathbf{r} \times \mathbf{v}$.

---

## 1 Magnitudes of three position vectors

Given (examples you can edit):

* $\mathbf{r}_1 = [7000,\  -1210,\ 1300]\ \text{km}$
* $\mathbf{r}_2 = [   0,\   6800,\  100]\ \text{km}$
* $\mathbf{r}_3 = [-4210,\  4100,\ 5200]\ \text{km}$

```python
import numpy as np

r1 = np.array([7000., -1210., 1300.])
r2 = np.array([   0.,  6800.,  100.])
r3 = np.array([-4210., 4100., 5200.])

def mag(v): return np.linalg.norm(v)

for k, r in enumerate([r1, r2, r3], start=1):
    print(f"|r{k}| = {mag(r):.3f} km")
```

---

## 2 Angle between two vectors via dot product

$$
\cos\theta = \frac{\mathbf{a}\cdot\mathbf{b}}{\|\mathbf{a}\|\ \|\mathbf{b}\|}
$$

```python
def angle_deg(a, b):
    num = np.dot(a, b)
    den = np.linalg.norm(a) * np.linalg.norm(b)
    # numerical safety
    c = np.clip(num / den, -1.0, 1.0)
    return np.degrees(np.arccos(c))

theta12 = angle_deg(r1, r2)
print(f"Angle(r1,r2) = {theta12:.3f} deg")
```

---

## 3 Orbital angular momentum $\mathbf{h} = \mathbf{r} \times \mathbf{v}$

Take a sample state (edit as needed):

* $\mathbf{r} = [7000,\, 0,\, 0]\ \text{km}$
* $\mathbf{v} = [0,\, 7.5,\, 1.0]\ \text{km/s}$

```python
r = np.array([7000., 0., 0.])     # km
v = np.array([0., 7.5, 1.0])      # km/s
h = np.cross(r, v)                 # km^2/s
h_mag = np.linalg.norm(h)

print("h =", h, "km^2/s")
print("|h| =", h_mag, "km^2/s")
```

**Sanity check:** $|\mathbf{h}| = |\mathbf{r}|\,|\mathbf{v}|\,\sin\phi$, with $\phi$ the angle between $\mathbf{r}$ and $\mathbf{v}$.

```python
phi = angle_deg(r, v)
h_check = np.linalg.norm(r) * np.linalg.norm(v) * np.sin(np.radians(phi))
print(f"|h| (via formula) = {h_check:.6f} km^2/s")
```

---

## 4 Projections (handy for flight-path angle later)

Projection of $\mathbf{v}$ onto $\hat{\mathbf{r}}$:

$$
\mathrm{proj}_{\hat{\mathbf{r}}}(\mathbf{v}) = (\mathbf{v}\cdot\hat{\mathbf{r}})\,\hat{\mathbf{r}}
$$

```python
rhat = r / np.linalg.norm(r)
v_radial_scalar = np.dot(v, rhat)
v_radial_vec = v_radial_scalar * rhat
v_transverse_vec = v - v_radial_vec

print("v_radial (scalar):", v_radial_scalar, "km/s")
print("v_transverse |.| :", np.linalg.norm(v_transverse_vec), "km/s")
```

---

## 5 Bonus checks you can try

* Verify $\mathbf{r}\cdot(\mathbf{r}\times\mathbf{v}) = 0$ (triple product orthogonality).
* Compute unit vectors $\hat{\mathbf{i}}_r, \hat{\boldsymbol{\theta}}, \hat{\mathbf{k}}_h$ using $\mathbf{r}, \mathbf{v}, \mathbf{h}$:

  * $\hat{\mathbf{i}}_r = \mathbf{r}/r$
  * $\hat{\mathbf{k}}_h = \mathbf{h}/h$
  * $\hat{\boldsymbol{\theta}} = \hat{\mathbf{k}}_h \times \hat{\mathbf{i}}_r$

---

## References

Curtis §1.3–1.4; Vallado §1.2; Goldstein *Classical Mechanics* (vector prelims).


