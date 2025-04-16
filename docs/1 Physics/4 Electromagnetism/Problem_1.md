# Problem 1
# Simulating the Effects of the Lorentz Force

##  Motivation

The Lorentz force, expressed as:

`F = qE + q(v × B)` &nbsp;&nbsp;&nbsp; <!-- hidden LaTeX for rendering -->
<!-- $ \vec{F} = q\vec{E} + q\vec{v} \times \vec{B} $ -->

governs the motion of charged particles in electric and magnetic fields. It is foundational in fields like plasma physics, particle accelerators, and astrophysics. By focusing on simulations, we can explore the practical applications and visualize the complex trajectories that arise due to this force.

##  Task Breakdown

### 1. Exploration of Applications

- **Practical Systems:** The Lorentz force plays a critical role in particle accelerators, mass spectrometers, and magnetic confinement in fusion reactors.
- **Field Roles:** Electric fields (`E`) accelerate particles linearly, while magnetic fields (`B`) bend or spiral particle paths, depending on velocity and field direction.
  <!-- $ \vec{E}, \vec{B} $ -->

### 2. Simulating Particle Motion

We simulate a charged particle’s motion in the following conditions:

- Uniform magnetic field only  
- Combined uniform electric and magnetic fields  
- Crossed electric and magnetic fields  

Circular, helical, and drift motions will be visualized using initial conditions and field configurations.

### 3. Parameter Exploration

We will vary:
- Field strengths (`E`, `B`)  <!-- $ \vec{E}, \vec{B} $ -->
- Initial velocity (`v`)       <!-- $ \vec{v} $ -->
- Particle charge (`q`) and mass (`m`)

### 4. Visualization

- Clear 2D and 3D plots of trajectories  
- Phenomena like **Larmor radius** and **drift velocity** will be demonstrated

---

##  Simulation in Python
![alt text](image.png)

```python
import numpy as np
import matplotlib.pyplot as plt
from mpl_toolkits.mplot3d import Axes3D

# Constants
q = 1.6e-19       # Charge of the particle (Coulombs)
m = 9.1e-31       # Mass of the particle (kg)
B = np.array([0, 0, 1])  # Uniform magnetic field (Tesla)
E = np.array([0, 0, 0])  # Electric field (V/m)
v0 = np.array([1e5, 0, 0])  # Initial velocity (m/s)

# Time settings
dt = 1e-11  # Time step (s)
steps = 1000  # Number of steps

# Initialize position and velocity arrays
r = np.zeros((steps, 3))
v = np.zeros((steps, 3))
r[0] = [0, 0, 0]
v[0] = v0

# Euler integration loop
for i in range(steps - 1):
    F = q * (E + np.cross(v[i], B))
    a = F / m
    v[i + 1] = v[i] + a * dt
    r[i + 1] = r[i] + v[i + 1] * dt

# Plotting the trajectory
fig = plt.figure(figsize=(8, 6))
ax = fig.add_subplot(111, projection='3d')
ax.plot(r[:, 0], r[:, 1], r[:, 2])
ax.set_title("Trajectory of Charged Particle in Magnetic Field")
ax.set_xlabel("X (m)")
ax.set_ylabel("Y (m)")
ax.set_zlabel("Z (m)")
plt.tight_layout()
plt.show()
```

---

##  Observations

- In a **uniform magnetic field**, the particle undergoes circular motion.  
- When an electric field is added, the trajectory becomes **helical** or shows **drift** depending on the direction.  
- Increasing `B` or `q` tightens the curve, while a higher `m` slows the spiral.  
- The **Larmor radius** is proportional to `$ \frac{mv}{qB} $`  
- **Drift velocity** appears as `$ \vec{v}_d = \frac{\vec{E} \times \vec{B}}{B^2} $` in crossed fields.

---

##  Real-World Applications

- **Cyclotrons** use magnetic fields to curve particles into spirals as they gain energy.  
- **Magnetic traps** hold particles in plasma reactors.  
- In **astrophysics**, the Lorentz force explains how charged particles move in planetary magnetic fields.

---

##  Extension Suggestions

- Introduce **non-uniform** magnetic fields `$ \vec{B}(x, y, z) $` or time-varying electric fields.  
- Implement **Runge-Kutta 4th order** integration for higher precision.  
- Simulate multiple particles with different `q/m` ratios.  
- Explore **relativistic speeds** and the resulting Lorentz transformations.

---

##  Deliverables Checklist

1.  Markdown document with embedded Python simulation  
2.  Particle trajectory plots for various field settings  
3.  Real-world discussion (cyclotrons, traps, etc.)  
4.  Ideas for extending the simulation  


