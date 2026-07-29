---
title: "Nuclear Cooling by Natural Convection"
description: "Developing a 1D-3D multifidelity framework for application to the simulation of natural convection flow."
date: "Jun 30 2023"
demoURL: "https://www.youtube.com/watch?v=NJFQGfBdixs"
repoURL: "https://github.com/admole/Wind-RL"
---



## Overview

As part of a research collaboration with **Rolls-Royce** and the **University of Manchester**, I investigated methods for combining fast one-dimensional thermal-hydraulic system models with three-dimensional Computational Fluid Dynamics (CFD) simulations. The project focused on improving the prediction of natural convection flows in nuclear reactor cooling systems while maintaining computational efficiency.

Alongside developing a novel coupling framework between systems codes and CFD, the project also explored **multi-fidelity surrogate modelling**, combining low-cost system simulations with high-fidelity CFD to efficiently predict complex flow behaviour across a design space.

![Natural Convection Loop](/portfolio/cooling_loop.png)
---

## The Challenge

Natural convection cooling systems are critical to many advanced nuclear reactor designs.

Two complementary simulation approaches are commonly used:

* **Systems codes** provide fast one-dimensional predictions of pressure, flow rate and temperature throughout an entire reactor system.
* **CFD** resolves the full three-dimensional flow field, capturing local phenomena such as recirculation and thermal stratification.

Each approach has limitations:

* Systems codes are computationally efficient but cannot resolve local flow physics.
* CFD provides much greater fidelity but is prohibitively expensive for whole-system analysis.

This project investigated how both approaches could be combined to obtain accurate predictions at practical computational cost.

![3D-1D Coupling](/portfolio/3D-1D.png)

---

## Methodology

### Dual Systems–CFD Coupling

Rather than dividing the computational domain between the two solvers, a **domain-overlapping coupling strategy** was developed.

Both models represent the entire cooling loop simultaneously:

* **Simcenter AMESim** predicts system-level thermal hydraulics.
* **STAR-CCM+** resolves the three-dimensional flow field.
* Information is exchanged continuously between the two models using source terms.

The coupling allows the systems code to guide the CFD solution in regions where the flow is well understood, while the CFD provides improved predictions in regions with complex flow behaviour.

![3D-1D Coupling](/portfolio/systems_couple.png)

---

## Novel Source-Term Coupling

A key contribution of the project was the development of new source terms for the CFD equations.

Unlike conventional approaches that impose uniform boundary conditions, the proposed method:

* Preserves the existing three-dimensional velocity profile.
* Corrects bulk momentum using systems-code predictions.
* Couples temperature between the two solvers.
* Avoids reconstructing complex inlet profiles from one-dimensional data.

The source terms were implemented within **STAR-CCM+** using user-defined functions and applied to both the momentum and energy equations.


$$ S_m = \frac{U}{|U|} \frac{|U|}{U_{b}}  \left(|U_b^{sys}| - |U_b|\right) $$

---

## Validation Cases

The methodology was evaluated using progressively more complex test cases.

### Straight Pipe Flow

The first validation considered turbulent flow through a straight pipe.

This simple case demonstrated that the momentum source term:

* Corrected the bulk flow rate.
* Preserved the velocity profile.
* Improved agreement with DNS reference data.

Importantly, the three-dimensional flow structure remained unchanged while the bulk quantities converged towards the systems-code solution.

![pipe mesh](/portfolio/pipe_mesh.png)
![pipe profile](/portfolio/pipe_profile.png)


### Industrial Test Facility

The methodology was finally extended to a realistic natural convection test facility representative of industrial reactor cooling systems.

This demonstrated the practical challenges of deploying coupled CFD simulations on high-performance computing systems, including:

* Distributed solver execution
* Data communication between software packages
* HPC workflow integration

The coupled simulations demonstrated stable interaction between CFD and the systems model while accurately reproducing the thermal behaviour of the loop.
The work highlighted both the potential and the engineering challenges associated with large-scale coupled simulations.

![test facility result](/portfolio/test_facility.png)
---

## Multi-Fidelity Surrogate Modelling

The second part of the project investigated machine learning techniques for combining systems-code and CFD data.

The objective was to predict high-fidelity CFD behaviour using:

* Dense low-cost systems-code simulations
* Sparse high-fidelity CFD simulations

Gaussian Process Regression (GPR) was used to construct **multi-fidelity surrogate models** capable of learning the relationship between the two simulation fidelities.

---

## Mixed-Dimensional Learning

Unlike conventional surrogate modelling, the two simulation fidelities produced outputs with different dimensionality:

* Systems code → one-dimensional bulk quantities
* CFD → spatially resolved flow fields

Analytical test cases demonstrated that the multi-fidelity framework could successfully combine these heterogeneous datasets, reconstructing detailed flow fields with substantially lower prediction error than either single-fidelity model alone.

![mixed dimensional surrogate](/portfolio/MDMF.png)

---

## Impact

This project demonstrated two complementary approaches for accelerating high-fidelity thermal-fluid simulations.

The first introduced a novel overlapping coupling framework that enables one-dimensional systems codes and three-dimensional CFD simulations to operate together while preserving local flow structures. The second showed how multi-fidelity machine learning can combine sparse CFD data with inexpensive systems-code simulations to accurately predict complex flow behaviour across a parameter space.

Together, these methods offer a pathway towards faster and more accurate analysis of advanced nuclear cooling systems, reducing computational cost while retaining the fidelity needed to capture critical thermal-hydraulic phenomena.

