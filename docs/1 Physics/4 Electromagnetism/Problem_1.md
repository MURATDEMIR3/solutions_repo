# Problem 1
# Simulating the Effects of the Lorentz Force

##  Motivation

The Lorentz force, expressed as:

$$
\vec{F} = q\vec{E} + q\vec{v} \times \vec{B}
$$

governs the motion of charged particles in electric and magnetic fields. It is foundational in fields like plasma physics, particle accelerators, and astrophysics. Through simulations, we can explore the practical applications and visualize the complex trajectories that arise due to this force.

---

##  Task Breakdown

### 1. Exploration of Applications

- **Real-world Systems**: The Lorentz force plays a crucial role in:
  - Particle accelerators
  - Mass spectrometers
  - Plasma confinement systems

- **Field Relevance**:
  - Electric fields ($\vec{E}$) accelerate particles.
  - Magnetic fields ($\vec{B}$) steer particle trajectories.
  - Combined fields create intricate motion patterns.

---

### 2. Simulating Particle Motion

We'll simulate the trajectory of a charged particle using the Runge-Kutta method (4th order). Scenarios:

- Uniform magnetic field
- Combined electric and magnetic fields
- Crossed electric and magnetic fields

We'll observe:
- **Circular motion**
- **Helical trajectories**
- **Drift behavior**

---

### 3. Parameter Exploration

We will vary:

- Field Strengths: $\vec{E}, \vec{B}$
- Particle's initial velocity $\vec{v}$
- Charge $q$ and mass $m$

Goal: Understand how each parameter impacts the trajectory.

---

##  Visualization

- 2D and 3D plots of particle motion
- Highlight physical effects:
  - **Larmor radius**
  - **Drift velocity**
  - **Cyclotron motion**

---

##  Python Simulation

We use `NumPy` for computation and `Matplotlib` for visualization.

```python
import numpy as np
import matplotlib.pyplot as plt
from mpl_toolkits.mplot3d import Axes3D

# Constants
q = 1.6e-19  # Charge (Coulombs)
m = 9.1e-31  # Mass (kg)

# Field Definitions (Uniform)
E = np.array([0.0, 0.0, 0.0])      # Electric field (V/m)
B = np.array([0.0, 0.0, 1.0])      # Magnetic field (T)

# Time settings
dt = 1e-11  # Time step
steps = 1000

# Initial conditions
r = np.zeros((steps, 3))   # Position array
v = np.zeros((steps, 3))   # Velocity array

# Initial position and velocity
r[0] = np.array([0.0, 0.0, 0.0])
v[0] = np.array([1e6, 0.0, 0.0])

# Lorentz force using Runge-Kutta 4
def lorentz_force(v, E, B):
    return (q/m) * (E + np.cross(v, B))

def runge_kutta_step(r, v, dt):
    k1v = lorentz_force(v, E, B)
    k1r = v

    k2v = lorentz_force(v + 0.5*dt*k1v, E, B)
    k2r = v + 0.5*dt*k1v

    k3v = lorentz_force(v + 0.5*dt*k2v, E, B)
    k3r = v + 0.5*dt*k2v

    k4v = lorentz_force(v + dt*k3v, E, B)
    k4r = v + dt*k3v

    v_new = v + (dt/6)*(k1v + 2*k2v + 2*k3v + k4v)
    r_new = r + (dt/6)*(k1r + 2*k2r + 2*k3r + k4r)
    return r_new, v_new

# Simulation loop
for i in range(steps - 1):
    r[i+1], v[i+1] = runge_kutta_step(r[i], v[i], dt)

# Plotting the trajectory
fig = plt.figure(figsize=(10,6))
ax = fig.add_subplot(111, projection='3d')
ax.plot(r[:,0], r[:,1], r[:,2])
ax.set_title('Particle Trajectory under Uniform Magnetic Field')
ax.set_xlabel('X Position (m)')
ax.set_ylabel('Y Position (m)')
ax.set_zlabel('Z Position (m)')
plt.show()

