# OVERFLOW demonstration case

Here a description of the test case + link toward the src and notebooks. <br>
The OVERFLOW experiment is inspired by the non-rotating overflow configuration similar to that described in Haidvogel and Beckmann (1999).
It can be used to investigate the impact of topography on spurious mixing, here we set experiment like Ilıcak, M. et al. "Spurious dianeutral mixing and the role of momentum closure", Ocean Modelling , 45-46, 37-58, 2012

This experiment is **created and tested** for NEMO **code at revision 8097**

## Objectives

The OVERFLOW experiment can be use to see the impact of different tracer advection schemes or vertical cooridnates into spurious mixing.
Here there is a physical description of this experiment, and a notebook is available to show some possible analysis. <br>
If you've already some outputs you can directly look at the notebook.

## Physical description

The domain is a 2000 mdeep, two-dimensional (x-z) steep topographic slope initialized with dense water on the shelf. The velocity field is initially at rest. A vertical density front with a 2 kg m−3 difference is located at x=20 km. There is initially no stratification in the off-shelfregion. The geometry and initial conditions are illustrated in figure:

<img src="./figures/overflow_init.jpg">

This test case is directly analogous to Lock_Exchange, only now with a topographic slope down whichthe dense water flows. We hold the horizontal grid spacing constant at ∆x=1 km, and ∆z=20 m (100-layers). The vertical viscosity is held constant throughout the test suite at a value of 10−4m2/s. Initial surface elevation and velocity are zero. Salinity is constant ( at 35 psu ) and initial cold dense water ( temperature at 10°C ) on the shallow slope, and light warm water ( temperature at 20°C ) throughout the remainder of the domain.
At t = 0, the separation is removed such that the dense water is forced under the fresh water, and the system evolves for 9 hours : 

Here figure from Ilıcak, M. et al. "Spurious dianeutral mixing and the role of momentum closure", Ocean Modelling , 45-46, 37-58, 2012.

<img src="./figures/overflow_end.jpg">

The left column shows the simulations three hours after the initial condition, and the right column shows snapshots after nine hours, with GOLD model. 

## How to set experiment

NEMO code needs : 

* <b>namelist_ref</b> : namelist of reference in which ALL parameters are declared
* <b>namelist_cfg</b> : blocks of namelist of the specific configuration, in which you can set specific parameters. It need to be used to overwrite namelist\_ref blocks 

<b> choice is done for ALL experiments for next parameters :</b>

- **laplacian lateral diffusion on momentum** (see namelist block: "namdyn_ldf")
- **horizontal direction** (see namelist block: "namdyn_ldf" ln_dynldf_hor=.true.)
- **with coefficient 0.01** (see namelist block: "namdyn_ldf" coefficient rn_ahm_0)

## Experiment:

* Set of LOCK EXCHANGE run : <br>
* Choice of vertical cooridnates (z-partial cells or s-coordinates)
* Choice of : FCT4 advection scheme, vector invariant form, energy conservation

in NEMOGCM/CONFIG/TEST_CASES/MY_OVERFLOW/EXP00 directory there are some namelists available: 

## Description of namelist\_zps\_FCT4\_vect\_ens\_cfg :
```
ln -sf namelist_zps_FCT4_flux_cen2_cfg namelist_cfg
```

- **FCT4** Advection scheme: FCT (flux-corrected transport scheme) 4th order on horizontal and vertical
- **flux** Invartiant Flux formulation of the momentum advection
- **cen2** Second order scheme

Run the executable :
``` mpirun -np 1 ./opa ```

Output files : <br>

OVF\_FCT4\_vect\_ens\_grid\_T.nc, <br>
OVF\_FCT4\_vect\_ens\_grid\_U.nc, <br>
OVF\_FCT4\_vect\_ens\_grid\_V.nc, <br>
OVF\_FCT4\_vect\_ens\_grid\_W.nc

<pre>
NOTA: output file name is set into EXP00/<b>file_def_nemo-opa.xml</b>
in variable <b>name="@expname@"</b>
</pre>

When output files are created see the notebook to start some analysis.