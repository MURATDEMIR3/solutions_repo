# Problem 1

# Simulation of Charged Particle Dynamics under the Lorentz Force in EM Fields

# Motivation
The Lorentz force, defined by the equation  
  𝐅 = 𝑞(𝐄 + 𝐯 × 𝐁)  
describes the motion of charged particles in electric (𝐄) and magnetic (𝐁) fields.  
This fundamental principle underpins many advanced systems in modern physics:

 • Particle accelerators (e.g., cyclotrons, synchrotrons)  
 • Plasma confinement devices (e.g., Tokamaks)  
 • Mass spectrometers  
 • Astrophysical phenomena (e.g., solar wind–magnetosphere interaction)

By simulating the Lorentz force numerically, we can explore trajectory patterns such as:
 • Circular motion (perpendicular 𝐯 and 𝐁)  
 • Helical paths (with longitudinal velocity component)  
 • Drift motion (crossed 𝐄 and 𝐁 fields)

# Task Structure

[1] Application Context
✔ Real-world systems where the Lorentz force is key:  
   - Mass analyzers (e.g., Time-of-Flight, Magnetic Sector MS)  
   - Plasma propulsion  
   - Radiation belts in planetary magnetospheres  

✔ Role of 𝐄 and 𝐁 fields:  
   - 𝐁 causes centripetal force → circular/spiral motion  
   - 𝐄 accelerates or retards particles → drift velocity (𝐯ᴅ = 𝐄 × 𝐁 / |𝐁|²)

[2] Numerical Simulation
We solve Newton’s second law with the Lorentz force:

 F = q(E + v × B) → a = F / m  
Numerical Integration: Explicit Euler method
# Python Implementation
![alt text](image.png)
```python
import numpy as np
import matplotlib.pyplot as plt
from mpl_toolkits.mplot3d import Axes3D

# Constants
q = 1.6e-19      # Elementary charge [C]
m = 9.11e-31     # Electron mass [kg]
E = np.array([0.0, 1e3, 0.0])   # Uniform Electric Field [V/m]
B = np.array([0.0, 0.0, 1.0])   # Uniform Magnetic Field [T]
v0 = np.array([1e6, 0.0, 0.0])  # Initial velocity [m/s]
r0 = np.array([0.0, 0.0, 0.0])  # Initial position [m]

dt = 1e-11
N = 2000

def lorentz(q, v, E, B):
    return q * (E + np.cross(v, B))

def run_simulation():
    r = np.zeros((N, 3))
    v = np.zeros((N, 3))
    r[0], v[0] = r0, v0
    for i in range(1, N):
        a = lorentz(q, v[i-1], E, B) / m
        v[i] = v[i-1] + a * dt
        r[i] = r[i-1] + v[i] * dt
    return r

path = run_simulation()

# Visualization
fig = plt.figure()
ax = fig.add_subplot(111, projection='3d')
ax.plot(path[:,0], path[:,1], path[:,2], lw=1.5, color='dodgerblue')
ax.set_title("Charged Particle Trajectory in Crossed Fields", fontsize=12)
ax.set_xlabel("x [m]"); ax.set_ylabel("y [m]"); ax.set_zlabel("z [m]")
plt.tight_layout(); plt.grid(True); plt.show()
```

[3] Parameter Exploration
We vary key physical quantities to observe their effects:

• |𝐁| ↑ ⇒ radius ↓ (r = mv⊥ / qB), cyclotron frequency ↑  
• Add 𝐄 ⟶ net drift along 𝐄 × 𝐁  
• Increase mass ⇒ slower acceleration (a ∝ 1/m)

Tip: Larmor Radius and Cyclotron Period are central to interpreting these paths.

[4] Visualization and Analysis
• 2D and 3D plots of the particle trajectory  
• Clear marking of axes and vector directions  
• Identification of:  
  - Spiral pitch and radius  
  - Drift displacement  
  - Motion type (circular, helical, drift)

# Deliverables

✔ A complete Python + Markdown simulation notebook  
✔ Visuals of trajectories under varying fields  
✔ Explanatory analysis connecting theory to real-world systems  
✔ Proposed extensions:  
  - Time-varying or spatially varying fields  
  - Relativistic effects (v ~ c)  
  - Multi-particle or charged cloud dynamics

# Hints & Tools

• Integration: Euler or Runge-Kutta  
• Libraries: NumPy for math, Matplotlib for plots  
• Start simple → progress to complex (e.g., uniform B → crossed E×B)  
• Useful checks:  
  - Is radius consistent with r = mv/qB?  
  - Is energy conserved (if no 𝐄 field)?

# Final Notes
This simulation bridges theoretical electromagnetism and real-world systems.  
The trajectories modeled here illustrate the rich dynamics induced by Lorentz force, critical in:

 • Charged particle confinement  
 • Mass filtering  
 • Plasma diagnostics 