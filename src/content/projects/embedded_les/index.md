---
title: "Embedded Large Eddy Simulations"
description: "Developing a nested Embedded Large Eddy Simulation approach for turbulent flow simulations."
date: "Mar 18 2024"
demoURL: "https://www.youtube.com/watch?v=NJFQGfBdixs"
repoURL: "https://github.com/admole/Wind-RL"
---

![ELES Cube](/ELES_cube.png)
Coupling together RANS and LES approaches on seperate meshes. This allows for the high-fidelity scale resolved LES to be focussed only in regions where it is needed.

## Nested Framework
![ELES Diagram](/ELES.png)
LES nested within larger RANS domain Synthetic eddy method used for LES inlet Drift terms introduced to correct the RANS downstream of LES

## Testing Synthetic Eddy Method
![vortices in boundary layer](/vortices.png)
Tested on boundary layer flow containing multiple vortices

## Tandem Cubes
![ELES Diagram](/ELES_cube.png)
    path: ELES_cube.png
Confining the LES region to a small part of the domain and coupling in both directions
