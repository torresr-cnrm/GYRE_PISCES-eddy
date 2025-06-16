# Using an energy-constrained mesoscale eddy parameterisation in NEMO5 (Part 1)

This tutoroial is about mesoscale eddy parameterisation available in NEMO version 5. In particular, it focuses on the eddy-induced circulation of [Gent and McWilliams, 1990](https://doi.org/10.1175/1520-0485(1990)020%3C0150:IMIOCM%3E2.0.CO;2), hereafter GM, that represents the eddy buoyancy flux due to baroclinic instability processes. This parameterisation is often used by climate and global ocean models as in the sixth phase of the Coupled Model Intercomparison Project (CMIP6) while large uncertainties persist in the specification of the coefficient involved in the GM scheme, $$\kappa_{gm}$$. NEMO5 allows for different approaches for setting the values of $$\kappa_{gm}$ from the simple constant case to physically-based formulations allowing space and time variations of the eddy coefficient. This page focuses on the latter case, in which NEMO offers two different formulations. 

In this tutorial, you will learn :
* how to set-up and run an idealised gyre configuration (GYRE_PISCES) with two different specifications for $\kappa_{gm}$
  - the default one which uses a formulation based on the baroclinic instability theory and scales with an estimation of the Eady growth rate following [Tréguier et al., 1997](link)
  - GEOMETRIC that employs a prognostic eddy energy equation to inform the GM coefficient [Mak et al., 2022](link)
* how to set  configuration from a restart file (spin-up)
* how to compare two mesoscale parameterisations and their effect on the simulations
–basic XIOS file manipulation to add variables in the output
–Python scripts for plotting variables
