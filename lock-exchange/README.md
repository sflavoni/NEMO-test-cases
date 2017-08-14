# Lock Exchange demonstration case

Here a description of the test case + link toward the src and notebooks. 
The LOCK EXCHANGE experiment has been suggested by Haidvogel and Beckmann (1999) as a test case for advection schemes in ocean models, and has been intensively used by Burchard and Bolding (2002) for testing the advection schemes in GETM.

## Objectives

The LOCK EXCHANGE experiment can be use to see the impact of different tracer advection schemes into spurious mixing. 

## Physical description

For the lock exchange test case, a closed two-dimensional vertical domain with a constant depth of H = 20 m and a length of L = 64 km is considered. Initially, the left half of the domain (x < 32 km) has a density of σt = 5 kg m−3 and the right half of the domain (x ⩾ 32 km) has a density of σt = 0 kg m−3, separated by a vertical line.
Initial surface elevation and velocity are zero.
At t = 0, the separation is removed such that the dense water is forced under the fresh water.
Earth rotation, bed friction and mixing are neglected, such that the effective density mixing is only due to advection of density.

Here, the numerical mixing of the first-order upstream (UBS) and the FCT2 and FCT4 schemes will be assessed.

<img src="./figures/start-lock-exchange.001.jpeg">

##Compile TEST CASES 
 
* compile LOCK_EXCHANGE test case : 

<pre>
cd my_TEST/NEMOGCM/CONFIG
./makenemo -a TEST_CASES -n <i>my_LOCK_EXCHANGE</i> -r LOCK_EXCHANGE -m <i>your_arch_file</i>
</pre>

<b> Now TEST CASE "LOCK_EXCHANGE" code is installed and compiled. </b>

You can find it in my_TEST/NEMOGCM/CONFIG/TEST\__CASES/my\_LOCK\_EXCHANGE.
The executable opa in TEST\_CASES/LOCK\_EXCHANGE/EXP00 directory.
In EXP00 directory there are available also some pre-set namelist_cfg with some choices already done. 
You've download, installed and compiled LOCK\_EXCHANGE test cases.


<b> choice is done for ALL experiments for next parameters :</b>

- **laplacian lateral diffusion on momentum** (see namelist block: "namdyn_ldf")
- **horizontal direction** (see namelist block: "namdyn_ldf" ln_dynldf_hor=.true.)
- **with coefficient 0.01** (see namelist block: "namdyn_ldf" coefficient rn_ahm_0)

## First experiment:

* Set of LOCK EXCHANGE run (choice in namelist_cfg)

NEMO code read namelist\_cfg (that overwrites namelist_ref parameters)

in NEMOGCM/CONFIG/TEST_CASES/MY_LOCK_EXCHANGE/EXP00 directory there are some namelists available: 

## Description of namelist\_FCT4\_vect\_ens\_cfg :
```
ln -sf namelist_FCT4_vect_ens_cfg namelist_cfg
```
- **FCT4** Advection scheme: FCT (flux-corrected transport scheme) 4th order on horizontal and vertical
- **vect** Vector formulation of the momentum advection
- **ens** Vorticity energy conserving scheme

* Run the executable :
``` mpirun -np 1 ./opa ```

* All output file will be :  LOCK\_FCT4\_vect\_ens\_grid\_T.nc, LOCK\_FCT4\_vect\_ens\_grid\_U.nc, LOCK\_FCT4\_vect\_ens\_grid\_V.nc, LOCK\_FCT4\_vect\_ens\_grid\_W.nc

```
output file name is set in EXP00/file_def_nemo-opa.xml
in variable name="@expname@"
```