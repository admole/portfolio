---
title: "Multi-Fidelity Surrogate Modelling"
description:  "Developing a multi-fidelity surrogate modelling framework for application to CFD data from RANS and LES."
date: "Dec 01 2022"
demoURL: "https://www.youtube.com/watch?v=NJFQGfBdixs"
repoURL: "https://github.com/admole/Multi-Fidelity-Surrogate"
---


## Overview

High-fidelity Computational Fluid Dynamics (CFD) methods such as Large Eddy Simulation (LES) can provide highly accurate predictions of complex turbulent flows, but they are computationally expensive. Lower-cost approaches such as Reynolds-Averaged Navier–Stokes (RANS) simulations can explore a wider design space but often miss important flow physics.

This project developed a **multi-fidelity machine learning framework** that combines the strengths of both approaches, using a small number of expensive LES simulations alongside a larger database of RANS results to create accurate surrogate models of aerodynamic flow behaviour. The work was published in *Flow, Turbulence and Combustion* and demonstrated on the challenging case of turbulent flow around tandem wall-mounted cubes.

---

## The Challenge

Engineering design often requires understanding how flow behaviour changes as operating conditions vary.

Traditionally this means:

* Running many CFD simulations across a parameter space
* Using expensive high-fidelity methods for accuracy
* Accepting significant computational cost

In this study, the parameter of interest was **inlet yaw angle**, with flow conditions varying between 0° and 30°. LES accurately captured the underlying flow structures, while RANS provided a cheaper but less accurate approximation.

![tandem cube geometry](/tandem_cube_geometry.png)

---

## Methodology

### Multi-Fidelity Learning

The surrogate model learns the relationship between:

* **Low-fidelity data (LF):** RANS simulations
* **High-fidelity data (HF):** LES simulations

Rather than learning directly from LES alone, the model uses predictions from the low-fidelity model as additional features when predicting the high-fidelity solution.

Conceptually:

$$ \text{Prediction}_{HF} = \mathcal{F}(\text{Prediction}_{LF}, \text{Input Parameters})$$



___This allows the model to learn the non-linear mapping between RANS and LES solutions and exploit information contained in both datasets.___

### Machine Learning Models

Two surrogate modelling approaches were investigated:

#### Gaussian Process Regression (MF-GPR)

* Probabilistic surrogate model
* Provides uncertainty estimates
* Effective with limited training data
* Uses Matérn-based covariance kernels

#### Multi-Layer Perceptrons (MF-MLP)

* Neural-network-based surrogate model
* Learns highly non-linear LF→HF relationships
* Hyperparameters optimised using cross-validation
* Trained using L-BFGS optimisation with L2 regularisation

![multi-fidelity regression](/MFR.png)

---

## CFD Dataset

### High-Fidelity Simulations

* Large Eddy Simulation (LES)
* ~32 million cells
* OpenFOAM implementation
* 7 yaw-angle configurations
* 4 used for training, 3 reserved for testing

### Low-Fidelity Simulations

* RANS with k-ω SST turbulence model
* 21 yaw-angle configurations
* 2° parameter spacing
* Approximately 2–3 million cells per simulation

The large difference in computational cost between LES and RANS makes this an ideal test case for multi-fidelity modelling.

---

## Key Results

### Predicting Global Flow Quantities

The first stage focused on predicting:

* Drag coefficient of the downstream cube
* Local velocity probe measurements

The multi-fidelity models consistently outperformed equivalent single-fidelity models, accurately predicting flow behaviour at yaw angles not included in the LES training set.

![multi-fidelity probe](/MFR_probe.png)

---

### Reconstructing Velocity Profiles

The framework was extended from scalar outputs to **multi-target regression**, enabling prediction of entire velocity profiles rather than individual quantities.

Key features:

* 183 velocity targets predicted simultaneously
* Correlations between outputs retained
* Improved reconstruction of flow structures
* Accurate interpolation between sparse LES samples

### Figure Placeholder

*Predicted velocity profiles compared against LES validation data*

---

### Predicting Two-Dimensional Flow Fields

The final stage scaled the approach to full spatial flow fields.

For each flow condition:

* 63,140 velocity values were predicted simultaneously
* Velocity slices were reconstructed at unseen yaw angles
* Major wake structures and recirculation regions were reproduced accurately
* Results closely matched LES while requiring only surrogate inference time

![multi-fidelity slice](/MFR_slice.png)

---

## Technical Highlights

* Python-based machine learning workflow
* Scikit-Learn implementation
* Gaussian Process Regression
* Multi-Layer Perceptron neural networks
* Multi-target regression
* Multi-fidelity information fusion
* OpenFOAM CFD simulations
* LES and RANS turbulence modelling
* Automated hyperparameter optimisation
* Surrogate modelling for reduced-order aerodynamic prediction

---

## Impact

This work demonstrates how machine learning can bridge the gap between expensive high-fidelity simulations and practical engineering design workflows.

By combining sparse LES data with extensive RANS datasets, the resulting surrogate models achieve near-LES accuracy while dramatically reducing the computational cost required to explore a design space. The methodology is applicable to aerodynamic optimisation, uncertainty quantification, digital twins, and real-time engineering analysis.

---

## Publication

[**Mole, A., Skillen, A., & Revell, A. (2023)**
*Multi-Fidelity Surrogate Modelling of Wall Mounted Cubes*
Flow, Turbulence and Combustion, 110, 835–853.](https://doi.org/10.1007/s10494-022-00391-1)

