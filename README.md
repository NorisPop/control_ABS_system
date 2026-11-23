# ABS Control Using Linear Controllers and Fuzzy Logic

Design and comparison of linear and fuzzy controllers for an Anti-lock Braking System (ABS), developed in MATLAB/Simulink.

**Course:** Automatic Control Engineering II, Technical University of Cluj-Napoca (Faculty of Automation and Computer Science), academic year 2025–2026.

## Goal

Keep the wheel slip at an optimal reference value of **0.2** during braking, avoiding wheel lock-up and loss of traction. The wheel–road interaction is strongly nonlinear, so the project compares classical linear controllers with a nonlinear fuzzy controller.

## Specifications

* Sampling time: `Ts = 0.01 s`
* Control signal (brake): limited to the range 0–1 with a Saturation block
* Target: reach the steady-state slip of 0.2 with low overshoot and bring the vehicle safely to a stop

## Method

1. **System identification**

   * Input/output data (Brake and Slip, along with Drive, VCar and VWheel) was acquired from the Simulink ABS test bench over an 8 s simulation.
   * The data was trimmed to the relevant transient and split 70% for identification and 30% for validation.
   * ARX, OE and Box-Jenkins models were compared. The **OE model** was selected with a **95.38% fit** and validated with the Compare and Resid tools.
   * The resulting discrete model was a second-order system with a small dead time (about 0.02 s).
2. **Linear controllers**

   * **Guillemin-Truxal:** designed from a second-order ideal model (10% max overshoot, 1.5 s response time).
   * **Kalman (deadbeat):** designed with the polynomial method for a minimum-time response.
3. **Fuzzy controller (Mamdani)**

   * One input (slip error) and one output (brake command).
   * Two variants were tested:

     * **Variant 1 (conservative):** smooth braking, but the vehicle kept rolling at low speed.
     * **Variant 2 (tuned):** more sensitive error range and a stronger "Maintain" brake level, which brought the vehicle to a complete stop in longer simulations.

## Results

* The linear controllers (Kalman and Guillemin-Truxal) struggled with the nonlinear behavior at low speeds, showing command saturation and virtual wheel lock.
* The fuzzy controller gave smoother braking and handled the instability spike that appears at low vehicle speed, where the slip equation divides by a value close to zero.
* Tuning the fuzzy rules was what allowed the vehicle to stop completely.

## Tools

MATLAB \& Simulink (2024), Control System Toolbox, System Identification Toolbox, Fuzzy Logic Toolbox.

## 

