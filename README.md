# Geothermal Heat Transfer Modeling Using Slender Body Theory (SBT)

## Project Overview

Developed a Python-based numerical heat-transfer model using Slender Body Theory (SBT) to simulate transient heat conduction in geothermal systems. Recreated four benchmark configurations from Koenraad F. Beckers' research, including single and interacting cylinders, a geothermal slinky with fluid advection, and square and rectangular borehole grids. The project demonstrates how reduced-order mathematical modeling can substantially accelerate long-term geothermal simulations compared with conventional finite-element methods.

## Theory

Slender Body Theory approximates transient heat transfer around elongated geometries whose radius is small relative to their length and the thermal diffusion length. The geometry is discretized into centerline elements, and the temperature field is constructed by matching an inner solution representing an infinite cylindrical source with an outer solution formed through Green's function superposition.

The resulting temperature–heat-flux relationship is expressed as a system of linear equations:

$$\mathbf{T}=\mathbf{F}\mathbf{Q}$$

where \(\mathbf{F}\) is the thermal response matrix constructed from Green's functions, \(\mathbf{Q}\) represents the heat fluxes, and \(\mathbf{T}\) represents the corresponding temperature response. Solving this system enables efficient prediction of transient thermal behavior across different geothermal geometries.

## How It Was Built

Developed a Python reduced-order heat-transfer solver by discretizing cylindrical and helical geometries into centerline elements and constructing matrix-based systems of discrete Green's functions. Implemented **Fourier-number-based decision trees** to select appropriate analytical approximations and eliminate negligible thermal interactions, reducing matrix computation without sacrificing benchmark accuracy. Exploited geometric symmetry and block-matrix structure to minimize redundant calculations across multiple interacting boreholes.

Extended the solver to model coupled conduction and fluid convection in a geothermal slinky by incorporating thermal resistance relationships and historical heat-pulse contributions. Implemented backward Euler time integration with first-order upwind spatial discretization to solve the fluid advection equation and predict outlet temperatures. Validated numerical outputs against published benchmarks using RMSE and MAE statistical error analysis.

## Results

**Single Cylinder:** Simulated approximately 31 years of transient heat transfer using 10 centerline elements and 150 logarithmically spaced time steps, achieving an RMSE of 2.848 W and MAE of 0.406 W against published benchmark results.

**Two Interacting Cylinders:** Modeled coupled thermal interactions using symmetric block matrices, completing the simulation in 27 seconds with an RMSE of 2.407 W and MAE of 0.69 W.

**Geothermal Slinky:** Simulated coupled conductive and advective heat transfer over approximately 115 days using 30 helical pipe elements, achieving an outlet-temperature RMSE of 1.122°C and MAE of 0.558°C in approximately 2 minutes and 47 seconds.

**Borehole Grids:** Extended the algorithm to square and rectangular multi-borehole configurations, exploiting matrix symmetry to achieve simulation runtimes of 37 and 33 seconds, respectively. Verified convergence toward the two-cylinder benchmark behavior at large borehole separations.

## Technologies

Python, NumPy, SciPy, Pandas, Matplotlib, Slender Body Theory, Discrete Green's Functions, Numerical Linear Algebra, Block-Matrix Optimization, Fourier-Number Asymptotics, Backward Euler, Upwind Discretization, Transient Heat Transfer, Statistical Error Analysis.

## Research Reference

[Slender-body theory for transient heat conduction — Koenraad F. Beckers](https://royalsocietypublishing.org/rspa/article/471/2184/20150494/57825/Slender-body-theory-for-transient-heat-conduction)
