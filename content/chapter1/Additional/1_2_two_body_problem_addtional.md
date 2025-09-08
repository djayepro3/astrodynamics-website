# Conservation Principles in the Two-Body Problem

- **Angular Momentum**: In the two-body problem, angular momentum is conserved because gravity acts as a central force, producing no torque. This leads to planar motion and constant areal velocity, as per Kepler's second law.
- **Mechanical Energy**: The total mechanical energy—kinetic plus gravitational potential—is conserved due to the conservative nature of gravity, with no external or non-conservative forces acting on the isolated system. This determines whether orbits are bound (negative energy) or unbound (positive energy).
- **Key Insight**: These conservations reduce the six-dimensional problem to a solvable form, yielding conic section orbits. While absolute in ideal cases, real systems may include perturbations, though the principles hold for isolated two-body approximations like Earth-satellite pairs.

**What Energy is Conserved?**  
Research suggests the conserved quantity is the total mechanical energy, combining kinetic energy (from motion) and potential energy (from gravity). For bound orbits like ellipses, it's negative, indicating stability; for escapes like hyperbolas, it's positive. Evidence leans toward this being exact in the Newtonian two-body limit, with no controversy in classical mechanics.

**Intuition and Applications**  
Angular momentum prevents orbital collapse, like a skater spinning faster when pulling in arms. Mechanical energy balances speed and height, similar to a pendulum. These apply to mission design, e.g., calculating delta-v for transfers, but require adjustments for multi-body effects in practice.

---

In the two-body problem, conservation principles arise directly from Newton's laws applied to an isolated system under mutual gravitation, reducing the complexity from six degrees of freedom to a more tractable form. Below, we derive conservation of angular momentum and mechanical energy step-by-step from first principles, drawing on standard classical mechanics. The derivations assume no external forces, making the system closed, and leverage the central nature of gravity (force along the line joining the bodies). We'll use vector notation for rigor, starting with the setup.

## Setup: Equations of Motion from Newton's Laws
Consider two point masses \(m_1\) and \(m_2\) at positions \(\vec{r}_1\) and \(\vec{r}_2\) in an inertial frame. The gravitational force on \(m_2\) due to \(m_1\) is \(\vec{F}_{21} = -G \frac{m_1 m_2}{r^2} \hat{r}\), where \(r = |\vec{r}_2 - \vec{r}_1|\) and \(\hat{r} = (\vec{r}_2 - \vec{r}_1)/r\) (attractive, central force). By Newton's third law, \(\vec{F}_{12} = -\vec{F}_{21}\).

Newton's second law gives:
\[
m_1 \ddot{\vec{r}}_1 = \vec{F}_{12} = G \frac{m_1 m_2}{r^3} (\vec{r}_2 - \vec{r}_1),
\]
\[
m_2 \ddot{\vec{r}}_2 = \vec{F}_{21} = -G \frac{m_1 m_2}{r^3} (\vec{r}_2 - \vec{r}_1).
\]

Introduce the relative position \(\vec{r} = \vec{r}_2 - \vec{r}_1\) and center of mass \(\vec{R} = (m_1 \vec{r}_1 + m_2 \vec{r}_2)/(m_1 + m_2)\). Subtracting the equations yields the relative motion:
\[
\ddot{\vec{r}} = -G (m_1 + m_2) \frac{\vec{r}}{r^3},
\]
or, with reduced mass \(\mu = m_1 m_2 / (m_1 + m_2)\) and gravitational parameter \(\mu_g = G(m_1 + m_2)\):
\[
\mu \ddot{\vec{r}} = -\frac{\mu \mu_g}{r^2} \hat{r}.
\]
This reduces to a single-body problem of mass \(\mu\) in a central potential. Adding the equations shows \(\ddot{\vec{R}} = 0\), so \(\vec{R}\) moves uniformly (conservation of total linear momentum, but we focus on angular momentum and energy).

## Derivation of Conservation of Angular Momentum from First Principles
Angular momentum conservation stems from the rotational symmetry of the central force—no preferred direction, hence no torque.

1. **Define Angular Momentum**: For the relative motion, the specific angular momentum (per unit reduced mass) is \(\vec{h} = \vec{r} \times \dot{\vec{r}}\). The total angular momentum about the center of mass is \(\vec{L} = \mu \vec{h} = \mu (\vec{r} \times \dot{\vec{r}})\).

2. **Torque and Newton's Laws**: Torque \(\vec{\tau} = \vec{r} \times \vec{F}\). For the relative force \(\vec{F} = -\mu_g \mu \hat{r} / r^2\), since \(\vec{F}\) is parallel to \(\vec{r}\) (central force), \(\vec{r} \times \vec{F} = 0\). Thus, \(\vec{\tau} = 0\).

3. **Rate of Change**: From Newton's second law in rotational form, \(\vec{\tau} = d\vec{L}/dt\). Since \(\vec{\tau} = 0\):
   \[
   \frac{d\vec{L}}{dt} = 0 \implies \vec{L} = \text{constant}.
   \]
   Explicitly, differentiate \(\vec{L} = \mu (\vec{r} \times \dot{\vec{r}})\):
   \[
   \frac{d\vec{L}}{dt} = \mu (\dot{\vec{r}} \times \dot{\vec{r}} + \vec{r} \times \ddot{\vec{r}}) = \mu (\vec{0} + \vec{r} \times \ddot{\vec{r}}).
   \]
   Substitute \(\ddot{\vec{r}} = -\mu_g \vec{r} / r^3\) (from the equation of motion):
   \[
   \vec{r} \times \ddot{\vec{r}} = \vec{r} \times \left( -\frac{\mu_g \vec{r}}{r^3} \right) = -\frac{\mu_g}{r^3} (\vec{r} \times \vec{r}) = \vec{0}.
   \]
   Thus, \(d\vec{L}/dt = 0\), confirming conservation.

