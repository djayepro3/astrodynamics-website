# Newton’s Laws and Universal Gravitation

Astrodynamics begins with **first principles**: how forces cause motion. In this section, we’ll build from Newton’s laws to the law of universal gravitation—the foundation of orbital mechanics. We'll explore these concepts with historical context, practical examples from space exploration, and their direct application to understanding orbits. This sets the stage for deriving the basic equations of motion for celestial bodies and spacecraft.

## Historical Context: From Kepler to Newton

Before diving into the laws, it's essential to appreciate the groundwork laid by earlier astronomers. Johannes Kepler, in the early 17th century, derived three empirical laws from Tycho Brahe's observations of planetary motion:
- **Kepler's First Law**: Planets orbit the Sun in ellipses, with the Sun at one focus.
- **Kepler's Second Law**: A line from the planet to the Sun sweeps equal areas in equal times.
- **Kepler's Third Law**: The square of the orbital period is proportional to the cube of the semi-major axis.

These were observational rules without a physical explanation. In 1687, Isaac Newton provided the theoretical foundation in his *Philosophiæ Naturalis Principia Mathematica*, using his laws of motion and gravitation to derive Kepler's laws mathematically. Newton's work unified terrestrial and celestial mechanics, showing that the same force pulling an apple to Earth keeps the Moon in orbit.

## Newton’s Laws of Motion

Newton's three laws describe how objects behave under forces, crucial for predicting spacecraft trajectories and satellite orbits.

### First Law (Law of Inertia)
An object at rest remains at rest, or if in motion, continues in a straight line at constant speed unless acted upon by a net external force.

\[
\mathbf{F}_{\text{net}} = 0 \quad \Rightarrow \quad \mathbf{a} = 0
\]

**In Space**: Without air resistance or other forces, a spacecraft coasts in a straight line indefinitely. However, in orbits, gravity provides the continuous force to curve the path—satellites are in perpetual "free fall" around Earth, not truly weightless but experiencing microgravity.

**Common Misconception**: Many think orbits require engines to "stay up." In reality, per the first law, no propulsion is needed once in orbit; gravity balances the inertial tendency to fly straight.

### Second Law (Force and Acceleration)
The net force on an object equals its mass times acceleration, or the rate of change of momentum.

\[
\mathbf{F} = \frac{d\mathbf{p}}{dt} = m \mathbf{a}, \quad \mathbf{p} = m \mathbf{v}
\]

**In Space**: This law quantifies how thrust from rockets accelerates spacecraft. For variable mass (e.g., fuel expulsion), it becomes \(\mathbf{F} = \frac{dm}{dt} \mathbf{v}_{\text{exhaust}} + m \mathbf{a}\), key for rocket equation derivations in later chapters.

### Third Law (Action–Reaction)
For every action force, there is an equal and opposite reaction force.

\[
\mathbf{F}_{12} = - \mathbf{F}_{21}
\]

**In Space**: Rockets propel forward by expelling exhaust backward. In orbital maneuvers, firing thrusters pushes the spacecraft in the opposite direction, conserving total momentum. This also explains tidal forces between bodies like Earth and Moon, where mutual gravitation causes subtle orbital changes over time (e.g., the Moon recedes from Earth by about 3.8 cm per year).

These laws ensure conservation of linear and angular momentum in isolated systems, fundamental for multi-body problems in astrodynamics.

## Newton’s Law of Universal Gravitation

Newton hypothesized that gravity is a universal force: every particle attracts every other with a force proportional to their masses and inversely proportional to the square of the distance between them.

\[
\mathbf{F}_{12} = -G \frac{m_1 m_2}{r^2} \hat{\mathbf{r}}
\]

where:
- \(G\) is the universal gravitational constant (\(6.67430 \times 10^{-11}\, \text{m}^3 \cdot \text{kg}^{-1} \cdot \text{s}^{-2}\)),
- \(m_1, m_2\) are the masses,
- \(r\) is the separation,
- \(\hat{\mathbf{r}}\) is the unit vector from \(m_1\) to \(m_2\) (making the force attractive).

**Historical Insight**: Newton reportedly conceived this while observing a falling apple, realizing it extended to the Moon. He delayed publication due to challenges proving it for spherical bodies (resolved via his shell theorem).

**Key Property**: The inverse-square nature explains why gravity weakens rapidly with distance, enabling stable orbits rather than chaotic falls.

**Example Calculation**: Surface gravity on Earth (\(g \approx 9.81\, \text{m/s}^2\)):

\[
g = G \frac{M_{\Earth}}{R_{\Earth}^2}
\]

where \(M_{\Earth} \approx 5.972 \times 10^{24}\, \text{kg}\), \(R_{\Earth} \approx 6.371 \times 10^6\, \text{m}\). Try computing this in the code repository for practice!

## Combining Newton’s Laws: The Two-Body Problem

In astrodynamics, we apply these laws to the **two-body problem**: motion of two masses under mutual gravity, ignoring other forces. This approximates satellite-Earth or planet-Sun systems where one mass dominates.

From the second law and gravitation:

For body 2 (mass \(m\)) orbiting body 1 (mass \(M\)):

\[
m \mathbf{a} = - G \frac{M m}{r^2} \hat{\mathbf{r}}
\]

Cancel \(m\) (equivalence principle—all objects fall at the same rate):

