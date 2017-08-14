# OVERFLOW demonstration case

Here a description of the test case + link toward the src and notebooks. 
The OVERFLOW experiment has been suggested <b> TO BE DONE!!! xxxx </b>


## Objectives

The OVERFLOW experiment can be use to see the impact of different tracer advection schemes into spurious mixing. 

<b> TO BE DONE!!! xxxx </b>

## Physical description

<b> TO BE DONE!!! xxxx </b>

<b> PUT image!!!! </b>

<img src="./figures/start-lock-exchange.001.jpeg">

##Compile TEST CASES 
 
* compile OVERFLOW test case : 

<pre>
cd my_TEST/NEMOGCM/CONFIG
./makenemo -a TEST_CASES -n <i>my_OVERFLOW</i> -r OVERFLOW -m <i>your_arch_file</i>
</pre>

<b> Now TEST CASE "OVERFLOW" code is installed and compiled. </b>

You can find it in my_TEST/NEMOGCM/CONFIG/OVERFLOW/my\_OVERFLOW.
The executable opa in TEST\_CASES/OVERFLOW/EXP00 directory.
In EXP00 directory there are available also some pre-set namelist_cfg with some choices already done. 
You've download, installed and compiled OVERFLOW test cases.


<b> choice is done for ALL experiments for next parameters :</b>

- **laplacian lateral diffusion on momentum** (see namelist block: "namdyn_ldf")
- **horizontal direction** (see namelist block: "namdyn_ldf" ln_dynldf_hor=.true.)
- **with coefficient 0.01** (see namelist block: "namdyn_ldf" coefficient rn_ahm_0)

## First experiment:

* Set of OVERFLOW run (choice in namelist_cfg)

NEMO code read namelist\_cfg (that overwrites namelist_ref parameters)

in NEMOGCM/CONFIG/TEST_CASES/MY_OVERFLOW/EXP00 directory there are some namelists available: 

## Description of namelist\_FCT4\_vect\_ens\_cfg :
```
ln -sf namelist_FCT4_vect_ens_cfg namelist_cfg
```
- **FCT4** Advection scheme: FCT (flux-corrected transport scheme) 4th order on horizontal and vertical
- **vect** Vector formulation of the momentum advection
- **ens** Vorticity energy conserving scheme

* Run the executable :
``` mpirun -np 1 ./opa ```

* All output file will be :  OVF\_FCT4\_vect\_ens\_grid\_T.nc, OVF\_FCT4\_vect\_ens\_grid\_U.nc, OVF\_FCT4\_vect\_ens\_grid\_V.nc, OVF\_FCT4\_vect\_ens\_grid\_W.nc

```
output file name is set in EXP00/file_def_nemo-opa.xml
in variable name="@expname@"
```