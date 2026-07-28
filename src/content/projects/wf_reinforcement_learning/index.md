---
title: "Reinforcement Learning for Dynamic Wind Farm Control"
description: "Reinforcement learning is applied to a LES wind farm environment to find dynamic control stratagies for improving power output."
date: "Mar 18 2024"
demoURL: "https://www.youtube.com/watch?v=NJFQGfBdixs"
repoURL: "https://github.com/admole/Wind-RL"
---

![Diagram of wind farm control by reinforcement learning](/WindFarm_RL_Diagram.png)

Wake steering aims to optimise turbine yaw angles to redirect wakes and maximise the overall power production of the wind farm.

Our approach uses reinforcement learning to train control policies that adapt dynamically to varying wind conditions.

By coupling an RL controller with a high-fidelity wind farm simulation environment, this framework learns optimal wake control strategies that dynamically adjust based on the wind conditions and increases the power output of the wind farm.

## SmartSim
![smartsim](/smartsim.png)
SmartSim and SmartRedis are used to couple the Fortran wind farm simulations with the Python RL code. This allows for multiple environments to run in parallel on HPC efficiently.

## Active Controller 
![rl gif](/RL.gif)
The RL agent learns a dynamic control stratagy that responds to fluctautions in the turbulent wind conditions. 

## Power Increase
![rl power](/RL_power.png)
The active RL controller gives 2x the power increase that a staticly optimised stratagy yeilds. 

