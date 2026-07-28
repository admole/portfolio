---
title: "Multi-Fidelity Optimisation of Wind Farms"
description: "A multi-fidelity Bayesian optimisation method is applied to wind farm wake steering for increasing the power output."
date: "Mar 18 2024"
demoURL: "https://www.youtube.com/watch?v=NJFQGfBdixs"
repoURL: "https://github.com/admole/Wind-RL"
---

![Diagram of wind farm control by reinforcement learning](/over_iso.gif)

Wake steering aims to optimise turbine yaw angles to redirect wakes and maximise the overall power production of the wind farm.


## Wind Farm Simulation Fidelities
![wind farm fidelities](/WindFarm_fidelities.png)
Multiple approaches of calculating the wake interactions in a wind farm are available with diffent associated costs and accuracy.

## Multi-fidelity Bayesian optimiastion
![multi-fidelity model](/MF_WindFarm.png)
Multi-fidelity Bayesian optimiastion process is built based on a non-linear autoregressive Gaussian Process model and an acquisition function to select the next experiment configuration and fidelity.


## Optimisation Result
![result of bo](/BO_result.png)
Combining LES simulations and analytical wake models in a multi-fidelity bayesian optimisation framework allows cheap experiments to inform the optimal placement of expensive experiments that find improved yaw steering strategies.

