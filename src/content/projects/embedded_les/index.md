---
title: "Embedded Large Eddy Simulations"
description: "Developing a nested Embedded Large Eddy Simulation approach for turbulent flow simulations."
date: "Jan 01 2021"
demoURL: "https://www.youtube.com/watch?v=NJFQGfBdixs"
repoURL: "https://github.com/admole/myELES"
---

## Overview

Large Eddy Simulation (LES) provides highly accurate predictions of turbulent flows but remains prohibitively expensive for many engineering applications. This project investigated **Embedded Large Eddy Simulation (ELES)**, a hybrid CFD approach that combines Reynolds-Averaged Navier–Stokes (RANS) and LES within a single computational framework, applying high-fidelity turbulence modelling only where it is needed.

The work focused on developing an embedded LES methodology in **OpenFOAM**, implementing synthetic turbulence generation at the RANS–LES interface, and validating the approach on both canonical turbulent channel flow and the complex separated flow around tandem wall-mounted cubes.

![ELES Diagram](/ELES_cube.png)
---

## The Challenge

Many engineering flows contain only small regions where LES is truly required.

Examples include:

* Separated wakes
* Shear layers
* Recirculation regions
* Strong vortex interactions

While RANS provides an efficient prediction of the overall flow, it often struggles to reproduce the large turbulent structures that dominate these regions. Running LES across the entire computational domain is significantly more accurate but can require an order of magnitude more computational resources.

Embedded LES aims to bridge this gap by resolving turbulence only within regions of interest while retaining RANS elsewhere.

---

## Methodology

### Embedded Large Eddy Simulation

The computational domain is divided into two simulation regions:

* **RANS region** – predicts the upstream flow efficiently.
* **LES region** – resolves large turbulent structures where increased fidelity is required.

Rather than changing turbulence models globally, the LES region is embedded within the RANS solution.

```text
Full-Domain RANS
        ↓
Extract Mean Flow Statistics
        ↓
Synthetic Turbulence Generation
        ↓
Embedded LES Region
        ↓
Resolved Turbulent Flow
```

This approach concentrates computational effort where it provides the greatest improvement in solution accuracy.

![ELES Diagram](/ELES.png)


---

## RANS–LES Interface

A key challenge in ELES is generating realistic turbulent fluctuations at the interface between the two simulation regions.

The upstream RANS solution provides:

* Mean velocity
* Reynolds stresses
* Turbulence length scales

These quantities are used to initialise the LES region through an enhanced **Synthetic Eddy Method (SEM)**, allowing resolved turbulence to develop rapidly while maintaining consistency with the upstream solution.

The methodology was implemented within **OpenFOAM**, providing a flexible framework for hybrid turbulence simulations.

![SEM Diagram](/sem.png)

---

## Code Coupling

Two seperate instances of the OpenFOAM solver were used to solve the RANS and LES regions. These could be independently set up to use a combination of independent RANS or LES turbulence models and solver settings. 

This requires a copling of the two  solvers which was implemented using the PreCICE coupling libary to exchange the required information between the solvers.

![PreCICE Diagram](/precice.png)


---

## Validation: Turbulent Channel Flow

The first stage of the project validated the methodology using fully developed turbulent channel flow.

This canonical benchmark allowed the performance of the interface treatment to be assessed independently of complex flow separation.

The study evaluated:

* Mean velocity profiles
* Reynolds stress distributions
* Turbulence development downstream of the interface
* Recovery length required for fully developed turbulence

The embedded LES accurately reproduced reference DNS statistics while demonstrating stable transition from the RANS inflow to fully resolved turbulence.

### Figure Placeholder

*Comparison of channel flow velocity and Reynolds stress profiles*
![ELES Channel](/eles_channel.png)

---

## Application: Flow Around Tandem Cubes

Following validation, the methodology was applied to the turbulent flow around tandem wall-mounted cubes.

This configuration presents several challenges:

* Flow separation
* Large recirculation regions
* Strong vortex shedding
* Complex wake interactions

The LES region was positioned downstream of the cubes, where large turbulent structures dominate the flow.

Compared with conventional RANS, the embedded LES captured:

* Improved wake development
* More realistic vortex structures
* Better prediction of recirculation regions
* Reduced numerical dissipation
* 
The embedded LES reproduced the key flow features while requiring significantly less computational effort than a full-domain LES simulation.

![ELES Cube](/eles_cube_2.png)

---

## Technical Highlights

* Embedded Large Eddy Simulation (ELES)
* Reynolds-Averaged Navier–Stokes (RANS)
* Large Eddy Simulation (LES)
* OpenFOAM
* Synthetic Eddy Method (SEM)
* Hybrid turbulence modelling
* Turbulent channel flow
* Bluff body aerodynamics
* Wake prediction
* High-performance computing

---

## Key Results

### Accurate Turbulence Development

The embedded LES successfully generated resolved turbulence downstream of the RANS interface, producing accurate turbulence statistics in the channel flow validation case.

### Improved Wake Prediction

For the tandem cube simulations, the methodology significantly improved predictions of separated flow compared with RANS alone, capturing coherent turbulent structures and wake dynamics that are essential for accurate aerodynamic analysis.

### Computational Efficiency

By restricting LES to regions where it provides the greatest benefit, the embedded approach substantially reduced computational cost relative to full-domain LES while retaining much of its predictive capability.

---

## Impact

This work demonstrates that Embedded LES offers an effective compromise between the speed of RANS and the accuracy of LES. By combining both approaches within a single simulation, it becomes possible to resolve complex turbulent flow structures without the prohibitive computational cost associated with full-domain LES.

The methodology provides a practical route towards higher-fidelity CFD for engineering applications involving separated turbulent flows, wake dynamics and bluff-body aerodynamics.

---

## Research Outputs

**Embedded Large Eddy Simulation Methodology Development**

Research on hybrid RANS–LES coupling, synthetic turbulence generation and validation using turbulent channel flow and tandem wall-mounted cubes.

