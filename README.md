# Smart Flight Autopilot Simulator

A physics-based altitude control simulation that implements a **Proportional-Integral-Derivative (PID)** control loop to stabilize aircraft flight profiles under stochastic environmental conditions.

## ✈️ Project Overview
This project simulates a commercial flight path from **Des Moines (DSM) to Chicago (ORD)**. It features a full mission profile—Takeoff, Cruise, and Landing—while managing atmospheric disturbances such as turbulence and wind drift.

### Key Technical Features
* **Velocity-Commanded PID Loop:** Utilizes a PID controller to generate target climb rates rather than raw acceleration, ensuring smoother transitions.
* **Stochastic Weather Engine:** Models real-time atmospheric noise using NumPy-based uniform distributions to simulate "Clear," "Windy," and "Storm" conditions.
* **Aeronautical Constraints:** Enforces realistic climb limits (±3,000 ft/min) and implements a first-order lag filter ($\alpha = 0.08$) to simulate aircraft inertia.
* **Telemetry Logging:** High-fidelity data pipeline using Pandas to record 60Hz flight states for post-flight stability analysis.

---

## 📊 Performance Analysis

The simulation achieved a **critically damped response**, effectively eliminating the "runaway" divergence seen in early prototypes.

| Phase | Duration | Controller Behavior |
| :--- | :--- | :--- |
| **Takeoff** | 0 - 900 steps | Smooth exponential ramp to target altitude. |
| **Cruise** | 900 - 2400 steps | Steady-state stability at 35,000 ft with <1% overshoot. |
| **Landing** | 2400 - 3000 steps | Controlled descent with active damping against wind drift. |



---

## 🛠️ Engineering Challenges & Solutions

### 1. Resolving System Divergence
**Challenge:** Initial models used raw PID output to modify acceleration, leading to exponential overshoot and "unstable rocket" behavior (exceeding 70,000+ ft).
**Solution:** Refactored the architecture to a **Velocity-Commanded** model. Added **Integrator Clamping** to prevent windup and **Output Clamping** to enforce a physical limit of 3,000 ft/min.

### 2. Simulating Inertia
**Challenge:** The digital controller was "too perfect," causing jerky, unrealistic movements.
**Solution:** Implemented a **First-Order Lag Filter** ($\alpha = 0.08$) to ensure the climb rate changes gradually, successfully simulating the mass of a commercial aircraft.

---



---

## 🎓 About the Author
Developed by **Shres**, a Master's student in Computer Science at **Iowa State University**. This project serves as a practical application of **Control Theory** and **System Architecture** principles.
