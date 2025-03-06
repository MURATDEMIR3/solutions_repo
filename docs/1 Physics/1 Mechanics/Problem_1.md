# Problem 1
# Investigating the Range as a Function of the Angle of Projection

## Motivation
Projectile motion, while seemingly simple, offers a rich playground for exploring fundamental principles of physics. The problem is straightforward: analyze how the range of a projectile depends on its angle of projection. Yet, beneath this simplicity lies a complex and versatile framework. The equations governing projectile motion involve both linear and quadratic relationships, making them accessible yet deeply insightful.

What makes this topic particularly compelling is the number of free parameters involved in these equations, such as initial velocity, gravitational acceleration, and launch height. These parameters give rise to a diverse set of solutions that can describe a wide array of real-world phenomena, from the arc of a soccer ball to the trajectory of a rocket.

## Theoretical Foundation
To investigate projectile motion, we begin with the fundamental kinematic equations. Assuming no air resistance, the motion of the projectile can be described using the following equations:

- Horizontal displacement:
  \[ x = v_0 \cos(\theta) t \]
- Vertical displacement:
  \[ y = v_0 \sin(\theta) t - \frac{1}{2} g t^2 \]

where:
- \( v_0 \) is the initial velocity,
- \( \theta \) is the angle of projection,
- \( g \) is the acceleration due to gravity,
- \( t \) is the time elapsed.

To determine the time of flight, we solve for \( t \) when \( y = 0 \):
\[ t_f = \frac{2 v_0 \sin(\theta)}{g} \]

The range \( R \) (horizontal distance traveled) is then given by:
\[ R = \frac{v_0^2 \sin(2\theta)}{g} \]

## Analysis of the Range

From the equation of range, we observe:
- The range is maximized when \( \theta = 45^\circ \), since \( \sin(2\theta) \) reaches its peak value of 1 at \( 90^\circ \).
- Increasing \( v_0 \) increases the range quadratically.
- Increasing \( g \) decreases the range, making it inversely proportional to gravitational acceleration.
- Adding initial height would modify the time of flight, thus altering the range.

## Practical Applications
This model applies to various real-world situations:
- Sports physics (e.g., soccer, basketball, golf)
- Ballistics and defense applications
- Space launch trajectory calculations
- Engineering problems related to parabolic motion

To extend realism, we could incorporate factors such as air resistance, uneven terrain, or varying gravitational fields.

## Implementation
A Python script will be used to simulate projectile motion and visualize the range as a function of the angle of projection. We will plot the range for different values of \( v_0 \) and \( g \).

### Python Code (Sample Outline)

```python
import numpy as np
import matplotlib.pyplot as plt

def projectile_range(v0, g):
    angles = np.linspace(0, 90, 100)
    ranges = (v0**2 * np.sin(2 * np.radians(angles))) / g
    return angles, ranges

# Parameters
v0 = 20  # Initial velocity in m/s
g = 9.81  # Acceleration due to gravity (Earth)

# Compute range
angles, ranges = projectile_range(v0, g)

# Plot results
plt.figure(figsize=(8, 5))
plt.plot(angles, ranges, label=f'v0={v0} m/s')
plt.xlabel('Angle of Projection (degrees)')
plt.ylabel('Range (m)')
plt.title('Projectile Range vs. Angle of Projection')
plt.legend()
plt.grid()
plt.show()
```

## Discussion

### Limitations of the Idealized Model
- Ignores air resistance, which reduces range.
- Assumes flat ground, whereas real-world terrains vary.
- Assumes constant gravitational acceleration, which may not be valid for high-altitude launches.

### Possible Extensions
- Implementing drag force using differential equations.
- Modeling projectiles launched from different heights.
- Considering wind effects and varying gravitational fields.

## Deliverables
- A Markdown document containing the theoretical derivations and Python code.
- Graphical representations showing the dependence of range on projection angle.
- A discussion on the limitations and possible extensions of the model.



