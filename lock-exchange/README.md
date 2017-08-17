# Lock Exchange demonstration case

Here a description of the test case + link toward the src and notebooks. 
<br>
The LOCK EXCHANGE experiment has been suggested by Haidvogel and Beckmann (1999) as a test case for advection schemes in ocean models, and has been intensively used by Burchard and Bolding (2002) for testing the advection schemes in GETM.

## Objectives

The LOCK EXCHANGE experiment can be use to see the impact of different tracer advection schemes into spurious mixing. <br>
Here there is a physical description of this experiment, and a notebook is available to show some possible analysis. <br>
If you've already some outputs you can directly look at LOCK_EXCHANGE notebook.

## Physical description

For the lock exchange test case, a closed two-dimensional vertical domain with a constant depth of H = 20 m and a length of L = 64 km is considered. Initially, the left half of the domain (x < 32 km) has a density of σt = 5 kg m−3 and the right half of the domain (x ⩾ 32 km) has a density of σt = 0 kg m−3, separated by a vertical line.
Initial surface elevation and velocity are zero.<br>
At t = 0, the separation is removed such that the dense water is forced under the fresh water. Earth rotation, bed friction and mixing are neglected, such that the effective density mixing is only due to advection of density.
<br>
Here, numerical mixing of the second-order FCT2 and fortht-order FCT4 schemes will be assessed.<br> 
<img src="./figures/start-lock-exchange.001.jpeg">
<br>

## HOW TO Compile TEST CASES 
 
* compile LOCK_EXCHANGE test case : 

instructions availables for NEMO 4.0 
 
<pre>
cd my_TEST/NEMOGCM/CONFIG
./makenemo -a TEST_CASES -n <i>my_LOCK_EXCHANGE</i> -r LOCK_EXCHANGE -m <i>your_arch_file</i>
</pre>

<b> Now TEST CASE "LOCK_EXCHANGE" code is installed and compiled. </b>

The executable <b>opa</b> in TEST\_CASES/LOCK\_EXCHANGE/EXP00 directory.<br>
NEMO code needs : 

* <b>namelist_ref</b> : namelist of reference in which ALL parameters are declared
* <b>namelist_cfg</b> : blocks of namelist of the specific configuration, in which you can set specific parameters. It need to be used to overwrite namelist\_ref blocks 

In EXP00 directory there are available also some pre-set namelist\_cfg with some choices already done. To activate one of this namelist\_xxx\_cfg just rename or do a link to namelist_cfg.

<b> choice is done for ALL experiments for next parameters :</b>

- **laplacian lateral diffusion on momentum** (see namelist block: "namdyn_ldf")
- **horizontal direction** (see namelist block: "namdyn_ldf" ln_dynldf_hor=.true.)
- **with coefficient 0.01** (see namelist block: "namdyn_ldf" coefficient rn_ahm_0)

## Experiment:

* Set of LOCK EXCHANGE run : <br>
*  Choice of : FCT4 advection scheme, vector invariant form, energy conservation

```
ln -sf namelist_FCT4_vect_ens_cfg namelist_cfg
```
### Description of namelist\_FCT4\_vect\_ens\_cfg :
- **FCT4** Advection scheme: FCT (flux-corrected transport scheme) 4th order on horizontal and vertical
- **vect** Vector formulation of the momentum advection
- **ens** Vorticity energy conserving scheme

Run the executable :
``` mpirun -np 1 ./opa ```

Output files : <br>
LOCK\_FCT4\_vect\_ens\_grid\_T.nc, <br>
LOCK\_FCT4\_vect\_ens\_grid\_U.nc, <br>
LOCK\_FCT4\_vect\_ens\_grid\_V.nc, <br>
LOCK\_FCT4\_vect\_ens\_grid\_W.nc

<pre>
NOTA: output file name is set into EXP00/<b>file_def_nemo-opa.xml</b>
in variable <b>name="@expname@"</b>
</pre>

When output files are created see the notebook to start some analysis