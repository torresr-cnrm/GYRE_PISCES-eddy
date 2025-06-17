# Mesoscale eddy parameterisations in NEMO5

This page introduces the approach used in NEMO to parameterise the transport of tracers induced be unresolved mesoscale eddies in the ocean. 
In particular, the tutorial focuses on the scheme of [Gent and McWilliams, 1990](https://doi.org/10.1175/1520-0485(1990)020%3C0150:IMIOCM%3E2.0.CO;2), hereafter GM, that represents the eddy buoyancy flux due to baroclinic instability processes.
In this page, we recall the basic formulation of the GM parameterisation, its expected behaviour and the main options available in NEMO5 to constrain the parameterised eddy flux.

> **NOTE:**  Users familiar with the GM scheme and its implementation in NEMO5 can skip this theoretical section and can [set-up the spin-up](spin_up.md) directly.

## The Gent and McWilliams parameterisation

This parameterisation is quite often used by climate and global ocean models as in the sixth phase of the Coupled Model Intercomparison Project (CMIP6) while large uncertainties persist in the specification of the coefficient involved in the GM scheme, $$\kappa_{gm}$$. NEMO5 allows for different approaches for setting the values of $$\kappa_{gm}$$ from the simple constant case to physically-based formulations allowing space and time variations of the eddy coefficient. This page focuses on the latter case, in which NEMO offers two different formulations.

### Tréguier et al. (1997)

### The GEOMETRIC parameterisation (Mak et al., 2022)

## Summary
