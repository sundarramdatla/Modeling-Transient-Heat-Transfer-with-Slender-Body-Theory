# Geothermal Heat Transfer Modeling Using Slender Body Theory (SBT)

## Project Overview

Developed a Python-based reduced-order numerical model using Slender Body Theory (SBT) to simulate transient heat transfer in geothermal systems. The project applies recently published mathematical research to model single and interacting boreholes, slanted geometries, geothermal slinkies, and multi-borehole configurations with substantially lower computational costs than traditional finite-element simulations.

## Theory

Slender Body Theory approximates transient heat conduction around elongated geometries by matching an inner cylindrical temperature solution with an outer solution constructed from discrete Green's functions. Discretizing the geometry into centerline elements transforms the heat-transfer problem into a system of linear equations:

$$\mathbf{F}\mathbf{Q}=\mathbf{T}-\mathbf{H}$$

where \(\mathbf{F}\) is the Green's function thermal response matrix, \(\mathbf{Q}\) represents element heat fluxes, \(\mathbf{T}\) represents temperatures, and \(\mathbf{H}\) accounts for historical heat contributions.

For fluid-coupled systems, thermal resistance is incorporated to obtain:

$$(\mathbf{R}+\mathbf{F})\mathbf{Q}=\mathbf{T}_f-\mathbf{H}$$

where \(\mathbf{R}\) is a diagonal thermal resistance matrix and \(\mathbf{T}_f\) contains fluid temperatures.

## How It Was Built

Developed a Python numerical solver that discretizes vertical, slanted, and helical geothermal geometries into centerline elements and constructs Green's function response matrices using **Fourier-number-based decision trees**. Implemented analytical approximations for infinite and finite cylindrical and line sources, point-source approximations, and adaptive numerical quadrature to evaluate current and historical thermal interactions. Eliminated negligible interactions based on thermal diffusion length and exploited geometric symmetry to reduce redundant matrix calculations.

Extended the algorithm to simulate coupled conduction, convection, and fluid advection by incorporating pipe thermal resistance, Reynolds- and Prandtl-number-dependent Nusselt correlations, and historical heat-pulse superposition. Solved matrix systems using NumPy linear algebra and applied backward Euler time integration with first-order upwind spatial discretization to update fluid temperatures. Validated simulation outputs against published SBT benchmarks and independent TRNSYS simulations using Pandas interpolation, RMSE, MAE, and SMAPE.

## Results

**Single Cylinder:** Simulated 31 years of transient heat transfer using 150 logarithmically spaced time steps, achieving an RMSE of 2.848 W and MAE of 0.406 W against published SBT benchmarks.

**Two Interacting Cylinders:** Modeled coupled heat transfer using symmetric block matrices, completing simulations in 27 seconds with an RMSE of 2.407 W and MAE of 0.69 W.

**Geothermal Slinky:** Simulated approximately 115 days of coupled conductive and advective heat transfer, achieving outlet-temperature RMSE of 1.122°C and MAE of 0.558°C in approximately 2 minutes and 47 seconds.

**Borehole Grids:** Exploited geometric symmetry and reusable interaction coefficients to simulate square and rectangular borehole configurations in 37 and 33 seconds, respectively.

**Slanted Geothermal Boreholes:** Extended the SBT framework to slanted geothermal geometries, incorporating fluid convection correlations, thermal resistance, and transient heat-transfer modeling. Compared simulated heat-flux trajectories against TRNSYS reference data using time-series interpolation and SMAPE analysis.

## Technologies

Python, NumPy, SciPy, Pandas, Matplotlib, Slender Body Theory, Discrete Green's Functions, Numerical Linear Algebra, Matrix Optimization, Adaptive Quadrature, Backward Euler, Upwind Discretization, Heat Transfer, Statistical Error Analysis, TRNSYS.

## Research Reference

[Slender-body theory for transient heat conduction — Koenraad F. Beckers](https://royalsocietypublishing.org/rspa/article/471/2184/20150494/57825/Slender-body-theory-for-transient-heat-conduction)
