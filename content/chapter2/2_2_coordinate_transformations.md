# 🔁 Chapter 2.2 — Coordinate Transformations

📂 **File:** `content/chapter2/2_2_coordinate_transformations.md`

## Why transforms?

We constantly change frames (perifocal ↔ ECI/ECEF, inertial ↔ body). Doing this cleanly requires **rotation matrices** and **direction cosine matrices (DCMs)**.

---

## 1 Elementary rotation matrices (right-hand rule)

* Rotate by angle $\alpha$ about **x**:

$$
R_x(\alpha)=\begin{bmatrix}
1&0&0\\
0&\cos\alpha&-\sin\alpha\\
0&\sin\alpha&\cos\alpha
\end{bmatrix}
$$

* About **y**:

$$
R_y(\beta)=\begin{bmatrix}
\cos\beta&0&\sin\beta\\
0&1&0\\
-\sin\beta&0&\cos\beta
\end{bmatrix}
$$

* About **z**:

$$
R_z(\gamma)=\begin{bmatrix}
\cos\gamma&-\sin\gamma&0\\
\sin\gamma&\cos\gamma&0\\
0&0&1
\end{bmatrix}
$$

**Properties (DCM/rotation matrix $C$)**

* Orthonormal columns/rows, $C^\top C = I$
* $\det C = +1$
* $C^{-1} = C^\top$

---

## 2 Euler angle sequences and DCMs

Common aerospace convention: **3–2–1** (yaw–pitch–roll):

$$
C_{B\leftarrow I} = R_x(\phi)\,R_y(\theta)\,R_z(\psi)
$$

This maps a vector in the **inertial** frame $I$ into the **body** frame $B$:

$$
\mathbf{v}_B = C_{B\leftarrow I}\,\mathbf{v}_I
$$

> ⚠️ Be explicit about the **order** and the **from/to** direction; many texts use opposite multiplication order. We’ll state it at the top of each section to avoid ambiguity.

---

## 3 Perifocal ↔ ECI (very common in orbits)

Given orbital elements $(\Omega, i, \omega)$, the transform from **perifocal** $\mathcal{P}$ to **ECI** $\mathcal{I}$ is:

$$
C_{\mathcal{I}\leftarrow \mathcal{P}} = R_z(\Omega)\,R_x(i)\,R_z(\omega)
$$

Thus

$$
\mathbf{r}_{\mathcal{I}} = C_{\mathcal{I}\leftarrow \mathcal{P}}\,\mathbf{r}_{\mathcal{P}},\quad
\mathbf{v}_{\mathcal{I}} = C_{\mathcal{I}\leftarrow \mathcal{P}}\,\mathbf{v}_{\mathcal{P}}
$$

---

## 4 Worked example (numbers)

Let $\Omega=60^\circ,\, i=45^\circ,\, \omega=30^\circ$. A point in perifocal:

$$
\mathbf{r}_{\mathcal{P}} = [8000,\ 2000,\ 0]\ \text{km}
$$

Compute $\mathbf{r}_{\mathcal{I}}$.

```python
import numpy as np

def Rx(a):
    c,s = np.cos(a), np.sin(a)
    return np.array([[1,0,0],[0,c,-s],[0,s,c]])

def Ry(a):
    c,s = np.cos(a), np.sin(a)
    return np.array([[c,0,s],[0,1,0],[-s,0,c]])

def Rz(a):
    c,s = np.cos(a), np.sin(a)
    return np.array([[c,-s,0],[s,c,0],[0,0,1]])

Omega = np.radians(60.0)
inc   = np.radians(45.0)
omega = np.radians(30.0)

C_I_P = Rz(Omega) @ Rx(inc) @ Rz(omega)

r_P = np.array([8000., 2000., 0.])  # km
r_I = C_I_P @ r_P

print("C_I<-P =\n", C_I_P)
print("r_I =", r_I, "km")
# sanity checks
orthonorm = np.allclose(C_I_P.T @ C_I_P, np.eye(3), atol=1e-12)
det_one   = np.isclose(np.linalg.det(C_I_P), 1.0, atol=1e-12)
print("Orthonormal?", orthonorm, " det≈1?", det_one)
```

---

## 5 Visual aid (optional static + interactive)

* **Static**: export a PNG of axes before/after rotation.
* **Interactive**: small Plotly scene that draws original axes and rotated axes (users can rotate with mouse).

```python
import plotly.graph_objects as go

axes_len = 1.0
I = np.eye(3)
B = C_I_P @ I

fig = go.Figure()

# inertial axes
fig.add_trace(go.Scatter3d(x=[0,axes_len], y=[0,0], z=[0,0], mode="lines+text", text=["","Ix"]))
fig.add_trace(go.Scatter3d(x=[0,0], y=[0,axes_len], z=[0,0], mode="lines+text", text=["","Iy"]))
fig.add_trace(go.Scatter3d(x=[0,0], y=[0,0], z=[0,axes_len], mode="lines+text", text=["","Iz"]))

# rotated/body axes
fig.add_trace(go.Scatter3d(x=[0,B[0,0]], y=[0,B[1,0]], z=[0,B[2,0]], mode="lines+text", text=["","Bx"]))
fig.add_trace(go.Scatter3d(x=[0,B[0,1]], y=[0,B[1,1]], z=[0,B[2,1]], mode="lines+text", text=["","By"]))
fig.add_trace(go.Scatter3d(x=[0,B[0,2]], y=[0,B[1,2]], z=[0,B[2,2]], mode="lines+text", text=["","Bz"]))

fig.update_layout(title="Inertial (I) vs Rotated (B) Axes", scene_aspectmode="cube")
fig.show()
```

On the site, include a **static snapshot**; link to the notebook for interactivity.

---

## 6 Pitfalls & best practices

* **Gimbal lock**: certain Euler sequences lose a degree of freedom when a middle angle hits $\pm 90^\circ$.
* **Always document** angle order and frame direction (e.g., “ECI ← Perifocal”).
* **Use quaternions** for robust chaining of rotations (we’ll introduce them later in attitude dynamics).

---

## 7 Quick utilities you’ll reuse

📦 Put this in your code repo (e.g., `astrodyn_math/rotations.py`) and import where needed.

```python
import numpy as np

def Rx(a): 
    c,s = np.cos(a), np.sin(a)
    return np.array([[1,0,0],[0,c,-s],[0,s,c]])

def Ry(a): 
    c,s = np.cos(a), np.sin(a)
    return np.array([[c,0,s],[0,1,0],[-s,0,c]])

def Rz(a): 
    c,s = np.cos(a), np.sin(a)
    return np.array([[c,-s,0],[s,c,0],[0,0,1]])

def is_rotation(C, atol=1e-10):
    return np.allclose(C.T @ C, np.eye(3), atol=atol) and np.isclose(np.linalg.det(C), 1.0, atol=atol)
```

---

## References

* Vallado, **§2.2** (Frames, rotation sequences, DCMs)
* Curtis, **App. A / §4** (Perifocal–ECI transforms)
* Wiesel, **Ch. 3** (Rigid rotations, Euler angles)

