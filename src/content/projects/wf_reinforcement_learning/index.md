---
title: "Reinforcement Learning for Wind Farm Control"
description: "Reinforcement learning is applied to a LES wind farm environment to find dynamic control stratagies for improving power output."
date: "Jun 30 2025"
demoURL: "https://www.youtube.com/watch?v=NJFQGfBdixs"
repoURL: "https://github.com/admole/Wind-RL"
---

## Overview

Modern wind farms typically operate each turbine independently, maximising local power production without considering the impact on neighbouring turbines. This often leads to wake interactions that reduce the overall energy output of the farm.

This project developed a **deep reinforcement learning (RL) controller** capable of dynamically coordinating multiple wind turbines using real-time flow information from high-fidelity simulations. By learning collaborative wake steering strategies, the controller increased total wind farm power production by over **4%**, substantially outperforming conventional static control approaches.

![rl gif](/portfolio/RL.gif)

---

## The Challenge

Wind turbine wakes create regions of reduced wind speed and increased turbulence downstream.

Traditional control strategies typically fall into two categories:

* **Greedy control** – each turbine maximises its own power output.
* **Static wake steering** – fixed yaw angles are optimised for a given wind condition.

While static optimisation can improve performance, it cannot respond to atmospheric turbulence or dynamic interactions between the turbine wakes.

The goal of this project was to develop a controller capable of making continuous decisions based on the evolving flow field and coordinating all turbines simultaneously.

![3 turbine diagram](/portfolio/3_turbine_diagram.png)

---

## Methodology

### Reinforcement Learning

The control problem was formulated as a **Markov Decision Process**.

At each control interval:

1. The controller receives flow measurements from the wind farm.
2. It selects yaw angles for all turbines.
3. The wind farm evolves according to the flow physics.
4. A reward is computed from the total farm power output.
5. The controller updates its policy to maximise long-term reward.

Over time, the agent learns coordinated strategies that improve overall energy production rather than individual turbine performance.

![Diagram of wind farm control by reinforcement learning](/portfolio/WindFarm_RL_Diagram.png)

---

## High-Fidelity Training Environment

Unlike many wind farm control studies that rely on reduced-order wake models, this work trained the controller directly within a **high-fidelity Large Eddy Simulation (LES)** environment.

The simulations used:

* Three aligned 5 MW turbines
* Turbine diameter of 126 m
* Atmospheric boundary layer inflow

The LES environment was implemented using the [**Winc3D**](https://www.turbulencesimulation.com/uploads/5/8/7/2/58724623/2020_laizet_we.pdf) framework, enabling turbulence-resolving simulations of wind farm wake dynamics.

---

## Controller Design

### State Representation

The controller observes the wind farm state using wind velocity measurements distributed throughout the flow field which give a partial observation of the turbulent flow field. These are representative of the measurements available through LiDAR Measurements.

### Action Space

The agent controls the yaw angle of each turbine through setting the angular velocity. Actions are updated every **10 seconds of simulated time**, allowing the controller to respond continuously to evolving wake behaviour.

### Learning Algorithm

The reinforcement learning controller was implemented using the soft actor-critic technique for continuous control that allows for:

* Continuous action spaces
* Policy optimisation
* Experience replay
* Parallelised environment sampling

Training was performed on high-performance computing infrastructure using 32 parallel running LES environments each using 128 CPU cores.

![sac training](/portfolio/sac_training.png)


### Code Coupling

[SmartSim and SmartRedis](https://github.com/CrayLabs/SmartSim) were used to enable the efficient communication between the RL controller and multiple simulation environments running across multiple nodes in parallel on HPC.

![smartsim](/portfolio/smartsim.png)
---

## Baseline Control Strategies

The RL controller was compared against several established approaches:

#### Greedy Operation

* Standard industrial control strategy
* Each turbine maximises individual power production
* No coordination between turbines

#### Static Optimal Wake Steering

* Fixed yaw angles
* Obtained using Bayesian optimisation
* Optimised for average conditions

#### Wind-Direction-Based Dynamic Control

* Dynamic yaw scheduling
* Based on global wind measurements
* Optimised using Bayesian optimisation

These baselines provided a benchmark for evaluating the benefits of flow-responsive RL control.

---

## Key Results

### Increased Wind Farm Power

The reinforcement learning controller achieved:

| Control Strategy               | Power Improvement |
| ------------------------------ | ----------------- |
| Static Optimal Yaw Control     | 2.19%             |
| Dynamic Wind-Direction Control | 2.67%             |
| Reinforcement Learning Control | **4.30%**         |

The RL controller nearly doubled the gains achieved using static optimal wake steering.

![rl power](/portfolio/RL_power.png)

---

### Emergent Collaborative Behaviour

One of the most interesting outcomes was that the controller learned coordinated behaviour between turbines without being explicitly programmed.

The learned strategy:

* Adapted to turbulent fluctuations
* Coordinated yaw actions between turbines
* Exploited wake interactions dynamically
* Responded to evolving flow conditions

Rather than following a fixed control law, the controller continuously adjusted turbine settings based on the current state of the wind farm.

![rl gif](/portfolio/RL.gif)

---

### Flow-Responsive Control

Analysis of the learned policies showed that the controller was not simply reproducing static wake steering.

Instead it learned to:

* React to instantaneous wake motion
* Anticipate downstream interactions
* Exploit transient flow structures
* Maintain higher-power operating states for longer periods

This demonstrates the value of combining reinforcement learning with turbulence-resolving simulations.

![gusts](/portfolio/gusts.png)

---


## Impact

This work demonstrates that reinforcement learning can discover dynamic, collaborative control strategies that outperform conventional wind farm optimisation methods.

By training directly within high-fidelity turbulence-resolving simulations, the controller learned to exploit flow structures and wake interactions that are inaccessible to traditional reduced-order control approaches.

The methodology provides a foundation for future:

* Autonomous wind farm operation
* Real-time flow control
* Digital twins
* AI-assisted renewable energy systems
* Net-zero energy optimisation

The results show that machine learning can unlock additional renewable energy generation from existing infrastructure without requiring new physical assets.

---

## Publication

[**Mole, A., Weissenbacher, M., Rigas, G., & Laizet, S. (2026)**
*Reinforcement Learning Increases Wind Farm Power Production by Enabling Closed-Loop Collaborative Control*](https://doi.org/10.1038/s44172-026-00667-8)

