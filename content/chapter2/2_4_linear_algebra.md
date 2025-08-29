# 2.4 Linear Algebra Essentials

📂 **File name:** `content/chapter2/2_4_linear_algebra.md`

---

## Why Linear Algebra in Astrodynamics?

Linear algebra is essential for:

* Representing vectors and matrices in 3D space
* Performing **coordinate transformations**
* Solving **systems of equations** in orbit determination
* Computing **eigenvalues/eigenvectors** for stability analysis in dynamics

---

## 1. Vector and Matrix Operations

* **Vector addition/subtraction:**

$$
\mathbf{a} + \mathbf{b} = [a_x+b_x, a_y+b_y, a_z+b_z]
$$

* **Scalar multiplication:**

$$
k \mathbf{a} = [k a_x, k a_y, k a_z]
$$

* **Matrix multiplication (dot product of matrices):**

$$
C = A \cdot B
$$

* **Matrix-vector multiplication:**

$$
\mathbf{v}' = C \mathbf{v}
$$

> Use this to apply rotation matrices and DCMs to vectors in different frames.

---

## 2. Determinants and Inverse

* Determinant tells if a matrix is **invertible**: $\det(A) \neq 0 \Rightarrow A^{-1}$ exists
* Inverse is needed to **reverse coordinate transformations**:

$$
\mathbf{v} = C^{-1} \mathbf{v}' \quad \text{or} \quad C^{-1} = C^\top \text{ for rotation matrices}
$$

---

## 3. Eigenvalues and Eigenvectors

* **Definition:**

$$
A \mathbf{x} = \lambda \mathbf{x}
$$

where $\lambda$ = eigenvalue, $\mathbf{x}$ = eigenvector

* **Use in astrodynamics:**

  * Stability analysis of orbital perturbations
  * Principal axes of inertia in spacecraft attitude dynamics

---

## 4. Solving Linear Systems

* System of equations: $A \mathbf{x} = \mathbf{b}$
* Solve using **NumPy**:

```python
import numpy as np

A = np.array([[2, -1, 0],
              [1,  2, -1],
              [3, -1, 2]], dtype=float)
b = np.array([1, 2, 3], dtype=float)

x = np.linalg.solve(A, b)
print("Solution x =", x)
```

> Useful for **orbital element determination** or **trajectory optimization**.

---

## 5. Example: Rotation of a Vector

```python
# Rotation of a position vector around z-axis
theta = np.radians(45)
Cz = np.array([[np.cos(theta), -np.sin(theta), 0],
               [np.sin(theta),  np.cos(theta), 0],
               [0, 0, 1]])

r = np.array([1, 0, 0])
r_rotated = Cz @ r
print("Rotated vector:", r_rotated)
```

---

## 6. Short Note

Linear algebra is the **framework** for handling multidimensional data in astrodynamics. Combined with calculus and coordinate transformations:

* We can **propagate orbits**
* Rotate and transform vectors between frames
* Analyze **stability and perturbations**

Mastery of these tools ensures smooth handling of **real spacecraft problems**.

---

## References

* Strang, G. *Introduction to Linear Algebra*, Ch. 1–5
* Vallado, D. A. *Fundamentals of Astrodynamics and Applications*, Appendix A
* Curtis, H. D. *Orbital Mechanics for Engineering Students*, Ch. 1–2

