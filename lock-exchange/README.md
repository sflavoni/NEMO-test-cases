# Lock Exchange demonstration case

Here a description of the test case + link toward the src and notebooks. 


## Objectives

The lock exchange experiment can be use to see the impact of different tracer advection schemes into spurious mixing. 

## Physical description

For the lock exchange test case, a closed two-dimensional vertical domain with a constant depth of H = 20 m and a length of L = 64 km is considered. Initially, the left half of the domain (x < 32 km) has a density of σt = 5 kg m−3 and the right half of the domain (x ⩾ 32 km) has a density of σt = 0 kg m−3, separated by a vertical line.
Initial surface elevation and velocity are zero.
At t = 0, the separation is removed such that the dense water is forced under the fresh water.
Earth rotation, bed friction and mixing are neglected, such that the effective density mixing is only due to advection of density.
This scenario been suggested by Haidvogel and Beckmann (1999) as a test case for advection schemes in ocean models, and has been intensively used by Burchard and Bolding (2002) for testing the advection schemes in GETM.
Here, the numerical mixing of the first-order upstream (UBS) and the FCT2 and FCT4 schemes will be assessed.

<img src="./figures/start-lock-exchange.001.jpeg">

<b> Choice done for ALL experiments is :</b>

- **laplacian lateral diffusion on momentum** (see namelist block: "namdyn_ldf")
- **horizontal direction** (see namelist block: "namdyn_ldf" ln_dynldf_hor=.true.)
- **with coefficient 0.01** (see namelist block: "namdyn_ldf" coefficient rn_ahm_0)

You've download, installed and compiled LOCK_EXCHANGE test cases. The executable opa in TEST_CASES/LOCK_EXCHANGE/EXP00 directory


# First experiment EXP01:

* **COPY EXP00 directory in EXP01 :**

> cd TEST\_CASES/MY\_LOCK\_EXCHANGE
 <br>cp -R EXP00 EXP01

in NEMOGCM/CONFIG/TEST_CASES/MY_LOCK_EXCHANGE/EXP01 directory there are some namelists available: 

choice the *namelist\_FCT4\_vect\_ens\_cfg* one and link it into the namelist_cfg (read by opa):
> ln -sf namelist\_FCT4\_vect\_ens\_cfg namelist_cfg


## EXP1 : choice of namelist\_FCT4\_vect\_ens\_cfg :
- **FCT4** Advection scheme: FCT (flux-corrected transport scheme) 4th order on horizontal and vertical
- **vect** Vector formulation of the momentum advection
- **ens** Vorticity energy conserving scheme

* Run the EXP1 :
> mpirun -np 1 ./opa


* You'll have the output file **"LOCK\_FCT4\_vect\_ens\_grid\_T.nc"**
> output file name is set in EXP01/file\_def\_nemo-opa.xml
<br> in variable name="@expname@"