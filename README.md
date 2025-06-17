# Energy-constrained mesoscale eddy parameterisations in NEMO5 (Part 1: The Gyre Test Case)

This article provides an overview of mesoscale eddy parameterisation available in NEMO version 5. This tutorial is designed for beginners who want to get introduced to eddy parameterisations and learn how to set up NEMO experiments in order to compare available parameterisations. 

* __Prerequisites__: Install [NEMO v5.0.1](https://forge.nemo-ocean.eu/nemo/nemo/-/releases/5.0.1) or later; [XIOS2](https://forge.ipsl.jussieu.fr/ioserver/svn/XIOS2/trunk) and other dependencies (HDF5, NETCDF-C). For the following, you'll need to be able to compile and run a NEMO experiment on your environment (either local or remote).   
* __Objectives__: To introduce mesoscale eddy parameterisations in NEMO, and allow users to test them in a simple test case.

## Overview

In this tutorial, you will :
* set-up and run an idealised gyre configuration (GYRE_PISCES).
* restart different experiments from an initial state, that can be used as a benchmark for eddy parameterisations. 
* modify the configuration namelist in order to set-up mesoscale eddy parameterisations. 
* basic XIOS file manipulation to add extra variables in output files.
* compare your simulation outputs in order to assess the impact of eddy parameterisation choices on the ocean state.

## Mesoscale parameterisations in NEMO

In particular, it focuses on the eddy-induced circulation of [Gent and McWilliams, 1990](https://doi.org/10.1175/1520-0485(1990)020%3C0150:IMIOCM%3E2.0.CO;2), hereafter GM, that represents the eddy buoyancy flux due to baroclinic instability processes. This parameterisation is often used by climate and global ocean models as in the sixth phase of the Coupled Model Intercomparison Project (CMIP6) while large uncertainties persist in the specification of the coefficient involved in the GM scheme, $$\kappa_{gm}$$. NEMO5 allows for different approaches for setting the values of $$\kappa_{gm}$$ from the simple constant case to physically-based formulations allowing space and time variations of the eddy coefficient. This page focuses on the latter case, in which NEMO offers two different formulations. 

  - the default one which uses a formulation based on the baroclinic instability theory and scales with an estimation of the Eady growth rate following [Tréguier et al., 1997](link)
  - GEOMETRIC that employs a prognostic eddy energy equation to inform the GM coefficient [Mak et al., 2022](link)