\[
\mathbf{a} = - G \frac{M}{r^2} \hat{\mathbf{r}}
\]

For relative motion, introduce the **gravitational parameter** \(\mu = G(M + m) \approx GM\) (when \(m \ll M\)):

\[
\ddot{\mathbf{r}} = - \frac{\mu}{r^3} \mathbf{r}
\]

This second-order differential equation governs orbital motion. Solutions are conic sections (ellipses for bound orbits), directly deriving Kepler's laws.

**Intuition**: Orbits balance inertia (straight-line motion) with gravitational pull, like swinging a ball on a string.

**Equivalence Principle**: The cancellation of mass explains why feathers and hammers fall equally in vacuum (as demonstrated on the Moon by Apollo 15).

## Visualization: Earth–Moon Gravitational Interaction

To build intuition, here's a Python/Plotly simulation visualizing the Earth-Moon system with a force vector. We've enhanced it for professionalism: realistic size ratios, a connecting line, and an annotation for the force. Run this in your Jupyter notebook (via Binder or Colab) for interactivity—rotate, zoom, and experiment with parameters.

```python
import plotly.graph_objects as go
import numpy as np

# Constants (in km)
earth_radius = 6371
moon_radius = 1737
distance = 384400  # Average Earth-Moon distance

# Positions
earth_pos = np.array([0, 0, 0])
moon_pos = np.array([distance, 0, 0])

# Direction for force on Moon (towards Earth)
force_dir = earth_pos - moon_pos
force_unit = force_dir / np.linalg.norm(force_dir)

# Create figure
fig = go.Figure()

# Earth marker (scaled size)
fig.add_trace(go.Scatter3d(
    x=[earth_pos[0]], y=[earth_pos[1]], z=[earth_pos[2]],
    mode='markers+text',
    text=['Earth'], textposition="top center",
    marker=dict(size=earth_radius / 10000, color='blue')  # Scaled for visibility
))

# Moon marker (scaled size)
fig.add_trace(go.Scatter3d(
    x=[moon_pos[0]], y=[moon_pos[1]], z=[moon_pos[2]],
    mode='markers+text',
    text=['Moon'], textposition="top center",
    marker=dict(size=moon_radius / 10000, color='gray')
))

# Line connecting centers
fig.add_trace(go.Scatter3d(
    x=[earth_pos[0], moon_pos[0]],
    y=[earth_pos[1], moon_pos[1]],
    z=[earth_pos[2], moon_pos[2]],
    mode='lines',
    line=dict(color='black', width=2),
    name='Separation'
))

# Force vector (cone arrow from Moon towards Earth)
arrow_length = distance * 0.1  # 10% of distance for visibility
fig.add_trace(go.Cone(
    x=[moon_pos[0]], y=[moon_pos[1]], z=[moon_pos[2]],
    u=[force_unit[0] * arrow_length],
    v=[force_unit[1] * arrow_length],
    w=[force_unit[2] * arrow_length],
    sizemode="absolute", sizeref=1,
    colorscale="Viridis",
    showscale=False
))

# Annotation for force
fig.update_layout(
    scene=dict(
        xaxis_title="X (km)",
        yaxis_title="Y (km)",
        zaxis_title="Z (km)",
        annotations=[dict(
            showarrow=False,
            x=moon_pos[0] - distance * 0.3,
            y=0,
            z=distance * 0.05,
            text="Gravitational Force on Moon",
            font=dict(size=12)
        )]
    ),
    title="Earth–Moon Gravitational Force Vector (Force on Moon Towards Earth)"
)

fig.show()
```

* **Improvements**: Realistic radius scaling (though compressed for plot visibility), a separation line, normalized force direction, and an annotation. The arrow represents the direction and relative magnitude of the force on the Moon.
* **Extension Idea**: Modify the code to compute and display the actual force magnitude using \(G\), \(M_{\Earth}\), and \(M_{\Moon}\) (add as variables).
* **Interactive Tip**: In Colab, tweak the distance to see how the force vector changes, illustrating the inverse-square law.

## Key Concepts and Takeaways

- **Gravitational Parameter (\(\mu\))**: For Earth, \(\mu \approx 3.986 \times 10^5\, \text{km}^3/\text{s}^2\). This combines \(G\) and \(M\), simplifying calculations since \(G\) is hard to measure precisely.
- **Applications**: These principles enable GPS satellites, interplanetary missions (e.g., Voyager), and understanding phenomena like eclipses and tides.
- **Limitations**: Assumes point masses and no other forces; real astrodynamics accounts for perturbations (e.g., Earth's oblateness, solar gravity).

Explore the companion repository for full code and simulations. Next sections build on this to derive orbital elements.

## References

* Newton, I. *Philosophiæ Naturalis Principia Mathematica* (1687).
* Curtis, H. D. *Orbital Mechanics for Engineering Students* (4th ed., 2020).
* Vallado, D. A. *Fundamentals of Astrodynamics and Applications* (4th ed., 2013).
* Wiesel, W. E. *Spaceflight Dynamics* (2nd ed., 1997).
* NASA Jet Propulsion Laboratory. *Basics of Space Flight* (online tutorial).
* Burrows, A. *Basics of Kepler and Newton* (Princeton University lecture notes).

---

**File name:** `content/chapter1/1_1_newtons_laws.md`