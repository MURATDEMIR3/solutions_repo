# Problem 1# Interference Patterns on a Water Surface

<<<<<<< HEAD
##  Motivation

Interference occurs when waves from different sources overlap, creating new patterns. On a water surface, this can be clearly observed when ripples from different points meet, forming distinctive interference patterns. These patterns can show how waves combine in different ways — sometimes reinforcing each other, other times canceling each other out.

Studying these patterns helps us understand wave behavior in a simple, visual way. It also allows us to explore important concepts, like the relationship between wave phase and the effects of multiple sources. This task offers a hands-on approach to learning about wave interactions and their real-world applications, making it an interesting and engaging way to dive into wave physics.

---

##  Task

A circular wave on the water surface, emitted from a point source located at (x₀, y₀), can be described by the **Single Disturbance equation**:

    η(x, y, t) = A / √r * cos(k * r - ω * t + φ)

where:

- η(x, y, t) is the displacement of the water surface at position (x, y) and time t  
- A is the amplitude of the wave  
- k = 2π / λ is the wave number (related to wavelength λ)  
- ω = 2π * f is the angular frequency (related to frequency f)  
- r = √[(x - x₀)² + (y - y₀)²] is the distance from the source to point (x, y)  
- φ is the initial phase of the wave  

---

##  Problem Statement

Your task is to analyze the interference patterns formed on the water surface due to the superposition of waves emitted from point sources placed at the vertices of a chosen regular polygon.

---

##  Steps to Follow

1. Select a Regular Polygon (e.g., triangle, square, pentagon)
2. Position the sources at the vertices of the polygon.
3. Use the wave equation for each source.
4. Superimpose the waves using:

       η_sum(x, y, t) = Σ (from i=1 to N) ηᵢ(x, y, t)

5. Analyze the interference pattern as a function of position (x, y) and time t.
6. Visualize the constructive and destructive interference regions.

---

##  Considerations

- All wave sources have the same amplitude A, wavelength λ, and frequency f.  
- The waves are coherent, maintaining constant phase differences.  
- Use Python (with NumPy, Matplotlib) to simulate and visualize the wave field.

---

##  Python Implementation
![alt text](image.png)
```python
import numpy as np
import matplotlib.pyplot as plt

# --- Wave Parameters ---
A = 1              # Amplitude
λ = 1              # Wavelength
f = 1              # Frequency
k = 2 * np.pi / λ  # Wave number
ω = 2 * np.pi * f  # Angular frequency
φ = 0              # Phase
t = 0              # Time snapshot

# --- Grid Setup ---
x = np.linspace(-5, 5, 500)
y = np.linspace(-5, 5, 500)
X, Y = np.meshgrid(x, y)

# --- Source Setup (Regular Triangle) ---
R = 2  # Radius of polygon
N = 3  # Number of vertices (triangle)
angles = np.linspace(0, 2 * np.pi, N, endpoint=False)
sources = [(R * np.cos(θ), R * np.sin(θ)) for θ in angles]

# --- Superposition of Waves ---
η_sum = np.zeros_like(X)

for (x0, y0) in sources:
    r = np.sqrt((X - x0)**2 + (Y - y0)**2)
    η = A / np.sqrt(r + 1e-6) * np.cos(k * r - ω * t + φ)
    η_sum += η

# --- Plot Interference Pattern ---
plt.figure(figsize=(8, 6))
plt.pcolormesh(X, Y, η_sum, shading='auto', cmap='RdBu')
plt.colorbar(label='Wave Displacement')
plt.title('Interference Pattern from Triangle Wave Sources')
plt.xlabel('x')
plt.ylabel('y')
plt.axis('equal')
plt.tight_layout()
plt.show()
```

---

##  Results & Discussion

- **Constructive Interference**: Occurs where the wave crests align, resulting in amplified wave heights.
- **Destructive Interference**: Occurs where crests and troughs cancel each other out.
- **Pattern Shape**: The symmetry of the polygon is reflected in the wave pattern’s geometry.

This simulation demonstrates the importance of source geometry and phase relationships in wave interference phenomena.

---

##  Deliverables

1.  A complete Markdown file containing the full Python simulation code.
2.  Detailed explanation of how the interference patterns arise based on wave superposition.
3.  Graphical output clearly showing interference zones (constructive and destructive regions).


=======
>>>>>>> fc56fae598979e8ee515901a147b0ef0920b1c83