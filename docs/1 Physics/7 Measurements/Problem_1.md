# Problem 1


# Measuring Earth's Gravitational Acceleration with a Pendulum

## Motivation:

The acceleration **$g$** due to gravity is a fundamental constant that influences a wide range of physical phenomena. Measuring **$g$** accurately is crucial for understanding gravitational interactions, designing structures, and conducting experiments in various fields. One classic method of determining **$g$** is through the oscillations of a simple pendulum, where the period of oscillation depends on the local gravitational field.

## Task:

Measure the acceleration **$g$** due to gravity using a pendulum and in detail analyze the uncertainties in the measurements.

This exercise emphasizes rigorous measurement practices, uncertainty analysis, and their role in experimental physics.

## Procedure:

### 1. Materials:
- A string (1 or 1.5 meters long).
- A small weight (e.g., bag of coins, bag of sugar, key chain) mounted on the string.
- Stopwatch (or smartphone timer).
- Ruler or measuring tape.

### 2. Setup:
- Attach the weight to the string and fix the other end to a sturdy support.
- Measure the length of the pendulum, $L$, from the suspension point to the center of the weight using a ruler or measuring tape. Record the resolution of the measuring tool and calculate the uncertainty as half the resolution:  
  $$\Delta L = \frac{\text{Ruler Resolution}}{2}$$

### 3. Data Collection:
- Displace the pendulum slightly ($<$15°) and release it.
- Measure the time for 10 full oscillations ($T_{10}$) and repeat this process 10 times. Record all 10 measurements.
- Calculate the mean time for 10 oscillations ($\bar{T}_{10}$) and the standard deviation ($\sigma_T$).
- Determine the uncertainty in the mean time as:

  $$\Delta T_{10} = \frac{\sigma_T}{\sqrt{n}}$$

where $n = 10$.

## Calculations:

1. Calculate the period:

$$
T = \frac{\bar{T}_{10}}{10} \quad \text{and} \quad \Delta T = \frac{\Delta T_{10}}{10}
$$

2. Determine $g$:

$$
g = \frac{4 \pi^2 L}{T^2}
$$

3. Propagate uncertainties:

$$
\Delta g = g \sqrt{\left(\frac{\Delta L}{L}\right)^2 + \left(2 \frac{\Delta T}{T}\right)^2}
$$

## Analysis:

1. Compare your measured **$g$** with the standard value (9.81 m/s$^2$).

2. Discuss:
- The effect of measurement resolution on $\Delta L$.
- Variability in timing and its impact on $\Delta T$.
- Any assumptions or experimental limitations.

## Deliverables:

1. Tabulated data in markdown:

- $L$, $\Delta L$, $T_{10}$ measurements, $\bar{T}_{10}$, $\sigma_T$, $\Delta T$.
- Calculated $g$ and $\Delta g$.

2. Discussion on sources of uncertainty and their impact on results.

---

## Python Script

![alt text](image.png)

```python
import numpy as np
import pandas as pd

# Constants
n = 10  # Number of trials

# Input data
# Length of pendulum (meters)
L = 1.00
ruler_resolution = 0.01  # 1 cm resolution, realistic

# Calculate uncertainty in length
delta_L = ruler_resolution / 2

# Time measurements for 10 oscillations (seconds)
T10_measurements = np.array([20.15, 20.22, 20.18, 20.21, 20.19, 20.17, 20.20, 20.16, 20.23, 20.18])

# Calculate mean and standard deviation
T10_mean = np.mean(T10_measurements)
sigma_T = np.std(T10_measurements, ddof=1)

# Calculate uncertainty in mean time
delta_T10 = sigma_T / np.sqrt(n)

# Calculate period and its uncertainty
T = T10_mean / 10
delta_T = delta_T10 / 10

# Calculate gravitational acceleration g
g = (4 * np.pi**2 * L) / T**2

# Propagate uncertainty for g
delta_g = g * np.sqrt((delta_L / L)**2 + (2 * delta_T / T)**2)

# Prepare tabulated data
data = {
    'Trial': np.arange(1, n + 1),
    'T10 (s)': T10_measurements,
}

df = pd.DataFrame(data)

# Summary data
summary = {
    'Pendulum Length (L)': L,
    'Uncertainty in Length (ΔL)': delta_L,
    'Mean Time for 10 Oscillations (T10_mean)': T10_mean,
    'Standard Deviation (σ_T)': sigma_T,
    'Uncertainty in Mean Time (ΔT10)': delta_T10,
    'Period (T)': T,
    'Uncertainty in Period (ΔT)': delta_T,
    'Gravitational Acceleration (g)': g,
    'Uncertainty in g (Δg)': delta_g
}

summary_df = pd.DataFrame(summary, index=[0])

# Display dataframes
print("Individual Measurements of T10:")
print(df)
print("\nSummary of Calculations:")
print(summary_df)

# Optionally export to markdown file
with open("pendulum_results.md", "w") as f:
    f.write("# Pendulum Experiment Results\n\n")
    f.write("## Individual Measurements of $T_{10}$ (seconds)\n")
    f.write(df.to_markdown(index=False))
    f.write("\n\n## Summary\n")
    f.write(summary_df.to_markdown(index=False))
