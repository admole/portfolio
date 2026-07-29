---
title: "Multi-Physics Wind Farm Optimisation"
description: "Multi-objective wind farm optimisation using high-fidelity multiphysics simulations that combine LES with structural modelling to increase power and minimise fatigue."
date: "Jun 30 2026"
demoURL: "https://www.youtube.com/watch?v=NJFQGfBdixs"
repoURL: "https://github.com/markhorn-dev/astro-sphere"
---


[description: "High-fidelity coupled fluid structure simulations for wind turbines."]:#
[description: "Developing a high-fidelity optimisation framework that combines large eddy simulations, aeroelastic modelling, and Bayesian optimisation to maximise wind farm power production while reducing structural fatigue."]:#

## Overview

This ongoing project investigates how **high-fidelity computational simulations** can be combined with **Bayesian optimisation** to improve wind farm operation. Rather than optimising solely for energy production, the competing objectives of increasing power output while reducing structural fatigue on wind turbine blades are considered.

By integrating turbulent flow simulation, structural dynamics, and optimisation on high performance computing (HPC) systems, a single automated workflow is capable of evaluating complex wind farm control strategies.

![Wind Turbine Video](/portfolio/wt.gif)

---

## The Challenge

Wind turbine wakes reduce the wind speed available to downstream turbines while increasing turbulence intensity, leading to lower power production and higher fatigue loading.

A common control strategy is **wake steering**, where upstream turbines are intentionally yawed away from the wind to redirect their wakes. Although this can improve overall wind farm efficiency, yaw misalignment also changes the aerodynamic loading on the blades and may increase long term structural fatigue.

Understanding this trade off requires simulations that resolve both:

- atmospheric turbulence and wake dynamics
- structural deformation of flexible wind turbine blades

while remaining computationally feasible for optimisation.

![ALM BeamDyn](/portfolio/alm_beamdyn.png)

---

## High-Fidelity Simulation Framework

The project couples several advanced simulation tools into a fully automated multiphysics workflow.


### Large Eddy Simulation (LES) 

The atmospheric flow is simulated using [**Xcompact3d**](https://www.incompact3d.com/), a high-order finite-difference CFD solver that resolves turbulent structures using Large Eddy Simulation (LES).

The simulations include:

- realistic atmospheric boundary layer inflow
- actuator line modelling of wind turbines
- wake interaction between turbines
- yaw-controlled turbine operation

### Fluid-Structure Interaction

Rather than assuming rigid blades, the aerodynamic model is coupled to [**BeamDyn**](https://openfast.readthedocs.io/en/dev/source/user/beamdyn/index.html), allowing the blades to deform under aerodynamic loading.

![FSI Diagram](/portfolio/fsi_diagram.png)

This two-way fluid-structure interaction captures how blade flexibility influences the aerodynamic forces, wake development and power generation whilst enabling calculation of the fatigue loading. This provides a more realistic representation of turbine behaviour than conventional rigid-blade models.


![slices of wind around turbines](/portfolio/3t_slices.png)

---

## Multi-Objective Bayesian Optimisation

Each LES-FSI simulation requires substantial HPC resources, making exhaustive parameter searches impractical.

To address this, the project employs **Multi-Objective Bayesian Optimisation** using Gaussian Process surrogate models implemented with [**BoTorch**](https://botorch.org/).

The optimisation seeks Pareto-optimal yaw control strategies that balance:

- maximising total wind farm power output
- minimising structural fatigue and maintenance requirements

By intelligently selecting new simulation points using Expected Hypervolume Improvement, the optimiser dramatically reduces the number of expensive simulations required.

![MOBO](/portfolio/mobo.png)


---

## HPC Automation

A significant software engineering component of the project was developing an automated optimisation pipeline capable of running entirely on an HPC cluster.

I developed a Python framework that bridges **BoTorch** with **Slurm**, allowing optimisation iterations to execute automatically by:

- generating simulation configurations
- submitting LES-FSI jobs to the cluster
- monitoring job status
- collecting simulation outputs
- extracting objective values
- updating Gaussian Process models
- selecting the next optimal simulation

This automation enables long-running optimisation campaigns involving many computationally expensive simulations with minimal manual intervention.

---

## Technologies

- BoTorch (PyTorch)
- Xcompact3d
- BeamDyn
- Multi-Objective Bayesian Optimisation
- Large Eddy Simulation (LES)
- Fluid-Structure Interaction (FSI)
- Slurm Workload Manager
- High Performance Computing (HPC)

---

## Current Status

🚧 **Ongoing Research**


