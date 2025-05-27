# Problem 1

# Measuring Earth's Gravitational Acceleration with a Pendulum

## **Motivation:**
The acceleration due to gravity, $g$, is a fundamental constant that influences a wide range of physical phenomena. Measuring $g$ accurately is crucial for understanding gravitational interactions, designing structures, and conducting experiments in various fields. One classic method for determining $g$ is through the oscillations of a simple pendulum, where the period of oscillation depends on the local gravitational field.

## **Task:**
Measure the acceleration due to gravity using a pendulum and in detail analyze the uncertainties in the measurements.

This exercise emphasizes rigorous measurement practices, uncertainty analysis, and their role in experimental physics.

## **Procedure:**

### 1. **Materials:**
- A string (1 or 1.5 meters long).
- A small weight (e.g., bag of coins, bag of sugar, key chain) mounted on the string.
- Stopwatch (or smartphone timer).
- Ruler or measuring tape.

### 2. **Setup:**
- Attach the weight to the string and fix the other end to a sturdy support.
- Measure the length of the pendulum, $L$, from the suspension point to the center of the weight using a ruler or measuring tape. Record the resolution of the measuring tool and calculate the uncertainty as half the resolution: 
  $$ \Delta L = \frac{\text{Ruler Resolution}}{2} $$

### 3. **Data Collection:**
- Displace the pendulum slightly ($\theta \leq 15^\circ$) and release it.
- Measure the time for 10 full oscillations ($T_{10}$) and repeat this process 10 times. Record all 10 measurements.
- Calculate the mean time for 10 oscillations ($\overline{T_{10}}$) and the standard deviation ($\sigma_T$).
- Determine the uncertainty in the mean time as:
  $$ \Delta T_{10} = \frac{\sigma_T}{\sqrt{n}} $$
  where $n = 10$.

## **Calculations:**

### 1. **Calculate the Period:**
The period $T$ is given by the formula:
$$ T = \frac{T_{10}}{10} \quad \text{and} \quad \Delta T = \frac{\Delta T_{10}}{10} $$

### 2. **Determine $g$:**
Using the formula for the acceleration due to gravity:
$$ g = \frac{4\pi^2L}{T^2} $$

### 3. **Propagate Uncertainties:**
The uncertainty in $g$ is given by:
$$ \Delta g = g \left( \frac{\Delta L}{L} \right)^2 + \left( \frac{2 \Delta T}{T} \right)^2 $$

## **Analysis:**

### 1. **Compare your measured $g$** with the standard value $9.81 \, \text{m/s}^2$.

### 2. **Discuss:**
- The effect of measurement resolution on $\Delta L$.
- Variability in timing and its impact on $\Delta T$.
- Any assumptions or experimental limitations.

## **Python Code Version of the Simulation**

![alt text](image.png)

```python
import numpy as np
import matplotlib.pyplot as plt

# Define constants
L = 1.5  # length of the pendulum in meters
n = 10  # number of oscillations
g_standard = 9.81  # standard value for g in m/s^2

# Sample data for T_10 (in seconds)
T_10 = np.array([19.8, 19.9, 20.1, 19.7, 19.9, 20.0, 19.8, 19.9, 19.7, 19.8])

# Calculate the mean and standard deviation of T_10
mean_T10 = np.mean(T_10)
std_T10 = np.std(T_10)

# Calculate the period T
T = mean_T10 / n
delta_T = std_T10 / np.sqrt(n)

# Calculate g
g = (4 * np.pi**2 * L) / T**2

# Propagate uncertainties
delta_L = 0.01  # Assuming ruler resolution uncertainty (1 cm)
delta_g = g * (delta_L / L)**2 + (2 * delta_T / T)**2

# Output results
print(f"Calculated g: {g:.4f} m/s^2")
print(f"Uncertainty in g: {delta_g:.4f} m/s^2")

# Plotting the data for T_10
plt.hist(T_10, bins=5, edgecolor='black')
plt.title('Distribution of T_10 Measurements')
plt.xlabel('Time for 10 Oscillations (s)')
plt.ylabel('Frequency')
plt.show()

```





## **Deliverables:**
The following should be provided in markdown format:
- $L$, $\Delta L$, $T_{10}$ measurements, $\overline{T_{10}}$, $\sigma_T$, $\Delta T$.
- Calculated $g$ and $\Delta g$.
- The discussion on sources of uncertainty and their impact on the results.


