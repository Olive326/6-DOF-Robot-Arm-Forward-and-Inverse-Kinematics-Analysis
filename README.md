# 6-DOF Robot Arm: Forward and Inverse Kinematics Analysis
## Overview
Comprehensive kinematic analysis of a 6 DOF robotic manipulator implementing both forward and inverse kinematics methods in MATLAB

## Forward Kinematics

### Approach
Computed end-effector position from joint angles using the Denavit-Hartenberg convention and homogeneous transformation matrices.

### Implementation
1.Derived DH parameters(link lengths, twist engles, offsets) from robot geometry
2.Applied 4x4 homogeneous transformation matrics combining rotation and translation
3.Computed complete transformation:

### Trajectory Generation
Generated smooth oscillating motion with 650 waypoints:
```
θ₂(t) = 20° + 30°·sin(t)     (shoulder oscillation)
θ₃(t) = -40° + 25°·sin(2t)   (elbow at double frequency)
```
### Results:
- Average waypoint spacing:1.06 mm
- Successfully maintained fixed end-effector orientation
- Demonstrated nonlinear joint-to-task space mapping

---

## Inverse Kinematics

### Approach
Implemented Newton’s iteration method with Jacobian-based updates to compute joint angles for desired end-effector positions.

### Why newton’s method?
Works for any robot configuration(no geometric constrains)
Handles 6-DOF complexity without closed-form solutions

### Algorithms:
For each waypoints:
1. Compute error: e= desired_pose- current_pose
2.Calculate Jacobian (6x6 matrix)
3.Update joints: Δθ = (J'J + λI)⁻¹J'e  (damped least squares)
4.Repeat until error < 0.001mm

### Test case:
Square trajectory with 400 waypoints in Cartesian space(100mm sides, 1mm spacing).

### Results: 

### Key Insight:** Using previous waypoint’s solution guess reduced convergence from 50 to just 3 iterations for most waypoints.

## Demo & Documentation
**Video Demo:**[YouTube Animation]([https://youtu.be/BIbAoDZN7so?si=KMd5PT8OXu11Swr])
**Full Report:**

