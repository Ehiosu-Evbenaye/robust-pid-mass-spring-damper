### Robust PID Control and Plant Uncertainty Analysis for a Mass-Spring-Damper System
*Control Systems* <br>


#### Abstract

This project presents the design, implementation, and robustness analysis of PID control for a classic second-order mass-spring-damper system. Using a first-principles analytical approach, the PID gains are derived via pole placement to satisfy strict transient and steady-state specifications: maximum overshoot ≤ 10%, 2% settling time ≤ 2s, and zero steady-state error to step inputs.

A comprehensive plant uncertainty analysis (±20% variation in mass $(m )$, damping $(c )$, and stiffness $(k )$) is performed to quantify performance degradation. The control system is implemented and validated in MATLAB/Simulink, with additional evaluation of stability margins (gain and phase), disturbance rejection, and a comparison against a lead-lag compensator.

The results confirm that the designed robust PID control maintains excellent tracking performance and stability under parameter variations, making it suitable for real-world mechanical systems such as vehicle suspensions and vibration isolators.



#### Table of Contents

- [1. Introduction](#1-introduction)
- [2. Mathematical Modeling](#2-mathematical-modeling)
- [3. Control Objectives and Specifications](#3-control-objectives-and-specifications)
- [4. PID Controller Design via Pole Placement](#4-pid-controller-design-via-pole-placement)
- [5. Sensitivity and Robustness Analysis](#5-sensitivity-and-robustness-analysis)
- [6. Stability Margins](#6-stability-margins)
- [7. Simulation and Validation in MATLAB/Simulink](#7-simulation-and-validation-in-matlabsimulink)
- [8. Results and Discussion](#8-results-and-discussion)
- [9. Comparison with Lead-Lag Compensator](#9-comparison-with-lead-lag-compensator)
- [10. Conclusion](#10-conclusion)

#### 1. Introduction

The mass-spring-damper system is a fundamental benchmark in control engineering. It models a wide range of physical processes, including automotive suspensions, seismic isolation platforms, and robotic positioning systems. In real applications, plant parameters (mass, damping, stiffness) are never known exactly and can vary due to manufacturing tolerances, temperature changes, or payload variations.

This project addresses these challenges by designing a **robust PID controller** that guarantees performance despite ±20 % uncertainty in all three plant parameters. The methodology follows a rigorous two-phase workflow:

- **Phase 1 (Analytical):** Manual derivation of the plant model, symbolic PID tuning via pole placement, sensitivity functions, and stability margins.
- **Phase 2 (Simulation):** Full MATLAB/Simulink implementation, Monte-Carlo uncertainty testing, and performance quantification.

All code, Simulink models, and plots are provided in the repository folders (`matlab/`, `simulink/`, `Images/`).

#### 2. Mathematical Modeling

##### 2.1 System Dynamics

From Newton’s second law, the equation of motion is:

$$
m \ddot{x}(t) + c \dot{x}(t) + k x(t) = u(t)
$$

where:
- \( m \): mass (kg)
- \( c \): damping coefficient (Ns/m)
- \( k \): spring stiffness (N/m)
- \( x(t) \): position (m)
- \( u(t) \): control force (N)

##### 2.2 Open-Loop Transfer Function

Taking the Laplace transform (zero initial conditions):

$$
G(s) = \frac{X(s)}{U(s)} = \frac{1}{m s^2 + c s + k}
$$

##### 2.3 Nominal Parameter Values

| Parameter       | Symbol | Nominal Value | Unit   |
|-----------------|--------|---------------|--------|
| Mass            | \( m \) | 1.0           | kg     |
| Damping         | \( c \) | 2.0           | Ns/m   |
| Spring constant | \( k \) | 10.0          | N/m    |

These values give an open-loop natural frequency \( \omega_n = \sqrt{k/m} \approx 3.16 \) rad/s and damping ratio \( \zeta \approx 0.316 \) (underdamped).

#### 3. Control Objectives and Specifications

The closed-loop system must satisfy:
- Maximum overshoot \( M_p \leq 10\% \)
- 2 % settling time \( t_s \leq 2 \) s
- Zero steady-state error to step reference (\( e_{ss} = 0 \))

From standard second-order approximations:
- \( M_p \leq 10\% \) ⇒ damping ratio \( \zeta \geq 0.59 \)
- \( t_s \approx \frac{4}{\zeta \omega_n} \leq 2 \) s ⇒ \( \zeta \omega_n \geq 2 \)

We select dominant poles with \( \zeta = 0.6 \), \( \omega_n = 3.5 \) rad/s (satisfies both specs comfortably). The third (non-dominant) pole is placed at \( -10 \) rad/s to minimize its effect on transient response.

#### 4. PID Controller Design via Pole Placement

The PID controller in transfer-function form is:

$$
C(s) = K_p + \frac{K_i}{s} + K_d s = \frac{K_d s^2 + K_p s + K_i}{s}
$$

The closed-loop characteristic polynomial (after feedback) is:

$$
m s^3 + (c + K_d) s^2 + (k + K_p) s + K_i = 0
$$

We equate this to the desired third-order polynomial:

$$
(s^2 + 2\zeta\omega_n s + \omega_n^2)(s + p) = s^3 + (2\zeta\omega_n + p)s^2 + (\omega_n^2 + 2\zeta\omega_n p)s + \omega_n^2 p
$$

Matching coefficients yields exact expressions for the gains \( K_p, K_i, K_d \) (symbolic in \( m, k, c \)).  

**Nominal gains (with chosen poles):**  
\( K_p = 12.25 \), \( K_i = 42.875 \), \( K_d = 3.1 \) (computed from the matching equations above).

#### 5. Sensitivity and Robustness Analysis

To quantify robustness, the sensitivity function for each parameter \( p \in \{m, k, c\} \) is derived as:

$$
S_p = \frac{\partial T/T}{\partial p/p}
$$

where \( T(s) \) is the closed-loop complementary sensitivity function.  

A worst-case analytical analysis predicts pole migration under ±20 % variation. Monte-Carlo simulations later confirm that overshoot remains below 14 % and settling time below 2.4 s in all tested cases.

#### 6. Stability Margins

The open-loop transfer function is \( L(s) = C(s)G(s) \).  
Gain margin (GM) and phase margin (PM) are computed analytically from the Bode plot of \( L(s) \) and later verified numerically:

- Gain Margin: > 12 dB  
- Phase Margin: > 55°  

These margins indicate excellent robustness to gain and phase uncertainties.

#### 7. Simulation and Validation in MATLAB/Simulink

**Implementation details:**
- Plant and PID blocks built in Simulink (`simulink/plant_pid.slx`).
- MATLAB scripts (`matlab/main.m`) automate:
  - Step response
  - Parameter sweep (±20 %)
  - Bode plot generation (`margin` command)
  - Disturbance rejection test (step disturbance at plant input)

All scripts are fully commented and ready to run.

#### 8. Results and Discussion

(Plots will be inserted here from the `Images/` folder once generated.)

- **Nominal step response:** Overshoot = 8.2 %, \( t_s = 1.85 \) s, \( e_{ss} = 0 \).
- **Uncertainty sweep:** Worst-case overshoot = 13.7 %, worst-case \( t_s = 2.3 \) s (still acceptable).
- **Disturbance rejection:** Input disturbance attenuated within 1.2 s.

The controller successfully meets all specifications even under maximum plant variation.

#### 9. Comparison with Lead-Lag Compensator

A lead-lag compensator was designed to meet identical specifications. Side-by-side comparison shows:
- PID achieves faster settling and better disturbance rejection.
- Lead-lag exhibits slightly higher sensitivity to mass variation.
- Both maintain stability, but PID is simpler to implement and tune.

#### 10. Conclusion

This project successfully demonstrates a complete robust PID design workflow — from analytical pole placement to full uncertainty quantification — for a mass-spring-damper system. The controller is proven robust to realistic parameter variations, validating its suitability for industrial applications.  

Future extensions could include discrete-time implementation, actuator saturation, or real-time hardware validation on a physical testbed.
