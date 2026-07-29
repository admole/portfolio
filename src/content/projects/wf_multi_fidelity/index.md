---
title: "Multi-Fidelity Optimisation of Wind Farms"
description: "A multi-fidelity Bayesian optimisation method is applied to wind farm wake steering for increasing the power output."
date: "Jun 30 2024"
demoURL: "https://www.youtube.com/watch?v=NJFQGfBdixs"
repoURL: "https://github.com/admole/Wind-RL"
---


## Overview

Wind turbines operating in the wake of upstream turbines experience lower wind speeds, reduced power output, and increased structural loading. Wake steering aims to mitigate these losses by intentionally yawing turbines to redirect wakes away from downstream machines.

This project developed a **multi-fidelity Bayesian optimisation framework** that combines fast analytical wake models with high-fidelity Large Eddy Simulations (LES) to identify optimal turbine control strategies. The approach achieves optimisation results comparable to LES-only methods while significantly reducing computational cost.

![yaw-animation](/portfolio/over_iso.gif)

---

## The Challenge

Wind farm control is fundamentally an optimisation problem:

> How should each turbine be yawed to maximise total farm power output?

Analytical wake models can evaluate thousands of turbine configurations quickly but simplify many important flow physics.

High-fidelity LES captures:

* Turbine wake interactions
* Atmospheric boundary layer effects
* Wake recovery mechanisms
* Non-linear flow behaviour

However, LES is too computationally expensive to evaluate every candidate design during optimisation.

![wind farm fidelities](/portfolio/WindFarm_fidelities.png)

---

## Methodology

### Multi-Fidelity Bayesian Optimisation

The framework combines:

* **Low-fidelity (LF):** Analytical wake models
* **High-fidelity (HF):** Large Eddy Simulations
* **Surrogate Model:** Non-linear Auto-Regressive Gaussian Process (NARGP)
* **Optimiser:** Bayesian Optimisation (BO)

Rather than treating the two simulation fidelities independently, the model learns the non-linear relationship between them and determines which fidelity should be evaluated at each optimisation step. This allows expensive LES evaluations to be used only where they provide the greatest benefit.

![multi-fidelity model](/portfolio/MF_WindFarm.png)

---

## Wind Farm Models

### Low-Fidelity Environment

Analytical wake models were implemented using FLORIS.

Three wake modelling approaches were investigated:

#### Jensen Wake Model

* Simple engineering wake model
* Uniform velocity deficit
* Very low computational cost
* Suitable for rapid optimisation

#### Gaussian Wake Model

* Smooth wake deficit distribution
* Improved wake interaction modelling
* More realistic wake recovery

#### Gauss-Curl Hybrid (GCH)

* Includes wake rotation effects
* Captures yaw-induced wake behaviour
* Models secondary steering effects
* Highest-fidelity analytical model tested

---

### High-Fidelity Environment

The high-fidelity simulations were performed using the **Winc3D** wind farm solver based on **XCompact3D**.

Key features:

* Large Eddy Simulation (LES)
* Actuator disc turbine representation
* Atmospheric boundary layer modelling
* Turbine-to-turbine wake interactions resolved directly

LES provides substantially more accurate predictions of wake behaviour but at a much higher computational cost than analytical wake models.

![adm 3d](/portfolio/3d_ADM.png)

---

## Bayesian Optimisation

Bayesian optimisation is particularly effective when:

* Function evaluations are expensive
* The design space is relatively small
* The objective function is unknown

For each optimisation iteration:

1. A Gaussian Process surrogate predicts farm power output.
2. An acquisition function estimates where information is most valuable.
3. The optimiser selects the next turbine yaw configuration.
4. The framework chooses whether to evaluate it using a wake model or LES.

This adaptive strategy focuses computational effort where it delivers the largest improvement in optimisation performance.

![bosteps](/portfolio/bo_steps.png)

---

## Test Cases

### Two-Turbine Wake Steering

The framework was first validated on a simple two-turbine configuration.

Objectives:

* Compare wake model and LES optima
* Assess surrogate accuracy
* Evaluate optimisation efficiency

The results demonstrated that the multi-fidelity framework successfully identified LES-level optimal yaw settings using significantly fewer LES evaluations than a purely high-fidelity optimisation.

---

### Multi-Turbine Wind Farm

The methodology was then extended to a more realistic wind farm layout involving multiple interacting wakes.

Challenges included:

* Higher-dimensional control space
* Strong wake interactions
* Increased non-linearity
* Larger optimisation search domain

Despite the increased complexity, the framework maintained optimisation performance while reducing the number of expensive LES simulations required.

![result of bo](/portfolio/BO_result.png)

---


## Key Results

### Improved Optimisation Efficiency

The multi-fidelity framework:

* Reduced the number of LES evaluations required
* Maintained optimisation quality
* Accelerated convergence towards optimal solutions

### Better Physical Fidelity

Compared with optimisation using analytical wake models alone:

* More realistic wake interactions were captured
* Additional flow physics influenced the optimum
* Improved turbine control strategies were identified

### Reduced Computational Cost

By selectively combining wake model evaluations with LES simulations, the framework achieved LES-quality optimisation outcomes at a fraction of the computational expense.

---

## Impact

This work demonstrates how modern machine learning and optimisation techniques can bridge the gap between engineering wake models and high-fidelity CFD.

The methodology enables more accurate wind farm control optimisation without requiring the prohibitive computational cost of LES only optimisation, making high-fidelity flow physics more accessible for practical wind energy applications.

Potential applications include:

* Wind farm operational control
* Real-time optimisation frameworks
* Digital twins
* Renewable energy system design
* Multi-fidelity engineering optimisation

---

## Publication

[**Mole, A. & Laizet, S. (2025)**
*Multi-Fidelity Bayesian Optimisation of Wind Farm Wake Steering using Wake Models and Large Eddy Simulations*
Flow, Turbulence and Combustion, 115, 1209–1234.](https://doi.org/10.1007/s10494-024-00629-0)

