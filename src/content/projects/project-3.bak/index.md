---
title: Wind Farm Layout Optimisation
description: Bayesian optimisation for computationally expensive wind farm design.
date: 2025-01-01
draft: false
---

## Overview

Designing wind farms requires balancing competing objectives such as power production, structural loading, and construction cost. Evaluating a single design often requires expensive CFD simulations, making conventional optimisation techniques impractical.

This project investigates how Bayesian optimisation and surrogate modelling can dramatically reduce the number of expensive simulations required to identify high-performing designs.

---

## Problem

Traditional optimisation approaches become prohibitively expensive when each function evaluation requires minutes or hours of simulation time.

The main challenges were:

* Expensive black-box objective functions
* Limited simulation budget
* No analytical gradients
* High-dimensional design spaces
* Noisy simulation outputs

---

## Approach

I developed a Bayesian optimisation framework that combined Gaussian Process surrogate models with adaptive sampling strategies.

The workflow consisted of:

1. Running CFD simulations to generate initial training data
2. Training probabilistic surrogate models
3. Selecting new candidate designs using acquisition functions
4. Updating the surrogate as new simulations became available
5. Iterating until convergence

Several extensions were investigated, including:

* Multi-fidelity optimisation
* Batch Bayesian optimisation
* Constraint handling
* Multi-objective optimisation
* Parallel evaluation on HPC systems

---

## Technical Highlights

* Built optimisation framework in Python
* Integrated Gaussian Process models with simulation workflows
* Automated large-scale optimisation experiments
* Parallel execution on university HPC clusters
* Reproducible computational pipelines

---

## Technologies

| Category             | Tools            |
| -------------------- | ---------------- |
| Programming          | Python           |
| Machine Learning     | PyTorch, BoTorch |
| Scientific Computing | NumPy, SciPy     |
| Visualisation        | Matplotlib       |
| HPC                  | SLURM, Linux     |
| Version Control      | Git              |

---

## Results

Key outcomes included:

* Significant reduction in expensive simulation evaluations
* Improved optimisation efficiency compared with baseline methods
* Publications in optimisation and engineering journals
* Open, reproducible computational workflows

---

## What I Learned

This project strengthened experience in:

* Bayesian optimisation
* Scientific machine learning
* Probabilistic modelling
* High-performance computing
* Software engineering for research
* Experimental design

---

## Related Outputs

* 📄 PhD thesis
* 📄 Journal publications
* 💻 Source code (where available)
* 📊 Conference presentations

---

## Future Directions

Potential extensions include:

* Deep surrogate models
* Physics-informed neural networks
* Foundation models for engineering design
* AI-assisted simulation workflows