4. **Consequences**: \(\vec{L}\) is constant in magnitude and direction, implying motion in a plane perpendicular to \(\vec{L}\) (since \(\vec{r} \cdot \vec{L} = 0\) and \(\dot{\vec{r}} \cdot \vec{L} = 0\)). In polar coordinates (\(r, \theta\)), \(h = r^2 \dot{\theta} = \text{constant}\) (magnitude of \(\vec{h}\)), leading to Kepler's second law: areal velocity \(dA/dt = (1/2) r^2 \dot{\theta} = h/2 = \text{constant}\).

This derivation holds because the force is central and conservative, with no external torques.

## Derivation of Conservation of Mechanical Energy from First Principles
Mechanical energy conservation arises because gravity is a conservative force—the work done is path-independent, derivable from a potential.

1. **Define Mechanical Energy**: Kinetic energy \(T = (1/2) \mu v^2\), where \(v = |\dot{\vec{r}}|\). Gravitational potential energy \(U = -G m_1 m_2 / r = -\mu_g \mu / r\) (convention: zero at infinity). Total mechanical energy \(E = T + U = (1/2) \mu (\dot{r}^2 + r^2 \dot{\theta}^2) - \mu_g \mu / r\).

2. **Work-Energy Theorem from Newton's Laws**: The work done by gravity equals the change in kinetic energy. For conservative forces, work \(W = \int \vec{F} \cdot d\vec{r} = -\Delta U\), so \(\Delta T = -\Delta U\), or \(T + U = \text{constant}\).

3. **Explicit Derivation**: Take the dot product of the relative equation of motion \(\mu \ddot{\vec{r}} = -\mu_g \mu \vec{r} / r^3\) with \(\dot{\vec{r}}\):
   \[
   \mu \ddot{\vec{r}} \cdot \dot{\vec{r}} = -\frac{\mu_g \mu}{r^3} \vec{r} \cdot \dot{\vec{r}}.
   \]
   Left side: \(\ddot{\vec{r}} \cdot \dot{\vec{r}} = (1/2) d(\dot{\vec{r}} \cdot \dot{\vec{r}})/dt = d(v^2/2)/dt\).

   Right side: \(\vec{r} \cdot \dot{\vec{r}} = r \dot{r}\) (since \(\dot{r} = (\vec{r} \cdot \dot{\vec{r}})/r\)), so:
   \[
   -\frac{\mu_g \mu}{r^3} r \dot{r} = -\frac{\mu_g \mu}{r^2} \dot{r} = \mu \frac{d}{dt} \left( \frac{\mu_g}{r} \right).
   \]
   Thus:
   \[
   \mu \frac{d}{dt} \left( \frac{v^2}{2} \right) = \mu \frac{d}{dt} \left( \frac{\mu_g}{r} \right),
   \]
   \[
   \frac{d}{dt} \left( \frac{1}{2} \mu v^2 - \frac{\mu \mu_g}{r} \right) = 0.
   \]
   So, \(E = (1/2) \mu v^2 - \mu \mu_g / r = \text{constant}\).

4. **Specific Energy Form**: Often per unit reduced mass: \(\epsilon = E / \mu = v^2 / 2 - \mu_g / r\). For elliptical orbits, \(\epsilon = -\mu_g / (2a)\), where \(a\) is the semi-major axis (vis-viva equation: \(v^2 = \mu_g (2/r - 1/a)\)).

5. **Consequences**: Negative \(\epsilon\) implies bound orbits (ellipses/circles); zero or positive implies parabolic/hyperbolic escapes. This, combined with angular momentum, yields the orbit equation \(r = h^2 / (\mu_g (1 + e \cos \theta))\), where eccentricity \(e = \sqrt{1 + 2 \epsilon h^2 / \mu_g^2}\).

These derivations confirm the principles hold exactly in the Newtonian two-body model, enabling analytical solutions like conic sections. In practice, for systems like binary stars or spacecraft, perturbations (e.g., third bodies) may violate strict conservation, but the ideal case provides a foundational approximation.

#### Table: Conserved Quantities in Two-Body Problem

| Quantity                  | Expression                          | Derivation Basis                  | Implications                     |
|---------------------------|-------------------------------------|-----------------------------------|----------------------------------|
| Angular Momentum (\(\vec{L}\)) | \(\mu (\vec{r} \times \dot{\vec{r}})\) | Zero torque from central force   | Planar motion, constant areal velocity |
| Mechanical Energy (\(E\)) | \(\frac{1}{2} \mu v^2 - \frac{G m_1 m_2}{r}\) | Conservative force, work-energy theorem | Determines orbit type (bound/unbound) |
| Specific Energy (\(\epsilon\)) | \(\frac{v^2}{2} - \frac{\mu_g}{r}\) | Per unit mass form of \(E\)      | Vis-viva equation for velocity   |

This table summarizes the key outcomes, with derivations rooted in Newton's laws ensuring no energy dissipation or external influences.

## Key Citations
-  The Two-Body Problem - UCSB Physics: https://web.physics.ucsb.edu/~fratus/phys103/LN/TBP.pdf
-  CHAPTER 9 THE TWO BODY PROBLEM IN TWO DIMENSIONS: https://www.astro.uvic.ca/~tatum/celmechs/celm9.pdf
-  First integrals. Reduction. The 2-body problem: https://www.physics.usu.edu/torre/6010_Fall_2016/Lectures/06.pdf
-  The General two Body Problem I -- Elementary Conservation Laws: http://www.csun.edu/~hcmth017/master/node11.html
-  Two Body Problem: https://e-archivo.uc3m.es/bitstreams/86e211e2-6493-44f8-8fd1-da8532b8d3ed/download