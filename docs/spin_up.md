# Set-up and run an idealised gyre configuration

This page is a guide to compile and run an idealised gyre configuration. 
Once installed, NEMO5 provides a suite of reference configurations in the _cfgs_ folder.

```
TODO: Explain the gyre test case here
```

```
TODO: Explain benchmark strategy here
```

Before going further, create a new git branch in order to not incorporate unwanted changes in the main branch:
```bash
git checkout -b tuto-gyre
git status
```
These commands will create and point to a new branch named 'tuto-gyre', and then display the working tree status associated to the current branch.

## Set-up the spin-up experiment

In the top-level NEMO folder, use the *makenemo* script to compile the configuration:
```bash
./makenemo -m 'auto' -n 'GYRE_PISCES' -j 2
```
This command compiles NEMO and stores buildt files in the *cfgs/GYRE_PISCES/BLD* folder. 
In particular, it creates an executable **cfgs/GYRE_PISCES/BLD/bin/nemo.exe** that will be used to run the model.

> **Note**: In this tutorial, we have used an auto

Test your installation by running the model:
```bash
cd cfgs/GYRE_PISCES/EXP00
./nemo &
```
You can follow how the simulation goes by printing the current iteration with `cat time.step`. 
When the iteration reaches _4320_, the simulation is finished. 
Results are stored in _GYRE\_\*\_grid\_\*.nc_ files.

We are now going to create a new experiment to activate the GM parameterisation and spin-up the model for 10 years:
1. Navigate and return to the configuration top-level folder: `cd .. & ls`. At this point, the folder structure should be as follow:
    ```bash
    BLD cpp_GYRE_PISCES_.fcm  EXP00  EXPREF  MY_SRC  WORK
    ```
2. Copy-paste the _EXPREF_ folder which contains links and configuration files with default settings to run the configuration.
    ```bash
    cp -R 'EXPREF' 'EXPSPIN'
    cd EXPSPIN
    ln -s ../BLD/bin/nemo.exe nemo
    ``` 
3. Now open the **namelist_cfg** file and edit the _&namrun_ section in order to have the following settings:
    ```vi
       nn_it000  = 1       !
       nn_itend  = 21600   !
       nn_leapy  = 30      !
       nn_stock  = 10800   !
       nn_write  = 30      !
    ```
4.  Still in the **namelist_cfg** file, add a new section after the _&namtra_ldf_ section, in order to activate the GM parameterisation:
    ```
    !-----------------------------------------------------------------------
    &namtra_eiv    !   eddy induced velocity param.                     
    !-----------------------------------------------------------------------
       ln_ldfeiv   = .true.        ! use eddy induced velocity parameterization
    ```
    This activates the default specification of the GM coefficient ($$\kappa_{gm}$$) which is constent all over the ocean domain with a value of $$2 000$$ $$m^2 s^{-1}$$.

The spin-up is now configured. We have kept the default time-step value `rn_Dt = 14400.` in the namelist, wich corresponds to a 4 hours time-stepping between each iteration.
The simulation will then last 10 years (this can be easily changed by setting the final iteration _ǹn_itend_ accordingly).

Before running the model, we will add extra variables using XIOS.

## Adding new variable to the output diagnostics using XIOS

The NEMO strategy to manage input and output files is based on XIOS.
The output files that will be saved during the simulation can be defined for each experiment in its top-level folder within the **file_def_nemo.xml** file.
The _EXPREF_ folder already provides a default xml file that allows to store variables every 5 days as well as additional diagnostic limited to yearly frequency. 

> **Note:** XIOS provides different methods to pre-process the data before storing. By default, variables are time-averaged to the period defined by the 'output_freq' attribute of a 'file_group' entry.

```
TODO: Explain here file changes
```

## Summary

