# 2.3 Calculus Refresher

📂 **File name:** `content/chapter2/2_3_calculus_refresher.md`

---

## Why Calculus in Astrodynamics?

In astrodynamics, **position, velocity, and acceleration** are all functions of time. Calculus allows us to:

* Compute **velocity** as the derivative of position: $\mathbf{v} = d\mathbf{r}/dt$
* Compute **acceleration** as the derivative of velocity: $\mathbf{a} = d\mathbf{v}/dt = d^2\mathbf{r}/dt^2$
* Analyze **orbital changes** and perturbations using differential equations

---

## 1. Derivatives of Vectors

For a vector $\mathbf{r}(t) = x(t)\hat{\mathbf{i}} + y(t)\hat{\mathbf{j}} + z(t)\hat{\mathbf{k}}$:

$$
\frac{d\mathbf{r}}{dt} = \frac{dx}{dt}\hat{\mathbf{i}} + \frac{dy}{dt}\hat{\mathbf{j}} + \frac{dz}{dt}\hat{\mathbf{k}} = \mathbf{v}(t)
$$

$$
\frac{d^2\mathbf{r}}{dt^2} = \frac{d\mathbf{v}}{dt} = \mathbf{a}(t)
$$

> **Physical meaning:** The derivative of position gives velocity; the derivative of velocity gives acceleration.

---

## 2. Chain Rule and Multiple Variables

If a vector depends on multiple variables, e.g., $\mathbf{r} = \mathbf{r}(\theta(t))$, then:

$$
\frac{d\mathbf{r}}{dt} = \frac{d\mathbf{r}}{d\theta} \cdot \frac{d\theta}{dt}
$$

**Use case:** Orbital mechanics often expresses motion in terms of **true anomaly** $\theta$ instead of time.

---

## 3. Gradient, Divergence, and Curl

* **Gradient ($\nabla f$)**: points in the direction of maximum increase of scalar $f$.

$$
\nabla f = \frac{\partial f}{\partial x} \hat{\mathbf{i}} + \frac{\partial f}{\partial y} \hat{\mathbf{j}} + \frac{\partial f}{\partial z} \hat{\mathbf{k}}
$$

* **Divergence ($\nabla \cdot \mathbf{F}$)**: measures the net “outflow” from a point.

$$
\nabla \cdot \mathbf{F} = \frac{\partial F_x}{\partial x} + \frac{\partial F_y}{\partial y} + \frac{\partial F_z}{\partial z}
$$

* **Curl ($\nabla \times \mathbf{F}$)**: measures the rotation of a vector field.

$$
\nabla \times \mathbf{F} = 
\begin{vmatrix}
\hat{\mathbf{i}} & \hat{\mathbf{j}} & \hat{\mathbf{k}} \\
\frac{\partial}{\partial x} & \frac{\partial}{\partial y} & \frac{\partial}{\partial z} \\
F_x & F_y & F_z
\end{vmatrix}
$$

> **Use in orbital mechanics:**
>
> * Gradient of gravitational potential gives acceleration: $\mathbf{a} = -\nabla U$
> * Divergence of velocity field helps in fluid dynamics for upper atmosphere models
> * Curl arises in rotating reference frames (Coriolis effects)

---

## 4. Practical Example: Derivatives in Python

```python
import numpy as np

# Position vector as function of time (circular orbit)
t = np.linspace(0, 3600, 1000)  # seconds
r = 7000e3  # meters
omega = 0.001  # rad/s

x = r * np.cos(omega*t)
y = r * np.sin(omega*t)
z = np.zeros_like(t)

# Velocity: derivative of position
vx = np.gradient(x, t)
vy = np.gradient(y, t)
vz = np.gradient(z, t)

# Acceleration: derivative of velocity
ax = np.gradient(vx, t)
ay = np.gradient(vy, t)
az = np.gradient(vz, t)

print("Sample velocity (m/s):", vx[0], vy[0], vz[0])
print("Sample acceleration (m/s^2):", ax[0], ay[0], az[0])
```

---

## 5. Short Note

Calculus is the **language of motion**. Every orbit, maneuver, or perturbation can be described mathematically as a derivative or differential equation. Mastering these tools allows us to:

* Predict spacecraft trajectories
* Compute orbital velocities and energies
* Solve the two-body and n-body problems

> The **next sections** will build on these skills: linear algebra (2.4) and differential equations (2.5) will combine calculus with vectors to solve real orbital motion problems.

---

## References

* Stewart, J. *Calculus: Early Transcendentals*, Ch. 12
* Arfken, G., & Weber, H. *Mathematical Methods for Physicists*, Ch. 1–3
* Vallado, D. A. *Fundamentals of Astrodynamics and Applications*, §1.6


